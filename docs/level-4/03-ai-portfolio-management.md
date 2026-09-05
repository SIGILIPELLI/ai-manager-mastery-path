# 03 · AI Portfolio Management

Once an organization runs more than a handful of AI initiatives, the
executive question shifts from "is this project good" to "is this the
right allocation of a fixed budget across all our AI bets." That's a
portfolio management problem, not a project management problem, and it
requires different tools: expected value under uncertainty, risk-adjusted
comparison across projects with very different risk profiles, and explicit
rules for when to kill a funded project to reallocate its budget. This
module gives you that toolkit.

## 1. Risk-adjusted value — the core comparison tool

Comparing AI projects by raw projected value alone is misleading because
AI initiatives carry wildly different probabilities of actually delivering
that value. A $4M-upside project with a 30% chance of working is not
better than a $1.7M-upside project with a 90% chance.

**Risk-adjusted value = projected value × probability of success**, where
probability of success is an honest, calibrated estimate (informed by
similar past projects, technical feasibility assessment, and — critically —
resisting the temptation to inflate it to justify a pet project).

| Project | Projected annual value | Estimated success probability | Risk-adjusted value |
|---|---|---|---|
| A: Support deflection (LLM) | $1.7M | 90% (proven technique, similar to Level 3 Module 7's worked example) | $1.53M |
| B: Personalization engine | $4.2M | 50% (high upside, unproven at this company's data scale) | $2.10M |
| C: Fraud detection upgrade | $2.1M | 80% (incremental improvement to existing system) | $1.68M |
| D: Generative design tool | $3.0M | 30% (novel application, no internal precedent) | $0.90M |

Ranked by risk-adjusted value: B ($2.10M) > C ($1.68M) > A ($1.53M) > D
($0.90M) — a different order than ranking by raw projected value (B > D >
C > A), and the ordering that should actually drive funding priority.
Project D might still be worth a small exploratory investment (Horizon 3,
per Module 1) precisely because it's unproven, but it should not receive
Horizon-2-scale funding on the strength of its raw upside number alone.

## 2. Portfolio allocation by horizon

Apply the three-horizon framework from Module 1 at the portfolio level, with
actual dollar allocation, not just proportional description.

For a $12M annual AI portfolio budget at a 65/25/10 Horizon 1/2/3 split:

| Horizon | Allocation | Dollar amount |
|---|---|---|
| Horizon 1 (efficiency, 0-12mo) | 65% | $7,800,000 |
| Horizon 2 (new capability, 1-3yr) | 25% | $3,000,000 |
| Horizon 3 (exploratory, 3yr+) | 10% | $1,200,000 |

Within each horizon, rank candidate projects by risk-adjusted value and fund
top-down until the horizon's budget is exhausted — don't let a
Horizon-3-appropriate exploratory bet compete directly against a
Horizon-1 efficiency project on raw value; they serve different portfolio
purposes and should be funded from separate pools.

## 3. Portfolio rebalancing triggers

A portfolio reviewed once a year and otherwise left alone will accumulate
zombie projects — funded, underperforming, and never explicitly killed
because no single trigger forced the conversation. Define triggers in
advance:

| Trigger | Action |
|---|---|
| Quarterly ROI tracking (Level 3 Module 7) shows realized value <50% of projection at the midpoint checkpoint | Formal review: fix, re-scope, or kill — no silent continuation |
| A Horizon 3 bet clears its feasibility gate | Promote to Horizon 2 funding tier with a real budget, not incremental scraps |
| A new competitive or regulatory event changes a project's risk/value estimate materially | Re-run the risk-adjusted value calculation immediately, don't wait for the next scheduled review |
| Two projects are found to be solving overlapping problems | Consolidate or kill one — a portfolio problem the Level 3 Module 5 platform review often surfaces |

## 4. Common portfolio management failures

- **Sunk-cost protection of the CEO's or a senior exec's pet project.**
  The risk-adjusted value framework only works if it's applied evenly —
  the moment one project is exempted from honest scoring because of who
  sponsors it, the entire portfolio process loses credibility with everyone
  who has to submit to it.
- **No kill criteria set at funding time.** Just as Level 2's experiment
  brief requires "decision if it fails" before the result is known,
  portfolio-level projects need a pre-committed re-evaluation checkpoint
  and threshold before funding, not an ad hoc conversation once someone
  notices it's underperforming.
- **Treating portfolio review as a once-a-year budget exercise.** AI
  project risk profiles change faster than annual planning cycles — the
  triggers in section 3 should operate continuously, with the annual
  review as a backstop, not the only checkpoint.

## Worked example

A regional airline, Cordova Air, ran a $9M annual AI portfolio across six
projects, including a long-running "AI-powered dynamic crew scheduling"
initiative that had consumed $2.1M over 18 months with no production
deployment — championed personally by the COO, which had made it
politically difficult to question.

The new CAIO introduced quarterly risk-adjusted value scoring across all
six projects, including the crew-scheduling initiative, using the same
rubric for every project regardless of sponsor. The scheduling project's
honestly-assessed success probability, given two failed pilot attempts and
a technical lead who had quietly begun describing the core optimization
problem as "harder than we scoped," was 20% against a projected value of
$3.5M — a risk-adjusted value of $700,000, the lowest in the portfolio,
against $2.1M already spent and a requested $900,000 for another year.

Presenting this required naming the sunk-cost dynamic explicitly to the
COO in a one-on-one before the portfolio review, rather than surfacing it
cold in front of peers. The COO, shown the same framework applied evenly
to every project (including two of the CAIO's own initiatives that also
scored lower than expected), agreed to reduce the scheduling project to a
small $150,000 Horizon 3 research effort with a hard 6-month feasibility
checkpoint, and reallocated the freed $750,000 to the fraud-detection
project, which had the portfolio's highest risk-adjusted value and had
been under-funded relative to its potential all along.

## How It Actually Works

Risk-adjusted value works as a ranking tool because it's computing an
expected value across a probability distribution over outcomes, not a
single deterministic projection — and expected value is the only quantity
that's additive and comparable across projects with genuinely different
risk profiles. A raw $4.2M projection for the personalization engine and a
raw $1.7M projection for support deflection aren't actually the same kind
of number: one is "the value if this unproven approach works," the other is
"the value from a technique already proven at similar scale," and
comparing them directly implicitly assumes both will succeed with equal
likelihood, which is false by construction. Multiplying by success
probability converts both projects onto a common footing — the value you'd
expect to realize *on average* if you ran this exact portfolio decision
many times — which is exactly the quantity that should drive capital
allocation under uncertainty, the same logic that underlies expected-value
reasoning in any domain involving probabilistic bets.

Cordova's sunk-cost dynamic reveals why "decision if it fails" has to be
set before funding, not during review: $2.1M already spent is a cost that
no future decision can recover regardless of what happens next, so it
should have zero bearing on whether continuing to fund the project is a
good use of the *next* dollar — the only economically relevant question is
whether $900,000 spent starting today, at a freshly and honestly assessed
20% success probability, is a better use of that money than reallocating it
to fraud detection. The psychological pull to keep funding a project after
heavy investment is powerful precisely because it feels like abandoning the
sunk cost is "wasting" it, but the $2.1M is equally gone whether the
project is killed today or in another year — the only question left with
any actual leverage is what the next dollar buys, which is exactly the
reframing that let the COO agree once it was made explicit rather than
implicit.

## Exercise

Take your own AI portfolio (or Cordova Air's six-project portfolio, above,
pre-rebalance).

1. **Score 3-5 real or plausible projects** using the risk-adjusted value
   formula in section 1. Be honest about probability — if you can't
   justify the number to a skeptical peer, it's not calibrated yet.
2. **Allocate a hypothetical budget** across the three horizons per section
   2, and rank projects within each horizon by risk-adjusted value.
3. **Write the kill/re-scope trigger** for your lowest-scoring funded
   project, using the pre-committed-threshold discipline from section 4 —
   state the specific number and date at which you'd force a decision.
