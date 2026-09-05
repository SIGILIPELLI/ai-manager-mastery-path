# 03 · MLOps Fundamentals for Managers

There is a gap between "the model works" and "the model works every Tuesday
at 3am, on data nobody warned us about, and we find out within an hour when
it stops." MLOps is the name for everything that lives in that gap. It is
where most AI projects that pass their demo quietly die.

You will not be configuring pipelines. But you own the consequences of a
model that silently degrades, and you sign off on the roadmap that either
funds this work or doesn't. The failure mode is predictable: MLOps work is
invisible when it's working, so it loses every roadmap argument to a
visible feature — until the first incident, after which it gets funded in a
panic at three times the price.

This module gives you a maturity model to locate your team on, the four
questions that reveal where you actually are, and the language to defend
the investment *before* the incident rather than after it.

## 1. The seven jobs MLOps covers

"MLOps" is not one thing. When someone says the team needs to "invest in
MLOps," ask which of these seven they mean — the answers have very
different costs.

| Job | The question it answers | Who feels it when it's missing |
|---|---|---|
| **Data pipelines** | Does the model get fresh, correct data on a schedule? | Everyone, eventually |
| **Reproducibility** | Can we rebuild the exact model that's in production today? | Auditors, and anyone debugging |
| **Versioning** | Which model, data, and code combination is live right now? | Incident responders |
| **Deployment** | How does a new model reach users, and how fast can it be undone? | Product, during a bad release |
| **Monitoring** | Would we notice if quality dropped? How quickly? | Customers, first |
| **Retraining** | What triggers a refresh, and who approves it? | Finance, via slow decay |
| **Governance & audit** | Can we show who approved what, and why? | Legal and compliance |

A useful manager reflex: when the team asks for MLOps investment, make them
name the job and the failure it prevents. "We need a feature store" is a
solution. "We can't reproduce the model that made a disputed decision in
March" is a problem — and it is the version that gets funded.

## 2. The MLOps maturity model

Locate your team honestly. Most organisations that describe themselves as
level 3 are level 1 with a CI pipeline.

| Level | Name | What it looks like | Deploy frequency | Time to detect a quality drop |
|---|---|---|---|---|
| **0** | Manual | Notebooks; a data scientist emails a model file; deployment is a ticket | Ad hoc, months | Never — a customer tells you |
| **1** | Repeatable | Training is a script anyone can run; models are stored somewhere known; deployment is documented but manual | Quarterly | Weeks, via business metrics |
| **2** | Automated pipeline | Training runs as a pipeline; models and data are versioned; deployment is scripted and reversible | Monthly | Days, via input-data monitoring |
| **3** | Monitored & tested | Automated eval gates before release; live quality monitoring; drift alerts; documented rollback | Weekly | Hours, automatically |
| **4** | Continuously improving | Retraining triggered by monitored conditions; shadow and canary deploys standard; full lineage for audit | On demand | Minutes, with automatic mitigation |

Two things to internalise. First, **higher is not always better** — a model
that informs a quarterly pricing review does not need level 4, and pushing
it there is waste. Second, **the levels are mostly about detection speed,
not deployment speed.** The right target is set by how much damage a bad
model does per hour it goes unnoticed.

| If a bad model running for one week would... | Target level |
|---|---|
| Mildly annoy an internal team | 1 |
| Cost tens of thousands, or embarrass you publicly | 2–3 |
| Trigger regulatory exposure or customer harm | 3–4 |

## 3. What actually breaks in production

Software fails loudly — a service returns an error and a pager goes off. ML
fails quietly: the system stays up and the answers get worse. These are the
four decay modes, and none of them produces an error message.

| Failure mode | Plain description | Typical trigger | What catches it |
|---|---|---|---|
| **Data drift** | Inputs no longer look like training data | New market, new segment, seasonality | Input distribution monitoring |
| **Concept drift** | The relationship between inputs and outcome changed | Competitor move, policy change, external shock | Outcome monitoring against fresh labels |
| **Pipeline break** | An upstream schema or source changed silently | Another team's "harmless" refactor | Data contract validation |
| **Training/serving skew** | Production computes a feature differently than training did | Two codebases, one feature definition | Comparing live and training feature values |

Training/serving skew is the one managers never hear about and the one that
most often explains "great offline results, no production lift." If a
project shows a large offline gain that fails to appear live, this is the
first thing to ask about — before anyone re-tunes the model.

## 4. The four questions that locate your team

Ask these in a review. You do not need to understand the implementation
behind the answers; you need to notice when there isn't one.

1. **"If the model started making bad predictions this morning, when would
   we know, and how?"** A confident answer naming a specific alert is level
   2+. "We'd probably hear from the business" is level 0–1.
2. **"How do we roll back to the previous model, and when did we last
   actually do it?"** A rollback that has never been rehearsed is a
   hypothesis, not a capability.
3. **"Which exact model is serving traffic right now, and what data was it
   trained on?"** If this takes more than a few minutes to answer, you have
   no audit story.
4. **"What triggers a retrain — a calendar, a metric, or someone's
   memory?"** "Someone's memory" is the most common answer and the least
   durable one.

## 5. The monitoring dashboard you should own

You do not need the ML team's technical dashboard. You need a small, stable
set of numbers that tells you whether the system is healthy, readable in
ninety seconds.

| Panel | Metric | Healthy looks like | Escalate when |
|---|---|---|---|
| Volume | Predictions served per day | Flat, or tracking business volume | Sudden step change either way |
| Input health | % of records failing validation | Under 1% | Sustained rise, or a new failure type |
| Output shape | Share of predictions per class or score band | Stable week over week | Shifts sharply with no product change |
| Quality | Primary model metric on recent labelled data | Within tolerance of release value | Drops below the pre-agreed floor |
| Business link | The product metric from Module 02 | Trending as forecast | Diverges from the model metric |
| Operations | p95 latency, error rate, monthly inference cost | Within budget | Cost per prediction rises without volume |

The fifth row keeps the rest honest. Model metrics that look fine while the
product metric sags mean the evaluation no longer reflects reality — that
is a finding, not a paradox.

## 6. Release safety, in manager terms

Three mechanisms, in increasing order of caution. You should know which one
a given release is using, and say so out loud before it ships.

| Mechanism | What happens | When to require it |
|---|---|---|
| **Shadow deploy** | New model runs on live traffic; outputs are logged, not used | First release of any consequential model |
| **Canary / staged rollout** | New model serves a small traffic share, watched against the old one | Any model touching customers |
| **Full rollout with rollback** | Everyone gets it; a tested revert path exists | Low-stakes internal models |

The one non-negotiable is **a rollback that has been rehearsed at least
once**. Ask for the date it was last exercised. If the answer is "we've
never had to," schedule a drill — an untested rollback path is a belief,
and beliefs fail at 2am.

## Worked example

A retail company ran a demand-forecasting model that fed automatic
replenishment across 140 stores. The model was built by a contractor,
deployed once, and left alone for eleven months. Maturity level: 1. There
was a dashboard, but it showed prediction volume and service uptime — both
of which stayed green throughout what follows.

In March the merchandising team changed promotional cadence from monthly to
weekly. Nothing about the model broke. Its inputs kept arriving; its
outputs kept flowing. But the relationship it had learned between past
sales and future demand no longer held — textbook concept drift.

Forecast error, measured afterwards, drifted from **12% MAPE to 21% over
nine weeks**. Finance estimated that on the roughly **$4.2M of monthly
inventory flow** the model steered, each point of MAPE cost about
**$18,000 a month** in carrying cost and lost sales combined. Nine extra
points is **$162,000 per month**, and the problem ran for roughly two
months before a regional manager complained loudly enough to trigger an
investigation — about **$324,000** in total.

The diagnosis took three days. The fix took an afternoon: retrain on recent
data. The entire cost sat in the detection gap.

What the manager did next mattered more than the fix. Rather than asking
for "better MLOps," she scoped the smallest jump from level 1 to level 2–3
for this one system:

| Investment | One-off | Annual |
|---|---|---|
| Weekly automated retrain pipeline | $45,000 | — |
| Forecast-error monitoring with alert thresholds | $30,000 | — |
| Input validation on the promotions feed | $20,000 | — |
| Ongoing platform and on-call cost | — | $30,000 |
| **Total** | **$95,000** | **$30,000** |

The proposal to the CFO was one sentence: *ninety-five thousand dollars,
once, to cut the detection window on a failure that has already cost us
three hundred and twenty-four thousand, from nine weeks to under one.* It
was approved in that meeting. The identical request, made a year earlier as
"we need to invest in MLOps maturity," had been deferred twice.

The transferable lesson is not about forecasting. It is that MLOps
investment is fundable when expressed as **detection-window reduction
against a quantified failure**, and rarely fundable when expressed as
platform maturity.

## How It Actually Works

Training/serving skew is worth understanding at the mechanism level because
it explains why "great offline results, no production lift" is so common
and so hard to catch by staring at the model itself. A feature like
"days since last purchase" sounds like one well-defined quantity, but it is
usually computed by two entirely separate code paths: an offline batch job
that built the training set, and a real-time service that computes it at
inference time. If the batch job uses calendar days and the real-time
service uses a rolling 24-hour window, or if one includes same-day
purchases and the other doesn't, the model was trained on one distribution
of that feature and is being fed a subtly different distribution in
production — and because both versions are plausible-looking numbers, this
mismatch produces no error, no crash, no validation failure. It just quietly
degrades every prediction that depends on the skewed feature, which is
exactly why comparing live feature values against training feature values
statistically (not just checking that a value exists) is the only reliable
way to catch it.

The maturity model's core claim — that levels are mostly about detection
speed, not deployment speed — follows from a basic property of how ML
failures compound: unlike a crashed service, a degraded model keeps
producing usable-looking output the entire time it's wrong, so the cost of
a failure scales with the *duration it goes unnoticed*, not with the size
of the underlying bug. The demand-forecasting example makes this concrete:
the actual technical fix (retrain on recent data) took an afternoon and
would have been equally cheap in week one or week nine — the $324,000 was
entirely a function of the nine-week detection gap, not of the concept
drift itself. This is why investment framed as "cut the detection window
from nine weeks to under one" is a mechanically sound way to price MLOps:
it is quantifying exactly the variable (time-to-detect) that multiplies
directly into the cost of every future silent failure, regardless of what
specific failure eventually occurs.

## Exercise

Pick one AI or ML system your organisation runs in production — or the one
you are closest to shipping.

1. **Place it on the maturity model** in section 2, then separately write
   the level it *should* be at using the damage-per-week table. If those
   differ, you have found your gap and its justification in one step.
2. **Ask the four questions** in section 4 of whoever runs the system.
   Record the answers verbatim, including the vague ones — the vagueness is
   the data.
3. **Estimate the detection window.** If the model degraded today, how many
   days until someone noticed? Multiply by your best estimate of daily cost
   or harm. That number is your MLOps business case.
4. **Check the rollback.** Find out when it was last actually exercised. If
   the answer is "never," propose a drill date this quarter.
5. **Sketch the six-panel dashboard** from section 5 for this system,
   naming the specific metric that goes in each row. Anywhere you cannot
   name a metric, you have found a blind spot.

Keep this maturity assessment — Module 10's capstone builds a full MLOps
process design on top of it.
