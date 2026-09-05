# 08 · Vendor & Partner Management for AI

AI vendor relationships carry risks generic software procurement doesn't:
model behavior can change without a version bump you control, pricing is
often usage-based and hard to forecast, and switching costs are higher than
they look at signing time because your prompts, evals, and integrations
become entangled with one vendor's specific model behavior. As a manager,
your job is to negotiate and manage these relationships so a vendor
decision made in month one doesn't become an unplanned dependency you
discover in month eighteen.

## 1. Build vs. buy vs. partner — the decision framework

| Factor | Favors build | Favors buy (vendor product) | Favors partner (co-development) |
|---|---|---|---|
| Differentiation | Core to competitive advantage | Commodity capability, not a differentiator | Strategic but you lack in-house depth |
| Data sensitivity | Highly sensitive data that can't leave your environment | Vendor has strong compliance posture, contractually verified | Depends entirely on the specific data-sharing terms |
| Time to value | You can tolerate a longer build timeline | Need capability in weeks, not quarters | Willing to trade some timeline for shared IP/cost |
| Total cost of ownership over 3 years | In-house team cost is lower than vendor fees at your scale | Vendor's economies of scale beat your build+maintain cost | Shared cost, shared (and negotiated) upside |
| Long-term flexibility needed | High — you expect requirements to diverge significantly from any vendor roadmap | Low — a standard capability with well-understood requirements | Medium — negotiate roadmap input as part of the deal |

Run this analysis per capability, not once for "AI" as a category — a
company might reasonably build its core recommendation model in-house while
buying its LLM API access and partnering on a specialized vision model for
a niche use case.

## 2. Vendor evaluation criteria specific to AI

Beyond standard procurement criteria (price, support, security), score AI
vendors specifically on:

| Criterion | Question to ask | Red flag answer |
|---|---|---|
| Model versioning transparency | "How do you notify us of model updates, and can we pin a version?" | "We update continuously and don't version" |
| Deprecation policy | "What's your minimum notice period before deprecating a model we depend on?" | Anything under 90 days for a production dependency |
| Data usage rights | "Is our data used to train your models, and can we opt out?" | Vague or "yes, per our standard terms" with no opt-out |
| Evaluation transparency | "Can we run our own eval suite against your model before committing?" | Only pre-packaged benchmark numbers, no sandbox access |
| Explainability/audit support | "Can you provide the documentation our compliance team needs for [applicable regulation]?" | "That's not something we typically provide" |
| Cost predictability | "What happens to our bill if usage spikes 5x unexpectedly?" | No rate limiting, alerting, or spend cap options offered |
| Exit/portability | "What does migrating off your platform actually involve?" | Proprietary formats with no export path |

Score each vendor 1-5 on each row and weight by how much that risk matters
for your specific use case — data usage rights matter enormously for a
healthcare application and much less for an internal engineering tool.

## 3. Contract terms worth negotiating specifically

| Term | Why it matters for AI specifically | Reasonable ask |
|---|---|---|
| Deprecation notice period | Silent model retirement breaks production without warning | 90-180 days minimum for anything production-critical |
| Version pinning | Prevents unannounced quality drift from a vendor-side model update | Right to pin a specific model version for a defined period |
| Usage-based price caps or alerts | LLM costs scale with usage in ways fixed-license software doesn't | Contractual alert thresholds, not just a bill at month-end |
| Data processing terms | Determines governance exposure (Module 2) | Explicit opt-out of training use; data residency guarantees if needed |
| SLA on latency/availability | AI features often sit on a critical user-facing path | Defined uptime and latency percentiles with credits for breach |
| Audit/documentation rights | Needed to satisfy your own compliance reviews | Contractual right to request model cards, bias testing summaries |

## 4. Ongoing vendor management, not just the signing

The relationship doesn't end at contract signature. Run a lightweight
recurring review:

| Cadence | Activity |
|---|---|
| Monthly | Spend vs. forecast check; any usage anomalies |
| Quarterly | Re-run your eval suite against the current live model version — catches silent drift |
| Annually | Renegotiate based on actual usage patterns and market rate changes; re-run the build-vs-buy analysis in case the calculus has shifted |
| Ad hoc | Any vendor-announced model deprecation or major version change triggers a mandatory re-eval before adopting |

## Worked example

A travel booking company, Solmar Travel, signed a two-year contract with an
LLM vendor for its trip-planning assistant feature, negotiated primarily on
price with no version-pinning clause — a gap the procurement team didn't
know to ask about. Eight months in, the vendor pushed a model update to
improve general performance. Solmar's assistant, tuned carefully around the
old model's specific response format, started producing malformed
itineraries in about 4% of requests — invisible until customer complaints
rose sharply.

Because there was no contractual version-pinning right, Solmar's only
options were an emergency prompt-engineering fix (delivered in 3 days, but
imperfect) or a costly urgent renegotiation. The team also discovered,
only when checking, that the contract's deprecation notice period was 15
days — far too short to plan a migration if the vendor ever discontinued
the model tier entirely.

At renewal, the AI manager applied this module's framework directly: added
a contractual right to pin model versions with a 30-day opt-in window for
any new version, extended the deprecation notice requirement to 120 days,
and added a quarterly-eval clause giving Solmar access to run its own test
suite against the vendor's staging environment before any major version
went live in production. The renegotiated contract cost 6% more annually —
a cost the team justified to finance as insurance against a repeat of the
8-month incident, which had cost an estimated $40,000 in engineering
firefighting plus unquantified reputational cost from the complaint spike.

## How It Actually Works

Solmar's malformed-itinerary failure illustrates why "the vendor improved
general performance" and "your specific integration broke" are entirely
compatible outcomes, not a contradiction — because a foundation model
update is optimized and evaluated against the vendor's own broad benchmark
suite, not against any individual customer's specific downstream parsing
logic. Solmar's system had been tuned around the old model's particular
response format (a specific structure the old model happened to produce
reliably), and nothing in the vendor's update process has visibility into,
or responsibility for, preserving that incidental behavior — from the
vendor's perspective, average quality genuinely went up, while from
Solmar's perspective, a downstream parser that depended on an
undocumented, informally-relied-upon output shape broke. This is the
general mechanism behind every "vendor-side model change" failure mode:
you are always depending on more of the model's behavior than what's
formally specified in the API contract, and a version change is free to
alter anything outside that formal contract without breaching it.

Version pinning fixes this mechanically by decoupling two events that would
otherwise be forced to happen simultaneously: the vendor's decision to ship
an improvement, and your system's exposure to that improvement's side
effects. Without pinning, every customer is silently migrated the moment
the vendor flips a switch, so the blast radius of any behavioral change is
every dependent system at once, with zero warning and zero opportunity to
re-validate first. With pinning, the new version exists but doesn't affect
you until you deliberately opt in after testing against your own eval
suite — converting an involuntary, simultaneous exposure into a scheduled,
voluntary migration you control the timing of. That's precisely why
Solmar's renegotiated contract paired pinning with a quarterly-eval clause:
pinning alone only delays the exposure; the eval suite is what lets you
decide, on your own evidence, when the new version is actually safe to
adopt.

## Exercise

Take a real or plausible AI vendor relationship at your organization.

1. **Run the build/buy/partner analysis** in section 1 for this specific
   capability — not for "AI" broadly.
2. **Score the vendor** against the seven criteria in section 2. Identify
   the single lowest-scoring row and what it would take to fix or
   contractually mitigate it.
3. **List the three contract terms from section 3** most relevant to this
   relationship's actual risk profile, and draft one sentence per term
   stating the specific ask you'd bring to the next renewal or negotiation.
