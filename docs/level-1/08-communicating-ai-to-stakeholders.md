# 08 · Communicating AI Concepts to Non-Technical Stakeholders

An AI manager spends a large share of their time translating — turning
"we improved the F1 score from 0.72 to 0.81 by adding a gradient-boosted
ensemble" into something an executive, a sales leader, or a customer support
director can actually act on. Getting this translation wrong in either
direction is costly: oversimplify and stakeholders make decisions on false
confidence; stay too technical and they tune out or, worse, approve
something they didn't actually understand. This module gives you concrete
patterns for translating in both directions.

## 1. The translation table: technical concept → business language

Keep a version of this table on hand for status updates — translating on
the fly in a live meeting is where technical jargon most often leaks
through unintentionally.

| Technical concept | Business translation |
|---|---|
| "Model accuracy is 87%" | "Out of 100 typical cases, the system gets about 87 right — we'll walk through what the other 13 look like and how we handle them" |
| "We're seeing model drift" | "The system's real-world performance has started slipping as customer behavior has shifted since we trained it — we're refreshing it" |
| "The model hallucinates sometimes" | "The system can occasionally state something confidently that isn't true — here's exactly where we've built in a human check for that" |
| "We need more labeled data" | "We need more examples of correct answers to teach the system from — here's the specific gap and what it'd take to close it" |
| "Precision vs. recall tradeoff" | "We can tune this to catch more real cases (at the cost of more false alarms) or fewer false alarms (at the cost of missing more real cases) — here's the mix we'd recommend and why" |

## 2. The "confidence, not certainty" framing

The single most important habit: never let a stakeholder walk away believing
an AI system is more reliable than it actually is. State performance as a
rate with real-world consequence, not a bare percentage.

| Weak framing | Strong framing |
|---|---|
| "The model is 90% accurate" | "Out of every 10 cases, we expect about 9 to be handled correctly and roughly 1 to need a human to step in — here's what that looks like operationally" |
| "It works well" | "It performs at [X] on our test set, which is [above/below/at] the bar we agreed we needed before launch" |
| "We fixed the bias issue" | "We reduced the performance gap between groups from X to Y; we haven't eliminated it, and here's our ongoing monitoring plan for it" |

## 3. A status-update template for AI projects

Use a consistent structure so stakeholders learn what to expect and where
to find the information they care about, meeting after meeting.

| Section | Content |
|---|---|
| **Where we are** | One sentence: which lifecycle stage (see Module 3), plain language |
| **What we learned since last update** | 1–2 concrete findings, translated using the table in section 1 |
| **What's still uncertain** | Named explicitly — don't let a stakeholder assume something is settled when it isn't |
| **What we need from you** | A specific decision or input, if any — vague updates with no ask train stakeholders to tune out |
| **Next checkpoint** | Date and what will be known by then (ties back to Module 6's range-and-checkpoint framework) |

## Worked example

An AI manager updates a company's executive team on a customer-churn
prediction project. Instead of "our AUC is 0.83, up from 0.79 last sprint,"
the update reads: "The model correctly flags about 8 in 10 customers who are
actually about to churn, and about 2 in 10 flags turn out to be false
alarms — that's an improvement from last month, and it's now within the
range where the retention team said acting on flags is worth their time.
What's still uncertain: performance for customers who joined in the last 90
days, where we have less historical data — we're treating that as a known
gap, not silently ignoring it. What we need from you: sign-off to start a
limited pilot with the retention team next week, targeting the top 500
flagged accounts." The executive team approves the pilot immediately,
because the update gave them exactly the information needed to make that
call — no jargon to decode, no hidden uncertainty, and one clear ask.

## How It Actually Works

The reason "8 in 10 flagged, 2 in 10 false alarms" lands where "AUC 0.83"
doesn't is that AUC (area under the ROC curve) is a summary statistic
averaged across *every possible decision threshold* a model could use, not
a description of how the model will actually behave once your team picks
one operating point and starts acting on its flags. AUC answers "how well
does this model rank positive cases above negative ones, in general" — a
question that matters to the data scientist choosing between candidate
models, but not to an executive who needs to know what will happen at the
specific precision/recall tradeoff (the specific threshold) the team plans
to deploy. Translating AUC into "8 of 10 flagged customers really are
churning" requires picking that operating threshold first and reporting the
confusion-matrix numbers it produces — which is exactly why the strong
framings in section 2 are all threshold-specific numbers, not the
aggregate metrics that appear in a data scientist's own notebook.

This also explains why naming what's "still uncertain" prevents a specific,
recurring failure: a metric computed on an overall test set silently
averages over subgroups (new customers, edge cases, rare categories) whose
individual performance can be much worse than the headline number suggests,
for the same statistical reason a rare class can hide inside an aggregate
accuracy figure (see Module 2). If the manager doesn't explicitly flag "we
have less historical data on 90-day-old customers, so performance there is
genuinely unknown," the executive has no way to distinguish "this number is
solid everywhere" from "this number is solid on average but untested where
it matters most" — the two situations look identical in a single reported
percentage, and only naming the gap out loud closes it.

## Exercise

Take a real or plausible technical status update from an AI project (write
2–3 genuinely technical sentences full of jargon — accuracy metrics, model
architecture, data issues). Rewrite it using the status-update template in
section 3, applying the translation table from section 1 and the
"confidence, not certainty" framing from section 2. Have a non-technical
colleague (or imagine one) read both versions and note which specific
sentences would have confused them in the original.
