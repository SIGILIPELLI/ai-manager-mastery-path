# 01 · What Is AI Management?

"AI management" is a fast-forming discipline sitting at the intersection of
product management, engineering management, and data science leadership. It
did not exist as a named job ten years ago, and its boundaries are still
being drawn differently at every company you'll interview with. This module
gives you a working map of the role, the closely related roles it's
frequently confused with, and the specific skills that separate someone who
merely "likes AI" from someone who can actually run AI work. Everything that
follows in this program builds on the distinctions made here.

## 1. What an AI manager actually does

An AI manager is responsible for turning an AI/ML capability — a model, a
pipeline, an LLM-powered feature — into something that ships, works reliably
in production, and delivers a measurable business outcome. That responsibility
spans four recurring activities:

| Activity | What it looks like day to day |
|---|---|
| **Scoping** | Translating a vague ask ("can we use AI to reduce churn?") into a specific, testable problem statement with a target metric |
| **Team leadership** | Managing or coordinating data scientists, ML engineers, MLOps engineers, and the product/design/legal partners around them |
| **Risk & governance** | Making sure the model's failure modes, data sources, and compliance exposure are understood *before* launch, not discovered after |
| **Delivery & iteration** | Running the project through experimentation, deployment, and the ongoing tuning that AI systems need after they ship |

Note what is *not* on this list: personally writing training code, tuning
hyperparameters, or building the data pipeline. An AI manager needs to
understand these well enough to ask good questions and catch bad answers —
that's the entire purpose of this training track — but the hands-on
implementation belongs to the team.

## 2. AI PM vs. AI engineering manager vs. AI program manager

These three titles get used interchangeably in job postings, but they carry
different day-to-day realities. Knowing which one you're being hired for (or
which one your org actually needs) avoids a mismatch that surfaces painfully
around month three.

| Role | Primary accountability | Reports to / works with | Success measured by |
|---|---|---|---|
| **AI Product Manager** | *What* gets built and *why* — problem selection, prioritization, user/business value | Usually a product org; partners with an ML lead | Business metrics (adoption, revenue impact, retention) |
| **AI Engineering Manager** | *How* it gets built — team structure, technical quality, delivery cadence, career growth of ICs | Usually an engineering org; may have a product-manager peer | Team velocity, system reliability, technical debt trend |
| **AI Program/Project Manager** | *When* and *coordination* — cross-team dependencies, timeline, risk tracking across a portfolio of AI efforts | Often a PMO or a VP; coordinates multiple AI PMs/EMs | On-time delivery, cross-team blockers resolved |

A useful gut-check: if your calendar is mostly full of roadmap and
prioritization conversations, you're closer to AI PM. If it's full of 1:1s,
sprint planning, and code-review escalations, you're closer to AI EM. If it's
full of status syncs across teams that don't report to you, you're closer to
AI program manager. Many real jobs blend two of these — especially at
smaller companies — but the blend should be a deliberate choice, not an
accident of an unclear job description.

## 3. Why AI management is harder than "regular" software management

Traditional software has a property AI systems mostly lack: given the same
input, you get the same output, every time. That single difference cascades
into everything an AI manager has to handle differently:

| Traditional software trait | AI/ML equivalent | Management implication |
|---|---|---|
| Deterministic output | Probabilistic output — the same input can yield a different (or wrong) answer | Timelines must budget for "the model might just not get good enough" as a real outcome, not a risk to wave away |
| Spec written up front | Spec discovered through experimentation | Planning uses ranges and checkpoints, not fixed deliverable dates |
| Bugs are binary (present/absent) | Quality is a spectrum (85% accurate vs. 91% accurate) | "Done" means "meets an agreed threshold," which must be defined before work starts |
| Behavior fully explained by code | Behavior partly explained by training data | Data quality and provenance become the manager's problem too, not just the model's |
| Regression tests catch breakage | Model drift can silently degrade quality over weeks | Ongoing monitoring is part of the deliverable, not a "nice to have" |

## Worked example

A mid-size retail company's VP of Customer Experience asks for "an AI
chatbot that reduces support tickets." Three different hires would approach
this differently, and the difference illustrates the roles above:

- An **AI PM** would first ask: which ticket categories are highest volume
  and most automatable, what's the current cost per ticket, and what
  reduction percentage would make this worth building — before any tool is
  chosen.
- An **AI engineering manager** would assess team capacity, decide whether
  to build on an in-house LLM integration or a vendor platform, and structure
  a small team (one ML engineer, one backend engineer, one support-domain
  SME) with a realistic sprint cadence.
- An **AI program manager** brought in because this touches the support
  team, the website team, and legal (for data-retention questions) would
  track those three dependencies and flag the legal review as the
  likely critical-path bottleneck two weeks before it becomes one.

A single strong AI manager in a smaller company would do all three — but
should still *name* which hat they're wearing in each meeting, because the
questions worth asking differ sharply between them.

## Exercise

Pick an AI-related initiative from your own organization (or a plausible one
if you're not currently in an AI-adjacent role — e.g., "add AI-generated
product descriptions to an e-commerce site"). Write three short paragraphs,
one from the perspective of each role above (AI PM, AI EM, AI program
manager), describing the first three questions that role would ask before
committing to a timeline. Then write one paragraph identifying which of the
three questions sets is most urgently missing at your organization today,
and why.
