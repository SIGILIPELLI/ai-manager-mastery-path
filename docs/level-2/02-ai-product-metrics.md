# 02 · AI Product Metrics

An AI project can be a technical success and a business failure at the same
time, and the usual reason is that nobody built the bridge between the two
scoreboards. The ML team optimises a model metric. The business cares about
a business metric. If no one has written down how one converts into the
other, the team will happily improve a number that doesn't move the outcome
you were funded to move.

This module is about that conversion. You don't need to compute these
metrics yourself. You need to be able to look at a reported number and ask
the two questions that expose most metric problems: *"compared to what?"*
and *"what does that cost us in dollars?"*

## 1. The three layers of AI metrics

| Layer | Example metrics | Who watches it | Update frequency |
|---|---|---|---|
| **Model metrics** | Precision, recall, AUC, hit-rate@k, agreement with human labels | ML team | Every experiment |
| **Product metrics** | Suggestion-acceptance rate, override rate, time-to-resolution, task completion | Product + AI manager | Weekly |
| **Business metrics** | Revenue retained, cost avoided, fraud losses, headcount hours saved | Sponsor, finance | Monthly / quarterly |

Most dysfunction lives in the gap between layers one and two. A model can
get better while the product gets worse — for example, a recommendation
model with higher offline accuracy that surfaces less diverse results and
reduces overall engagement. Insist that every project names at least one
metric per layer, and states explicitly how a movement in the top layer is
expected to propagate down.

## 2. The model metrics a manager must actually understand

You need working intuition for four, and only four, ideas.

| Concept | Plain-language meaning | The question it answers |
|---|---|---|
| **Precision** | Of the things the model flagged, what share were right? | "How much will we annoy people with false alarms?" |
| **Recall** | Of the things that were actually there, what share did we catch? | "How much are we still missing?" |
| **Threshold** | The confidence cut-off for taking action | "Where do we set the dial between the two above?" |
| **Baseline** | What the dumbest reasonable approach scores | "Is this model earning its keep at all?" |

Precision and recall trade off against each other. There is no setting that
maximises both, and the right balance is a **business decision, not a
technical one** — it depends entirely on whether a miss or a false alarm
costs you more. That decision belongs to you, not to the ML team, and it is
routinely abdicated by managers who treat the threshold as an implementation
detail.

### The accuracy trap

Accuracy — the share of all predictions that were correct — is the metric
executives ask for and the one that misleads most often on rare events. If
0.5% of transactions are fraudulent, a model that simply says "never fraud"
is 99.5% accurate and completely worthless. Whenever someone reports
accuracy on a rare-event problem, the follow-up is: *"what would accuracy be
if we always predicted the majority class?"*

## 3. Translating model metrics into money

The bridge is a cost table. Assign a dollar value to each of the four
outcomes of a binary decision, then multiply by expected volumes. This is
arithmetic, not modelling, and you can do it on a napkin.

| Outcome | What it is | Cost driver to estimate |
|---|---|---|
| True positive | Correctly flagged | Value captured (loss avoided, revenue gained) |
| False positive | Wrongly flagged | Review time, customer friction, churn risk |
| False negative | Missed | The full loss the system was meant to prevent |
| True negative | Correctly ignored | Usually zero |

Two rules make this useful. First, get the **ratio** between false-positive
and false-negative cost roughly right — precision on the absolute values
matters far less. Second, always price the **do-nothing baseline** too, so
the model is evaluated against reality rather than against zero.

## 4. Leading vs. lagging indicators

Business metrics are lagging: churn reduction shows up two quarters later,
which is far too slow to steer by. You need leading indicators that move in
days and are plausibly causally upstream.

| Business metric (lagging) | Leading product indicator | Why it's a reasonable proxy |
|---|---|---|
| Quarterly churn rate | Share of at-risk accounts contacted within 48h of flagging | The intervention is the mechanism; if it isn't happening, nothing downstream can work |
| Annual fraud losses | Weekly caught-fraud value and false-positive review queue length | Direct components of the annual number |
| Support cost per ticket | Draft-acceptance rate and average edit distance | Measures whether agents actually use the assist |
| Sales conversion | Lead-score calibration drift | Predicts when the model stops being trustworthy |

Publish the leading indicators weekly and the lagging ones quarterly. Never
let the weekly report contain only model metrics — that is how a project
runs for six months on green dashboards and then fails its business review.

## 5. Metric anti-patterns

| Anti-pattern | What it looks like | Fix |
|---|---|---|
| Metric with no denominator | "We caught 800 fraud cases!" | Always report out of how many, and versus what baseline |
| Single-number reporting | Only F1, or only accuracy | Report the precision/recall pair at the chosen operating point |
| Moving the goalposts | Threshold quietly retuned before the review | Freeze the operating point between reviews; log any change |
| Optimising a proxy to death | Click-through up, satisfaction down | Pair every optimisation metric with a guardrail metric |
| Model metrics only in exec updates | AUC in a board deck | Translate to dollars or hours before it leaves the team |

The guardrail-metric habit is the highest-value one here: for every metric
you ask the team to maximise, name one metric that must *not* degrade. It
costs nothing and prevents the most common category of AI product harm.

## Worked example

A payments company runs about **200,000 transactions per month**, of which
**0.5% (1,000) are fraudulent**. The ML team presents two candidate
operating points for the same model and recommends B, because "it's more
accurate and has a much better F1 score."

| | Model A (high recall) | Model B (high precision) |
|---|---|---|
| Recall | 80% | 55% |
| Precision | 20% | 50% |
| Fraud caught | 800 | 550 |
| Fraud missed | 200 | 450 |
| Legitimate transactions wrongly flagged | 3,200 | 550 |
| Total flagged for review | 4,000 | 1,100 |
| Accuracy | 98.3% | 99.5% |
| F1 score | 0.32 | 0.52 |

Model B does look better on every headline number. Note first that B's
99.5% accuracy is *exactly the accuracy of a model that never flags
anything* — a clean illustration of why accuracy is meaningless here.

Now the manager applies the cost table. Finance puts the average loss on a
missed fraud at **$180**, and the fully-loaded cost of a false positive —
manual review time plus customer friction — at **$12**.

| | Model A | Model B | Do nothing |
|---|---|---|---|
| Cost of missed fraud | 200 × $180 = $36,000 | 450 × $180 = $81,000 | 1,000 × $180 = $180,000 |
| Cost of false positives | 3,200 × $12 = $38,400 | 550 × $12 = $6,600 | $0 |
| **Total monthly cost** | **$74,400** | **$87,600** | **$180,000** |

Model A is **$13,200 per month cheaper** than Model B — about $158,000 a
year — despite scoring worse on accuracy and F1. Both beat doing nothing
(A saves $105,600/month, B saves $92,400/month), which is the comparison the
sponsor actually cares about.

The manager also asks the sensitivity question: *how wrong would the $12
estimate have to be to flip this?* Holding everything else fixed, the two
options break even when a false positive costs about **$17**. So the
recommendation is robust to moderate error in the estimate, but if the
review queue is understaffed enough that friction costs rise above ~$17 per
false positive, the answer changes — which converts a vague worry into a
specific, monitorable trigger: **queue cost per review**.

The decision made was Model A, with a guardrail metric of review-queue
latency and a standing agreement to revisit the threshold if per-review cost
exceeds $15.

## Exercise

Take an AI system in your organisation, or a plausible one, and build its
metric bridge.

1. **Name one metric per layer** using section 1's table: a model metric, a
   product metric, and a business metric. Write one sentence stating how a
   movement in the model metric is *supposed* to reach the business metric.
2. **Build the cost table.** Estimate the dollar (or hour) cost of a false
   positive and a false negative in your context. Don't stall on precision —
   an order-of-magnitude estimate with your reasoning written down beats no
   estimate.
3. **Compute the do-nothing baseline** at your real monthly volume, and then
   the cost at two different operating points. If you can't get real numbers
   from the team, use plausible ones; the goal is the habit, not the figure.
4. **Find the break-even.** At what false-positive cost do your two options
   swap places? Write that number down as a monitoring trigger.
5. **Name one guardrail metric** that must not degrade while the primary
   metric improves.

Bring the result to your ML lead and ask whether the current threshold was
ever chosen with this arithmetic in mind. In most organisations, it wasn't.
