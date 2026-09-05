# 03 · Managing LLM/GenAI Initiatives

Classical ML projects fail in fairly predictable ways: bad data, wrong
metric, model doesn't generalize. LLM and generative AI projects fail in
those ways too, plus a set of new ones that catch experienced managers off
guard, because the earlier intuitions about "the model is deterministic
enough to spec against" stop applying. This module covers what changes
specifically when the initiative is LLM-based, not classical ML — scoping,
cost structure, evaluation, and the vendor dependency that comes bundled
with using someone else's foundation model.

## 1. What's actually different about LLM initiatives

| Dimension | Classical ML project | LLM/GenAI project |
|---|---|---|
| Where the capability comes from | Usually trained in-house on your data | Usually a third-party foundation model, adapted via prompting or fine-tuning |
| Cost structure | Mostly fixed (compute for training), predictable | Variable, per-token, scales with usage — can spike unexpectedly |
| Output space | Bounded (a class, a score, a ranked list) | Open-ended text/code/image — infinite failure surface |
| Evaluation | Fixed metric on a frozen holdout | Harder to define "correct"; often needs human or LLM-judge grading |
| Failure mode | Wrong prediction | Wrong prediction *plus* hallucination, prompt injection, unsafe/off-brand output |
| Vendor dependency | Usually low (your model, your infra) | Often high (model version changes, deprecations, and price changes are outside your control) |
| Time to first demo | Weeks (needs data + training) | Hours (a good prompt looks like a product) — creating a "it's basically done" illusion |

That last row is the trap that catches the most managers: a compelling demo
in an afternoon does not mean the system is close to production-ready. The
gap between demo and production is usually 80% of the real project — eval
harness, guardrails, cost control, and handling the long tail of inputs the
demo never saw.

## 2. Scoping an LLM initiative correctly

Because the output space is open-ended, "does it work" is not a yes/no
question the way it is for classical ML. Force the team to commit, before
building, to:

| Field | Purpose | Example |
|---|---|---|
| Task definition | Exact input/output contract | "Given a support ticket + account history, draft a reply a human can send after ≤30 seconds of editing" |
| Quality bar | What "good enough" means, operationalized | "Human editor accepts with no factual correction in ≥85% of drafts" |
| Grading method | How quality gets measured at scale | LLM-judge against a rubric, calibrated monthly against 100 human-graded samples |
| Cost ceiling | Per-interaction and monthly budget | "≤$0.02/ticket; ≤$8K/month at current volume" |
| Guardrail requirements | What the system must never do | "Never quote a specific refund amount without a tool call verifying account balance" |
| Fallback behavior | What happens when confidence is low | "Route to human queue if judge score <7/10 or tool call fails" |
| Vendor exposure | What breaks if the model changes | "Prompt tested against two model families; contract includes 90-day deprecation notice" |

## 3. Evaluation for open-ended output

You cannot hold out a labeled test set the way you would for classification
and call it done — but you also cannot skip evaluation because "it's
subjective." Build a layered eval approach:

| Layer | What it catches | Cadence |
|---|---|---|
| Deterministic checks (schema validity, banned phrases, PII leakage, tool-call correctness) | Structural failures, safety violations | Every request, automated, blocking |
| LLM-judge scoring against a rubric | Quality drift, tone, factual grounding | Sampled continuously; full run on every prompt/model change |
| Human spot-check | Judge calibration, edge cases the rubric misses | Weekly, 20-50 samples, done by someone who wasn't on the build team |
| Production signal (edit rate, escalation rate, user complaints) | Real-world quality that offline eval misses | Continuous dashboard |

The rubric for the LLM-judge layer should be written by a human first,
in plain language, before any judge prompt is built — teams that skip this
step end up with a judge that scores "sounds confident" rather than "is
correct."

## 4. Cost and vendor risk management

LLM costs scale with usage in a way training-based ML costs mostly don't,
and foundation-model vendors change pricing, deprecate models, and shift
behavior on updates outside your control. Manage both proactively:

- **Set a per-feature cost ceiling before launch**, not after the first
  invoice. A feature that costs $0.02/interaction at 10K/month costs
  $2,000/month; the same feature at 500K/month is $10,000/month — model
  this before scaling traffic, not after finance asks questions.
- **Test against at least two model providers or model families** before
  committing prompts and infrastructure irreversibly to one. This is
  insurance, not necessarily a multi-vendor production strategy.
- **Track model version pinning.** Silent model upgrades from a vendor can
  change output quality without any code change on your side. Pin versions
  in production and test new versions in a staging eval before adopting.
- **Negotiate deprecation notice periods** in vendor contracts (see Module
  8) — a model your prompts depend on being retired with 30 days' notice is
  a fire drill; 6 months' notice is a planned migration.

## Worked example

A media company, Fenwick Publishing, launched an LLM feature to auto-generate
article summaries for its mobile app. The demo, built in two days, looked
excellent on the ten articles the team tried it on. Leadership approved a
six-week timeline to full launch based on that demo.

At week 3, the eval layer (built per section 3, over the team's objection
that it was "slowing things down") surfaced two problems the demo had
missed: on articles involving ongoing legal cases, the model occasionally
stated outcomes as settled when they were still pending (a factual-grounding
failure invisible in the ten cherry-picked demo articles), and cost per summary was $0.15 (long-article context plus a generous output
length) — a manageable $900/month at the 200 articles/day the newsroom
currently published, but the product team's actual target was 3,000
articles/day across a planned expansion, which would have put monthly cost
at $13,500 against an approved budget of $6,000.

Both were caught before launch because the eval and cost-ceiling steps
were mandatory checkpoints, not optional add-ons. The fix: a deterministic
check added to flag any summary of an article tagged "ongoing litigation"
for mandatory human review, and a prompt-compression pass that cut token
usage by 40%, bringing projected cost to $8,100/month — still above the
original budget, but a plannable conversation about raising it rather than
a surprise invoice discovered after scale-up.

## How It Actually Works

The "demo looks basically done" illusion has a specific mechanical cause: a
demo built on ten hand-picked or hand-tried articles samples from exactly
the region of input space the builder already knows the model handles well,
because they kept iterating on prompts until those ten examples looked
good. That process, by construction, cannot surface a failure mode that
only appears on inputs outside the demo set — like articles about ongoing
litigation, which is a thin slice of the full article distribution and
therefore was never among the ten chances the builder happened to try. This
is the same distributional mismatch as a vendor's cherry-picked benchmark
in Module 07 of Level 1, just self-inflicted rather than sold to you: a
system's apparent quality is always relative to whatever inputs it was
checked against, and a demo's input set is selected — consciously or not —
for exactly the property of "looking good," which structurally excludes
the long tail where production failures live.

The cost blow-up at scale is a mechanical consequence of how LLM pricing
composes with traffic growth in a way training-based ML cost does not: a
classical model's training cost is paid once regardless of how many
predictions it later serves, so inference is comparatively cheap and mostly
fixed-infrastructure; an LLM API charges per token on every single call, so
total cost is a direct linear function of interaction volume with no
amortization effect. Fenwick's summary feature didn't get less efficient
between 200 and 3,000 articles/day — the per-call cost stayed the same
$0.15 — but because that cost multiplies against volume with no fixed
component to spread it over, a 15x volume increase produces almost exactly
a 15x cost increase. This is exactly why "model the cost at your real
planned scale before launch" isn't caution for its own sake — a linear
cost function has no forgiving regime the way amortized fixed costs do; the
invoice at scale is knowable in advance from the per-call cost and the
volume plan alone, with no surprises hiding in between.

## Exercise

Take an LLM/GenAI initiative your org is running or considering.

1. **Fill in the seven-field scoping template** in section 2. If any field
   can't be answered yet, that's your finding — name who needs to answer it
   before development proceeds.
2. **Design the four-layer eval approach** from section 3 specifically for
   this initiative: what are the deterministic checks, what's in the judge
   rubric, who does the weekly human spot-check, and what production signal
   will you watch?
3. **Model the cost at 10x current volume** using the arithmetic pattern in
   the worked example. If nobody can currently state per-interaction cost,
   that's the first gap to close.
