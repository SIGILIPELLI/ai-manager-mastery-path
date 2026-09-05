# 06 · Managing AI Incidents & Model Failures

AI systems fail differently from traditional software, and your incident
process needs to account for that or it will misclassify severity, route to
the wrong owner, and produce a postmortem that doesn't prevent recurrence.
A traditional outage is binary: the service is up or down. An AI incident
is often a *quality* degradation — the system is running, answering
requests, and quietly getting worse — which means your monitoring has to be
built to catch something that never trips a conventional uptime alert. This
module gives you a severity taxonomy and a runbook specific to AI/ML
failures.

## 1. AI-specific failure modes

Before you can triage, you need a vocabulary broader than "it's down."

| Failure mode | What it looks like | Typical detection lag if unmonitored |
|---|---|---|
| Data/concept drift | Model accuracy degrades gradually as real-world patterns shift away from training data | Weeks to months |
| Silent input schema change | An upstream data source changes format; model runs but consumes garbage | Days to weeks |
| Feedback loop degradation | Model's own outputs pollute the data it's later trained or evaluated on | Months |
| Hallucination / factual error (LLM) | Confidently wrong output, no error thrown | Immediate to never, depending on whether anyone checks |
| Bias/fairness regression | Disparate outcome across a protected group emerges post-launch | Months, often only found by external audit |
| Prompt injection / jailbreak (LLM) | Adversarial input causes the model to ignore its instructions | Immediate if logged, otherwise indefinite |
| Vendor-side model change | Foundation model provider updates the model; behavior shifts without your code changing | Days, if output monitoring exists |

The common thread: most of these produce **no error, no crash, no alert** in
a conventional monitoring stack. Traditional ops monitoring (latency,
error rate, uptime) misses nearly all of them.

## 2. Severity taxonomy for AI incidents

Adapt standard incident severity levels to account for quality-based, not
just availability-based, harm.

| Severity | Definition | Example | Response time |
|---|---|---|---|
| SEV1 | Active harm to users/customers, or regulatory/legal exposure, ongoing | Loan-decision model producing systematically biased declines; LLM giving unsafe medical advice | Immediate, page on-call, exec notified within 1 hour |
| SEV2 | Significant quality degradation, not yet causing measurable harm but likely to soon | Recommendation model's CTR down 25% week-over-week with no known cause | Response within 4 hours, mitigation within 24 |
| SEV3 | Localized or edge-case failure, contained | Model mishandles a rare input category affecting <0.1% of traffic | Response within 1 business day |
| SEV4 | Known limitation, no active harm | Model underperforms on a language it was never designed to support, already documented | Logged, addressed in normal roadmap |

Calibrate SEV1/SEV2 boundaries with legal/compliance input specifically for
systems flagged high-risk in your governance inventory (Module 2) — a
quality dip in a marketing-copy generator and the same-size dip in a
credit-decision model are not the same severity.

## 3. The AI incident response runbook

| Step | Action | Owner |
|---|---|---|
| 1. Detect | Automated monitoring alert, user report, or internal audit finding | Monitoring system / any employee |
| 2. Triage | Assign severity using the taxonomy above within 30 minutes of detection | On-call ML lead |
| 3. Contain | For SEV1/2: roll back to last known-good model version, or disable the feature, before root-causing | Engineering on-call |
| 4. Communicate | Notify affected stakeholders (legal, affected product teams, execs per severity) with known facts only, no speculation | Incident commander |
| 5. Root-cause | Distinguish model issue vs. data issue vs. infrastructure issue vs. vendor issue | ML lead + data engineer |
| 6. Remediate | Fix, retrain, or permanently roll back; verify against the eval set before re-enabling | ML lead |
| 7. Postmortem | Blameless write-up within 5 business days: timeline, root cause, what monitoring would have caught it sooner | Incident commander |
| 8. Prevent recurrence | Add the missing check to the shared eval framework or monitoring stack (Module 5) so this class of failure is caught automatically next time | Platform/ML lead |

Step 3 deserves emphasis: for AI systems, "roll back to the last known-good
model version" is almost always faster and safer than trying to root-cause
under pressure while the current model keeps serving bad output. Treat
model rollback as routine, not exceptional — which requires model
versioning to already be in place before the incident, not built during it.

## 4. What good monitoring looks like

You cannot run this runbook without monitoring built to catch quality
issues, not just availability. Minimum viable AI monitoring includes:

- **Input distribution monitoring** — alert when the shape of incoming data
  shifts meaningfully from the training/eval distribution.
- **Output distribution monitoring** — alert on anomalies like a sudden
  spike in a particular prediction class, or (for LLMs) a spike in
  flagged/refused responses.
- **Proxy quality metrics in production** — edit rate, escalation rate,
  explicit user feedback, correlated against offline eval scores so you
  know when offline and online quality diverge.
- **Segment-level tracking**, not just aggregate — a model that looks fine
  in aggregate can be badly failing one customer segment or protected
  group, invisible until you slice the dashboard.

## Worked example

Nordway Insurance's claims-triage model, which routes incoming claims to
either fast-track auto-approval or manual review, started auto-approving an
unusual number of claims from one region over a two-week period. No error
was thrown; the model was doing exactly what it was trained to do.

It was caught not by an alert but by a claims adjuster who noticed the
pattern manually and flagged it — a detection failure the postmortem
called out explicitly. Root cause: a regional weather event had shifted
the distribution of incoming claims (more storm-damage claims, higher
average payout, different loss descriptions) away from what the model had
been trained on, and the model's confidence scores hadn't moved enough to
trigger the existing (too-loose) fallback-to-manual threshold.

Classified SEV2 (real financial exposure — an estimated $340K in claims
auto-approved that a manual reviewer would likely have flagged for further
investigation — but not yet a systemic or regulatory failure). Containment:
manual review threshold tightened immediately for the affected region.
Remediation: retrained on data including the regional event, with a new
input-distribution monitor specifically tracking claim-description
similarity to training data by region. The postmortem's key finding,
recorded and acted on: the existing monitoring only tracked model output
confidence, never input distribution — exactly the gap that let a two-week
drift run undetected. That monitor is now part of the shared eval framework
(Module 5) for every claims-adjacent model at the company.

## How It Actually Works

Nordway's confidence-score threshold failing to catch the drift illustrates
a specific and common blind spot: a model's confidence score is calibrated
against the training distribution, so it reflects how typical an input
*looks relative to what the model has seen before* — but a shift in the
input distribution itself (more storm-damage claims, different loss
descriptions) doesn't necessarily produce low-confidence predictions if the
new inputs happen to resemble existing feature patterns closely enough. The
model can be confidently, consistently wrong on an entire new sub-population
of claims precisely because confidence measures internal consistency with
what the model learned, not correctness relative to ground truth it has
never observed. This is exactly why output-confidence monitoring alone
misses this class of failure and input-distribution monitoring is a
structurally different signal: it compares the *shape of incoming data*
against the training distribution directly, independent of what the model
thinks about it, which is the only way to catch a shift the model itself
is not equipped to flag.

The rollback-before-root-cause ordering in step 3 reflects a basic
asymmetry in cost between the two courses of action: every additional hour
a degraded model keeps serving live traffic accrues real, compounding harm
(more bad claims decisions, more biased declines, more unsafe outputs),
while root-causing under pressure is slow and error-prone precisely because
it's happening under the stress of live harm continuing to accumulate.
Rolling back to a known-good, already-validated model version stops the
bleeding immediately and converts the situation from "harm ongoing, cause
unknown" to "harm stopped, cause to be determined at leisure" — a strictly
better position from which to investigate, since nothing about
understanding the failure requires the broken model to keep running. This
is also why rollback has to be pre-built rather than improvised: a rollback
path invented during an active incident is itself an untested piece of code
being deployed under pressure, which risks compounding the original
failure with a second, self-inflicted one.

## Exercise

Take an AI system you manage or have access to (or Nordway's claims model,
above, pre-incident).

1. **Classify its current monitoring** against the four failure modes with
   the longest typical detection lag in section 1 (drift, silent schema
   change, feedback loop, bias regression). For each, state whether you'd
   currently detect it in days, weeks, or "only if someone notices
   manually."
2. **Assign severity** to a real or plausible failure of this system using
   the taxonomy in section 2, and justify the assignment in one sentence.
3. **Write the postmortem's "prevent recurrence" line** (step 8 of the
   runbook) for that failure — the specific monitor or check you'd add, and
   where it would live so it protects other systems too, not just this one.
