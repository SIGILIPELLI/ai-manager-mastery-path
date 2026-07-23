# 03 · Understanding AI Project Lifecycles

An AI project's lifecycle looks nothing like a typical feature build's linear
"design → build → ship" flow. It loops, it can dead-end at multiple points
for legitimate reasons, and the amount of time spent in each phase is much
harder to predict up front. This module gives you a management-level map of
the full lifecycle — from a raw idea to a monitored production system — and
the specific decision gates you, as the manager, are responsible for at each
stage.

## 1. The AI project lifecycle, stage by stage

| Stage | Purpose | Typical duration | Manager's key decision |
|---|---|---|---|
| **1. Problem framing** | Turn a business ask into a specific, measurable ML/AI problem | Days to 2 weeks | Is this even a good fit for AI, or is a simpler rule-based solution sufficient? |
| **2. Data discovery** | Figure out what data exists, where it lives, and whether it's usable | 1–4 weeks | Do we have enough data, or does this become a "collect data first" project? |
| **3. Feasibility / proof of concept** | A quick, throwaway-quality experiment to test if the approach can work at all | 2–6 weeks | Go/no-go: does the early signal justify further investment? |
| **4. Model development** | Iterative building, training, and evaluation of candidate models | Weeks to months | Have we hit the pre-agreed quality bar, or do we need another iteration (or to reset scope)? |
| **5. Integration & productionization** | Wrapping the model in real infrastructure: APIs, monitoring, fallback logic | Weeks to months (often underestimated) | Is this ready for real users, or does it need a staged/limited rollout first? |
| **6. Launch** | Releasing to real users, often gradually | Days to weeks | What's the rollback plan if something goes wrong? |
| **7. Monitoring & iteration** | Ongoing tracking of live performance, retraining as needed | Indefinite — this never "finishes" | Is the model still meeting the bar, or has drift eroded it? |

The critical mental shift for a new AI manager: stages 3 and 4 are *expected*
to sometimes fail or reset. A proof of concept that shows the approach
doesn't work is not a failed project — it is the project doing its job of
preventing a much more expensive stage-5 failure. Budget explicit "kill
criteria" at the end of stages 1–3 rather than treating every project as
guaranteed to reach launch.

## 2. Where AI lifecycles diverge from standard software delivery

| Standard software delivery | AI/ML project delivery |
|---|---|
| Requirements are mostly knowable up front | Requirements include "is this even achievable," which is answered *during* the project |
| A sprint's "done" criteria is binary (feature works or doesn't) | "Done" is a quality threshold agreed before work starts (e.g., 90% precision) |
| QA happens once, near the end | Evaluation happens continuously, at every iteration |
| Ship and move on | Ship, then monitor indefinitely — the model is never "finished" |
| Bugs are fixed by changing code | Quality issues are often fixed by changing *data*, not code |

## 3. The stage-gate decision framework

A practical tool for running this lifecycle: define, in writing, the
criteria that must be true to move from one stage to the next, before the
stage begins. This turns "the model isn't good enough yet, should we keep
going?" from a political argument into a pre-agreed checklist.

| Gate | Sample criteria to move forward |
|---|---|
| Problem framing → Data discovery | A single, specific success metric is written down and agreed with the business sponsor |
| Data discovery → Feasibility | Data of sufficient volume and quality exists, or a plan (and budget) to collect it is approved |
| Feasibility → Development | The proof of concept beats an agreed baseline (see Module 2) by a meaningful margin |
| Development → Integration | The model meets the pre-agreed quality bar on a held-out test set that reflects real production conditions |
| Integration → Launch | Monitoring, rollback, and a fallback (non-AI) path are all built and tested |
| Launch → steady state | A first monitoring window (e.g., 2 weeks) shows no unexpected degradation or safety issues |

## Worked example

A logistics company wants to predict delivery delays. The AI manager sets the
success metric at "problem framing": predict delays of 2+ hours with at
least 75% precision, evaluated on the next quarter's real shipments. During
"data discovery," the team finds that delay-cause data is inconsistently
logged across regions — the gate isn't met, so the project pivots to a
2-week data-cleanup effort before feasibility work even starts, rather than
building a model on unreliable labels. The proof of concept then hits 71%
precision — just under the bar. Rather than quietly lowering the bar to call
it a win, the manager convenes the team: is 71% close enough that another
2-week iteration likely closes the gap, or is a different feature set needed?
They choose one more iteration, hit 78%, and only then move into
integration. The stage gates made three real decisions visible and
deliberate instead of implicit.

## Exercise

Pick a real or plausible AI project. Write out all seven lifecycle stages
from the first table, and for each one write: (1) a realistic time estimate
given your organization's actual constraints, and (2) one specific, written
gate criterion that must be true before moving to the next stage. Then
identify which single gate is most likely to be skipped or rushed under
deadline pressure at your organization, and write one sentence on how you'd
defend keeping it.
