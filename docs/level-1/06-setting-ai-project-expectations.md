# 06 · Setting AI Project Expectations

The single most common source of AI project failure isn't a bad model — it's
a good model that was promised on a bad timeline, to a stakeholder who was
never told that "we don't know exactly how long this will take" is a
legitimate, professional answer. This module covers how to communicate
uncertainty honestly while still giving stakeholders something they can plan
around, and how to structure commitments so an AI project doesn't quietly
become "the thing that's always six weeks from done."

## 1. Why AI timelines are inherently uncertain

Unlike a typical feature build, an AI project's duration depends on
questions that can only be answered *by doing the work*: will this approach
reach the needed quality bar at all, and if so, after how many iterations?
Refusing to acknowledge this uncertainty up front doesn't remove it — it
just moves the moment of painful discovery from the kickoff meeting to a
missed deadline.

| Traditional estimate | AI project estimate |
|---|---|
| "This feature takes 3 weeks" | "The proof of concept takes 3 weeks; whether it's viable to proceed is the outcome of those 3 weeks, not a given" |
| Effort scales roughly linearly with scope | Effort can be dominated entirely by one unknown (data quality, achievable accuracy) that no amount of extra headcount fixes |
| Missing a deadline usually means "not done yet" | Missing a quality bar can mean "not achievable with this approach," which is a different conversation entirely |

## 2. The range-and-checkpoint communication framework

Instead of a single date, communicate a **range** tied to explicit
**checkpoints** where the range narrows. This is honest, and it gives
stakeholders real planning information at each stage rather than false
precision followed by a broken promise.

| Stage | What you communicate | Example |
|---|---|---|
| Kickoff | A wide range and the first checkpoint date | "Feasibility in 3 weeks; if it clears the bar, full build is 2–4 months; if not, we'll have a clear alternative recommendation" |
| After feasibility checkpoint | A narrowed range based on real evidence | "Feasibility cleared the bar with margin to spare; full build now estimated at 2.5–3 months" |
| Mid-development checkpoint | Confirm or further narrow | "On track for the low end of that range; no red flags in this iteration" |
| Pre-launch checkpoint | A firm date, now backed by evidence, not hope | "Launch-ready in 2 weeks pending final monitoring setup" |

## 3. Setting a shared definition of "good enough"

Before work starts, get explicit, written agreement — from the business
sponsor, not just the technical team — on what quality bar counts as
"ready to ship." Without this, "is it done yet?" becomes a subjective,
recurring argument instead of a checkable fact.

| Element to agree in writing | Example |
|---|---|
| **Primary metric** | Precision on flagged fraud cases |
| **Minimum acceptable threshold** | 80% precision at 60% recall |
| **Evaluation conditions** | Measured on the most recent full quarter of real transactions, not a curated test set |
| **What happens if the bar isn't met** | Ship a rules-based fallback for this release; revisit the model next quarter |

## 4. Managing scope creep and "just one more feature" requests

AI projects are especially vulnerable to expanding scope mid-flight, because
each new capability sounds achievable in a demo. Two habits contain this:

| Habit | Why it works |
|---|---|
| Log every scope-change request against the original success metric | Forces the requester to justify the addition against what was actually promised, not just "wouldn't it be nice" |
| Re-run the range-and-checkpoint conversation for any accepted scope change | Prevents scope from growing "for free" while the original date silently stays fixed |

## Worked example

A marketing team asks for a model recommending which customers to target
with a retention offer, expecting it "in a month, like the last few
features." The AI manager sets a 2-week feasibility checkpoint with an
explicit success bar (lift over random targeting of at least 15%, measured
on a held-out sample) agreed in writing with the marketing VP beforehand.
Feasibility comes back at 22% lift — comfortably clearing the bar — and the
manager now gives a confident 5–7 week range for full build, backed by real
evidence rather than an initial guess. Two weeks into the build, the
marketing team asks to also predict *which specific offer* to send, not just
who to target — a meaningfully larger scope. The manager logs this as a new
request, points to the original success metric it wasn't part of, and offers
two options: ship the original scope on the original timeline and treat
offer-personalization as a fast-follow, or extend the timeline by 3–4 weeks
to include it now. The stakeholder, seeing the tradeoff made explicit,
chooses the fast-follow — a decision that would have been an unspoken,
resentment-generating slip if scope had just quietly expanded instead.

## How It Actually Works

The range-and-checkpoint framework works because it aligns the *shape* of a
communicated estimate with the actual shape of the underlying uncertainty,
instead of forcing a single number onto a process that doesn't produce one.
A traditional feature's remaining unknowns shrink roughly linearly as work
gets done — each day of coding removes a known, bounded amount of remaining
work. An AI project's uncertainty is lumpy: almost all of it is concentrated
in a small number of specific unknowns (does this data support the target
accuracy at all, does the chosen architecture converge on it) that resolve
suddenly, at the moment an experiment finishes, rather than gradually. A
single point estimate given at kickoff is really a guess at the *outcome* of
an experiment that hasn't been run yet — mathematically no more grounded
than a coin flip weighted by experience — while a range that narrows at each
checkpoint is reporting the estimate only after the relevant uncertainty has
actually resolved. This is why the range at each stage in the table gets
narrower specifically *after* a checkpoint and not gradually across the
weeks in between: nothing informative happens to the estimate during an
experiment's run, only at its conclusion.

The scope-creep discipline works for a related mechanical reason: a written
success metric acts as the fixed reference point against which any new
request's marginal cost can be honestly compared, because without it,
"wouldn't it be nice to also predict the offer type" is being compared to
nothing — there's no anchor showing that offer-type prediction is a
materially different modeling problem (a different target variable, its own
feasibility question, its own evaluation data) rather than a small addition
to the existing one. Logging the request against the original metric forces
the comparison to happen explicitly, at the moment the tradeoff is still
cheap to make, rather than being absorbed silently into "the model" as a
single expanding blob of work whose real cost only becomes visible once the
combined timeline has already slipped.

## Exercise

Take an AI project you're planning (real or plausible). Write: (1) the
kickoff-stage range-and-checkpoint statement you'd give a stakeholder,
following the format in section 2; (2) a filled-out "definition of good
enough" table from section 3, with a real number for the threshold; and (3)
one likely scope-creep request you can anticipate, and the exact sentence
you'd use to redirect it back to the original success metric.
