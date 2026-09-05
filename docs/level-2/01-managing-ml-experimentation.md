# 01 · Managing ML Experimentation & Iteration

Most of what an ML team does day to day is not "building the model" — it is
running experiments to find out which model is worth building. As a manager
you will almost never read the code or inspect the training curves yourself.
What you *can* control, and what largely determines whether the team
converges or wanders, is the structure around the experiments: what counts
as a question worth asking, how long a question gets before it must produce
an answer, and what happens to the answer afterwards.

Teams that struggle here rarely lack technical skill. They lack a stopping
rule. A strong data scientist with no time-box will keep improving a model
that was never going to clear the business bar, because each individual
increment feels productive. Your job is to make the *portfolio* of
experiments productive, which sometimes means killing individually
interesting ones.

## 1. What an experiment actually is

An ML experiment is a falsifiable claim plus a pre-committed decision rule.
If you can't say in advance what result would make you abandon the idea, you
don't have an experiment — you have an open-ended activity.

| Weak framing (avoid) | Strong framing (use) |
|---|---|
| "Improve the churn model" | "Adding 90-day support-ticket history as a feature raises recall at fixed precision by ≥3 points" |
| "Try the new embedding model" | "Swapping to the new embedding model improves retrieval hit-rate@5 by ≥5 points on our 400-query eval set" |
| "Explore whether an LLM could help" | "An LLM classifies inbound email into our 12 routing categories at ≥85% agreement with a human labeler on 300 held-out emails" |
| "Reduce hallucinations" | "Adding retrieval grounding cuts unsupported-claim rate from 14% to ≤6% on the 200-item factuality eval" |

Each strong version contains the four things to insist on before approving
the work: **the change being tested**, **the metric**, **the threshold**, and
**the evaluation set it will be measured on**.

## 2. The experiment brief — a one-screen template

Require this before any experiment expected to take more than about two
days. It should take fifteen minutes to fill in; if it takes much longer,
the experiment isn't well-defined yet, which is itself a useful finding.

| Field | Purpose | Example entry |
|---|---|---|
| Hypothesis | The falsifiable claim | "Ticket-history features raise recall ≥3 pts at 40% precision" |
| Why we believe it | Forces a prior; exposes pure guessing | "Support contact precedes 61% of observed churns in the data audit" |
| Metric & threshold | The pre-committed bar | Recall at fixed 40% precision; ≥3 point gain |
| Eval set | Prevents metric shopping after the fact | Frozen Q3 holdout, 12,000 accounts |
| Time-box | The stopping rule | 6 working days |
| Cost | Makes the portfolio visible | ~1.5 person-weeks, ~$400 compute |
| Decision if it fails | Prevents zombie experiments | Drop this feature family; move to pricing-signal features |
| Who reviews the result | Ensures it's actually read | Weekly experiment review; ML lead + PM |

The last two rows are the ones teams skip and the ones that matter most.
"Decision if it fails," written *before* the result is known, is the
cheapest available defence against sunk-cost reasoning.

## 3. Time-boxing without micromanaging

You are not estimating how long the work takes — that is genuinely
unknowable in advance. You are buying a fixed amount of information for a
fixed price. The time-box is the price; the deliverable is *an answer*,
which may well be "no."

| Experiment class | Typical time-box | What "done" means |
|---|---|---|
| Feasibility spike | 3–5 days | We know whether the signal plausibly exists at all |
| Feature or approach test | 1–2 weeks | Metric moved or didn't, on the frozen eval set |
| Architecture or vendor swap | 2–3 weeks | Head-to-head quality numbers plus cost and latency deltas |
| Production-hardening iteration | 1 sprint | Same quality, now inside the latency and cost budget |

When a time-box expires without a clear answer, the reflex "give it another
week" is usually wrong. Ask instead: *what would we have to change to get an
answer inside the next box?* If nobody can name it, the question is badly
posed rather than under-resourced. One extension, once, with a stated
reason, is a healthy norm. Three extensions is a project with no stopping
rule.

## 4. The weekly experiment review

A 45-minute standing meeting run to a fixed agenda does more for
experimentation throughput than any tool purchase. Structure it so negative
results are as easy to present as positive ones — if the meeting implicitly
rewards good news, you will get filtered news.

| Segment | Time | Content |
|---|---|---|
| Closed experiments | 15 min | Each: hypothesis, result, decision taken. Negative results first |
| Open experiments | 10 min | Days left in the box, current signal, blockers |
| Queue re-ranking | 15 min | What's next and why, given what we now know |
| Killed / parked list | 5 min | Explicit, so nobody silently re-runs a dead idea |

A useful manager habit in this meeting: when a result is presented, ask
*"what would have made you conclude the opposite?"* It is a fast,
non-hostile check on whether the evaluation was capable of giving a real
answer.

## 5. Making results durable

The most common waste on ML teams is not failed experiments — it is
*repeated* failed experiments. Six months on, nobody remembers that the
demographic-feature idea was tried and produced nothing, so a new hire tries
it again.

You don't need to mandate a specific tool. You do need to mandate that every
closed experiment leaves behind a retrievable record containing: hypothesis,
data and config version, metric result, and the decision taken. Whether that
lives in an experiment-tracking system, a wiki page, or a structured commit
message matters far less than whether a new team member can find it in under
five minutes.

Ask your ML lead one question: *"If someone proposes an idea we already
tested last quarter, how would we know?"* The quality of the answer tells
you whether your team's experimental history is an asset or lost work.

## 6. Warning signs a manager can spot without reading code

| Signal | What it usually means | What to ask |
|---|---|---|
| Metric improves in small increments every week for months | Overfitting to the eval set through repeated exposure | "When was the holdout last refreshed, and who has seen it?" |
| The evaluation set keeps changing | Post-hoc metric shopping | "Was this eval set chosen before or after we saw the result?" |
| Every experiment "succeeds" | Hypotheses set too safe, or results being framed | "What have we killed this quarter?" |
| Large offline gain, no production movement | Offline/online mismatch — the eval doesn't reflect reality | "What's the gap between our eval set and live traffic?" |
| Nobody can state the current baseline | No reference point; all gains are unverifiable | "What does the simplest possible approach score?" |

The last one is worth enforcing permanently: **every project keeps a live,
stated baseline** — usually a rule-based heuristic or the existing manual
process. Gains get reported against it, never in the abstract.

## Worked example

A five-person ML team at a B2B SaaS company was four months into a churn-
prediction project with nothing shipped. The manager, new to the team, found
eleven experiments in flight simultaneously, none with a written threshold,
and a shared belief that the model was "at about 0.71 AUC" — with nobody
able to say what the existing sales-team heuristic scored.

Three changes over two sprints:

1. **Established a baseline.** The incumbent heuristic — flag any account
   with a support ticket in the last 30 days and no login in 14 — was
   measured properly for the first time and caught 34% of churners. The
   0.71-AUC model, converted to the same operating point, caught 39%. Four
   months of work had produced a five-point gain over a two-rule heuristic.
   Real, but nothing like what stakeholders had been told.
2. **Cut eleven experiments to three**, each with a brief, a threshold, and
   a written kill decision. Two of the eleven turned out to be re-runs of
   work a departed contractor had already done and found negative.
3. **Started a weekly review** that opened with negative results.

The outcome that mattered wasn't a modelling breakthrough. Within three
weeks the team established that no feature family available in their current
data pushed recall past roughly 45%, and that the real constraint was
product-usage telemetry being discarded after 30 days. The project was
re-scoped into a data-engineering effort to retain 12 months of telemetry,
with modelling paused until it existed. That conclusion had been reachable
in week three of the project rather than month five. The missing ingredient
was never technical skill — it was a stopping rule that forced the question
"is the signal here at all?" to be asked out loud.

## How It Actually Works

"Metric improves in small increments every week for months" is a warning
sign for a precise statistical reason: it's the signature of the multiple-
comparisons problem playing out over time. Every time the team evaluates a
new idea against the same frozen holdout set and only keeps the ones that
improve the score, they are running an implicit selection process — and
some fraction of tested ideas will appear to help purely by chance, because
a finite holdout set has sampling noise just like any other measurement.
Keep testing and keeping "winners" against the same fixed set for long
enough, and the model gradually specializes to that specific set's noise
rather than to the underlying real-world pattern, exactly the way a student
who sees the same practice exam repeatedly memorizes its particular
questions rather than the subject. This is why a genuinely frozen,
infrequently-refreshed holdout is not bureaucratic caution but the only
thing standing between "the metric moved" and "the metric moved on data we
already leaked information about" — and it's why the warning-sign question
is specifically "when was the holdout last refreshed," not "is the metric
still improving."

The offline/online mismatch warning sign has an equally mechanical
explanation: an offline eval set is, by construction, a sample from a
distribution frozen at the moment it was collected, while live traffic is
drawn from whatever distribution exists *right now* — user behavior,
seasonal patterns, upstream data pipeline changes, and adversarial
adaptation (users learning to game a fraud model, for instance) all shift
the live distribution continuously in ways the static holdout cannot
capture. A large offline gain with no matching production movement usually
means the experiment improved performance on a feature or pattern that is
well-represented in the frozen holdout but rare or shifted in current live
traffic — which is exactly the gap the "what's the eval-to-live gap"
question is designed to surface before a team spends another quarter
chasing offline numbers that will never move a real business metric.

## Exercise

Take a current or recent ML effort on your team (or a plausible one) and do
three things.

1. **Write down the baseline.** What does the simplest non-ML approach — a
   rule, a heuristic, or today's manual process — actually score on the
   project's primary metric? If nobody knows, that is your finding: record
   who would need to measure it and how long that would take.
2. **Convert one in-flight activity into an experiment brief** using the
   eight-field template in section 2. Pay particular attention to the
   "decision if it fails" row, and write it as though the failure has
   already happened.
3. **Audit for the warning signs** in section 6. Mark each of the five
   signals present / absent / unknown, and for anything marked present,
   write the single question you will ask your ML lead this week.

Keep the brief — Module 10's capstone reuses it as the experimentation-
tracking component of your MLOps process design.
