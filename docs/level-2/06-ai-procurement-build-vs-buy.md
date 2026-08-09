# 06 · AI Procurement & Build-vs-Buy Decisions

Build-vs-buy is usually decided before anyone runs the analysis. An
engineering-led organisation builds; a lean organisation buys; and the
memo produced afterwards rationalises the instinct. Both instincts are
right often enough to survive, which is why the pattern persists.

The decision deserves better, because it is expensive in a specific way: it
is hard to reverse. A built system carries a permanent maintenance
obligation you cannot walk away from. A bought system embeds a dependency
in your product and your data flows, and switching costs compound quietly.
Either way you are choosing for roughly three years.

This module gives you a scoring matrix for the strategic side, a total-cost
model for the financial side, and a due-diligence checklist for the vendor
side. The order matters: strategy narrows the field, cost breaks the tie,
diligence protects you from the option you chose.

## 1. There are four options, not two

Framing the choice as build-or-buy hides the two that most often win.

| Option | What it means | Best when |
|---|---|---|
| **Buy** | Commercial product handles the capability end to end | The capability is undifferentiated and a mature market exists |
| **Build** | You develop and operate it | The capability *is* your differentiation, or your data makes it uniquely feasible |
| **Buy and wrap** | Vendor model or API underneath; your orchestration, data, evaluation, and UX on top | Very common in practice — the model is a commodity, the integration is not |
| **Don't** | Solve it with a rule, a process change, or not at all | More often than anyone admits |

"Buy and wrap" deserves a specific look, because it is where most current
AI work actually sits. You are not building a model; you are building
retrieval, evaluation, guardrails, and workflow around someone else's
model. Budget it as engineering work — it is — while recognising the model
itself is replaceable.

And keep "don't" alive as a real option through the whole process. A team
that has spent six weeks evaluating vendors will find it psychologically
very hard to conclude that a three-rule heuristic captures 70% of the
value, which is why you should ask for the heuristic's number in week one.

## 2. The decision matrix

Score build and buy 1–5 on each criterion. Weights should be set — and
written down — *before* any scores are entered, or the weights will quietly
be tuned until the preferred answer wins.

| Criterion | Weight | What a high build score means | What a high buy score means |
|---|---|---|---|
| **Strategic differentiation** | 25 | Customers choose us partly because of this | Nobody chooses a vendor over this |
| **Time to value** | 20 | We can ship fast with existing people | Working next quarter |
| **Total cost over 3 years** | 20 | Cheaper to own at our volume | Cheaper to rent at our volume |
| **Data sensitivity & control** | 15 | Data cannot leave our boundary | Vendor terms are acceptable |
| **Switching / lock-in risk** | 10 | We own it outright | Exit is cheap and tested |
| **Team capability & capacity** | 10 | We have the people, with slack | We don't, and hiring is slow |

Three rules of use. **Differentiation carries the heaviest weight for a
reason** — building undifferentiated capability is the most reliable way to
waste an engineering team. **Capacity is not capability**: a team that
could build it but is fully committed scores low, and "we'll hire" is a
6–9 month assumption you must price. And **a close score is information**:
within a few points, the strategic case is genuinely neutral and the
decision should fall to cost and reversibility, not to the louder advocate.

## 3. Total cost of ownership

Sticker price is the smallest term on both sides. Model three years, and
separate one-off from recurring.

| Cost line | Build | Buy |
|---|---|---|
| Development | Team × months, fully loaded | — |
| Integration | Included above | Usually 20–50% of year-one licence |
| Licence / usage fees | — | Per seat, per call, or per unit |
| Training & experiment compute | Real, often underestimated | — |
| Inference / serving infrastructure | Yours | Vendor's (in the fee) |
| Ongoing maintenance | 15–25% of build cost per year, forever | Reduced, not zero |
| Monitoring & MLOps | Yours to fund (Module 03) | Partly vendor's; verify |
| Vendor management | — | 0.1–0.3 FTE, plus renewals |
| Exit cost | Low | Re-integration, data extraction, retraining staff |

**Fully loaded** means salary plus benefits, tooling, management overhead
and recruiting cost — typically 1.25–1.4× salary. Using base salary
understates build cost by roughly a third, which is the single most common
error in these analyses.

The maintenance row is where build cases quietly fail. A system built by
2.5 people does not maintain itself; budget a durable fraction of a
headcount for as long as the system lives, and put that number in the model
before anyone gets attached to the answer.

## 4. Vendor due diligence

Once you're buying, these are the questions that separate a vendor
relationship from a hostage situation. Get answers in writing.

| Area | Ask | Answer that should worry you |
|---|---|---|
| **Quality evidence** | Performance on *our* data, not their benchmark | "Our benchmark shows 94%" with no offer to run a pilot |
| **Data handling** | Is our data retained? Used for training? Where processed? | Vague, or "configurable" without contract language |
| **Model change policy** | Notice period when the underlying model changes | "We continuously improve" — meaning your behaviour changes without warning |
| **Evaluation access** | Can we run our own eval set continuously? | Output-only API with no batch access |
| **Failure behaviour** | What happens on outage or low confidence? | No documented fallback |
| **Exit** | Can we export data, configuration, and history? Format? | "Talk to your account manager" |
| **Roadmap dependency** | Does our use case need something unreleased? | Anything sold on a roadmap promise |
| **Viability** | Funding stage, customer count, support model | Single-customer concentration; unclear runway |

Two of these carry outsized weight. **Model change policy** is unique to
AI procurement — with traditional software, version upgrades are events you
schedule; with hosted models, behaviour can shift under you without a
version number. Insist on notice and the ability to pin a version.
**Evaluation access** is what makes the first item enforceable: without
your own continuous eval, you cannot detect the change even after it
happens.

The single most useful procurement action is a **paid pilot on your own
data with your own evaluation set**, before commitment. Vendors who resist
this are telling you something.

## 5. Contract terms a manager should insist on

You are not the lawyer, but these five are business terms and they are
yours to raise.

| Term | Why |
|---|---|
| No training on our data, in writing | Default terms often permit it |
| Version pinning + 60–90 days' notice of model changes | Protects against silent behaviour shifts |
| Quality floor with a remedy | Turns a marketing claim into an obligation |
| Data export on demand and at termination, in a documented format | Makes exit real |
| 12-month initial term, not 36 | AI markets reprice fast; long lock-ins have aged badly |

## Worked example

An insurance operations team processed **40,000 documents a month** —
claims forms, medical letters, correspondence — extracting fields by hand.
The question: build an extraction model or buy a document-AI product.

**Step 1 — the matrix.** Weights set at kickoff, scored jointly by the ML
lead and the ops director.

| Criterion | Weight | Build (1–5) | Buy (1–5) | Build weighted | Buy weighted |
|---|---|---|---|---|---|
| Strategic differentiation | 25 | 4 | 2 | 100 | 50 |
| Time to value | 20 | 2 | 5 | 40 | 100 |
| 3-year total cost | 20 | 2 | 4 | 40 | 80 |
| Data sensitivity & control | 15 | 5 | 3 | 75 | 45 |
| Switching / lock-in risk | 10 | 5 | 2 | 50 | 20 |
| Team capability & capacity | 10 | 2 | 5 | 20 | 50 |
| **Total (max 500)** | **100** | | | **325** | **345** |

Twenty points apart on a 500-point scale — statistically meaningless given
the subjectivity of the scores. The honest reading is *the strategic case
is a tie*, which is itself the finding: this capability is not where the
company differentiates, whatever the ML lead's 4 on differentiation
suggested. The decision moved to cost.

**Step 2 — three-year TCO.** Fully loaded salaries: ML engineer $180,000,
vendor-ops half-headcount $160,000.

| | Year 1 | Year 2 | Year 3 | 3-year total |
|---|---|---|---|---|
| **Buy** — licence ($0.12/doc), $2,500/mo platform, 0.5 FTE ops, $60k one-off integration | $227,600 | $167,600 | $167,600 | **$562,800** |
| **Build** — 2.5 FTE × 9 months ($337,500), $40k training compute, then 1.0 FTE + $18k infra + $0.015/doc inference | $428,800 | $205,200 | $205,200 | **$839,200** |

Buy is **$276,400 cheaper over three years** at current volume, and it
delivers roughly seven months sooner.

**Step 3 — the break-even question.** Build has high fixed cost and very
low marginal cost ($0.015/doc versus $0.12/doc); buy is the reverse. So the
answer is volume-dependent, and the useful number is the crossover:

> At **~110,600 documents per month**, the two options cost the same over
> three years. Below that, buy wins; above it, build wins.

That is **2.8× current volume**. The team's own five-year growth plan
reached about 65,000 documents a month. So buy wins across the entire
planning horizon, not just today — a far stronger conclusion than "buy is
cheaper right now," and one that survives the inevitable "but we're
growing" objection.

**Step 4 — diligence changed the deal.** Two findings from the checklist:

- The default contract permitted the vendor to use submitted documents to
  improve its models. For medical correspondence, unacceptable. Negotiated
  out; the vendor had a standard no-training addendum but did not offer it
  unprompted.
- The vendor could not commit to notice on model updates. Compromise: a
  pinned model version with 90 days' notice before forced migration, plus
  API access to run the team's own 500-document eval set weekly.

**Step 5 — the decision.** Buy, on a 12-month term with the two amendments,
plus a $15,000 paid pilot on 2,000 real documents first. The pilot measured
field-level accuracy at 91% against the vendor's claimed 96% — a gap large
enough to change the staffing plan for human review, and one that would
have surfaced as a nasty surprise three months into production. The
staffing plan was adjusted before signature rather than after.

Note what did most of the work. The matrix did not pick the winner; it
established that nothing strategic was at stake. The break-even volume,
not the point-in-time cost, made the decision durable. And the pilot — 2.7%
of first-year spend — corrected an assumption that would have broken the
operating model.

## Exercise

Take a real or plausible AI capability decision facing your organisation.

1. **List all four options** from section 1, including "don't." Write one
   sentence on what "don't" would look like and roughly what fraction of
   the value it captures. Get an actual number for the heuristic baseline.
2. **Set the weights first.** Fill in the matrix column of weights and
   circulate it *before* anyone scores. Note any pressure you get to change
   the weights afterwards.
3. **Score both options** with at least two people scoring independently,
   then reconcile. Treat any total within ~10% as a tie.
4. **Build the three-year TCO** using section 3's line items. Use fully
   loaded salaries at 1.3× base, and include the maintenance line for the
   build option in every year.
5. **Find the break-even volume** — the level at which the two options
   cost the same. Compare it to your growth plan. This single number is
   usually the most persuasive slide in the whole analysis.
6. **Run the diligence checklist** against your leading vendor and mark
   every answer you do not have in writing. Pick the two most important and
   get them in writing before any commitment.
