# 05 · Cross-Team AI Platform Strategy

Once an organization has more than one AI team, someone eventually asks:
"should we build a shared platform?" The honest answer is usually "not
yet, and here's what would have to be true first." A platform built too
early solves problems nobody has yet, gets built to the wrong abstraction,
and turns into overhead the pods route around. A platform built too late
means every team has independently reinvented feature stores, eval
harnesses, and deployment pipelines, at real and mostly invisible cost.
This module gives you the decision framework for when and what to
centralize.

## 1. The build-a-platform decision framework

Don't start with "what could we centralize." Start with evidence of real,
measured duplication cost.

| Signal | Threshold worth acting on | How to verify it's real, not anecdotal |
|---|---|---|
| Duplicated infrastructure | 2+ teams independently building the same capability (feature store, eval harness, model registry) | Audit actual tooling in use across teams, not what's on a slide |
| Duplicated vendor spend | 2+ teams separately licensing overlapping tools | Pull vendor contracts, check for overlap in capability, not just vendor name |
| Inconsistent standards causing incidents | An incident traced to one pod's practice not matching another's (see Module 6) | Root-cause reports citing "no shared standard" as a contributing factor |
| Onboarding friction | New hires or transfers report re-learning tooling per pod | Exit/transfer interview data, not just complaints in a hallway |

If none of these are present yet, the right move is usually a **shared
standard, not a shared platform** — e.g., "all pods use this eval report
format" costs almost nothing and captures much of the benefit of full
platformization without the overhead of a dedicated team.

## 2. What to centralize first, in order

When the evidence does justify a platform investment, sequence it by
leverage, not by what's technically interesting to build.

| Priority | Capability | Why it comes first |
|---|---|---|
| 1 | Model/experiment registry | Prevents the highest-cost failure (re-running known-negative experiments); cheapest to build |
| 2 | Shared eval framework | Makes cross-pod risk and quality comparable; required for governance (Module 2) to function at all |
| 3 | Deployment/serving infrastructure | High effort, high payoff — but only after 1-2 exist, or you'll standardize the wrong pipeline |
| 4 | Feature store | Highest effort, most organization-specific; often better bought than built below a certain scale |
| 5 | Fine-tuning/training infrastructure | Only justified once multiple teams train models at meaningful frequency and scale |

Notice the registry and eval framework are both *process-plus-lightweight-
tooling* investments, buildable by a two-person team in weeks. The later
items are substantial engineering projects — don't let a team's enthusiasm
for building infrastructure jump the queue ahead of demonstrated need.

## 3. The internal platform-as-product model

The platform team's biggest risk is becoming an ivory tower that builds
what it thinks pods need. Run it like an internal product team with real
customers:

| Product-team practice | Platform-team equivalent |
|---|---|
| Customer interviews | Regular check-ins with each pod's lead on what's blocking them |
| Adoption metrics | % of pods actually using the platform vs. maintaining a workaround |
| Roadmap prioritized by customer request | Roadmap prioritized by pod-reported friction, not platform-team preference |
| Deprecation policy | A pod that adopts the platform shouldn't be punished with unannounced breaking changes |
| A named point of contact per customer | A platform liaison embedded or assigned per pod |

Track **adoption rate**, not lines of code shipped or features built. A
platform with beautiful architecture and 20% adoption has failed at its
actual job, which is reducing organization-wide duplication.

## 4. Governance for the platform itself

A shared platform becomes a single point of failure and a single point of
control — both need explicit governance, or the platform team accumulates
unaccountable power over every pod's roadmap.

- **Change approval process.** Breaking changes to shared infrastructure
  need a notice period and pod sign-off, not a Slack message the morning of.
- **SLA for platform reliability.** If the eval framework is down, every
  pod's release process stalls — define an uptime/response-time commitment
  like any other production dependency.
- **An escape hatch.** Pods should be able to opt out of the platform for a
  specific need with a documented reason, rather than building silent
  shadow infrastructure because the platform team said no.

## Worked example

A consumer fintech, Ashgrove Financial, had three AI pods (fraud, credit
underwriting, and a customer-service LLM assistant) each running its own
model registry by month 18 of the company's AI investment. The head of AI,
new to the role, found this out only when the credit team re-ran an
experiment the fraud team had already completed and found negative six
months earlier — the two teams had no shared visibility.

Applying the framework: the duplication signal was real and measured (three
registries, one wasted experiment costing roughly 3 person-weeks, and two
separate LLM API vendor contracts with 70% overlapping capability). Per the
priority order in section 2, the head of AI built a shared model/experiment
registry first — a four-week project for two engineers — before touching
anything else, deliberately declining a proposal from one pod lead to build
a full shared feature store immediately, since no duplication evidence yet
existed at that layer.

Adoption was tracked explicitly: 100% of new experiments were required to
log to the shared registry starting week 5, with a dashboard showing
compliance per pod visible to all three pod leads. By month 3, cross-pod
duplicate work dropped to zero measured instances, and the vendor contract
review consolidated the two overlapping LLM API contracts, saving
approximately $95K/year. The feature store was revisited eight months later,
once genuine duplication evidence existed at that layer too — and by then
the platform team, having earned trust with the registry, had pods actively
requesting it rather than needing to be sold on it.

## How It Actually Works

The registry-before-feature-store sequencing works because the two
capabilities have fundamentally different dependency structures on
organizational maturity. A model/experiment registry has almost no
prerequisite: it's a place to record what was tried and what happened, and
its value (preventing the exact re-run-a-known-negative failure Ashgrove
hit) is realized the moment even two teams start using it consistently. A
feature store, by contrast, requires the organization to already agree on
feature definitions, freshness requirements, and access patterns across
teams whose actual needs may still be genuinely different — building it
before that convergence exists means guessing at an abstraction the real
usage patterns haven't revealed yet, which is exactly why "no duplication
evidence yet existed at that layer" was the correct reason to defer it: an
abstraction built ahead of evidence encodes assumptions instead of observed
need, and those assumptions are usually wrong in ways only visible after
multiple teams have organically converged on similar patterns.

Tracking adoption rate rather than lines of code shipped follows from what
a platform is actually for: eliminating organization-wide duplication only
happens if pods stop maintaining their own version and use the shared one
instead, so a platform's entire value proposition is contingent on adoption
in a way most engineering work isn't — a beautifully engineered registry
nobody uses has produced zero reduction in duplicate spend or duplicate
experiments, the exact problem it was built to solve. This is also why an
escape hatch matters mechanically rather than just diplomatically: a pod
that's blocked from opting out of a platform that genuinely doesn't fit its
need will build shadow infrastructure anyway, but now invisibly, which
reintroduces the original duplication problem in a form the platform team
can no longer see or measure — an explicit, documented opt-out keeps the
duplication visible and countable, even when it can't be eliminated.

## Exercise

Take your own multi-team AI org (or Ashgrove Financial, above, at month 17).

1. **Run the evidence check** in section 1 against your actual org. For each
   signal, cite a specific instance (a duplicated tool, a specific
   incident, an onboarding complaint) or mark it absent — don't guess.
2. **If evidence exists, sequence a platform build** using the priority
   order in section 2. Name what you'd build first and what you'd
   deliberately defer, and why.
3. **Design one adoption metric** for a platform capability you already
   have or plan to build, and state the number you'd consider a
   success/warning/failure threshold.
