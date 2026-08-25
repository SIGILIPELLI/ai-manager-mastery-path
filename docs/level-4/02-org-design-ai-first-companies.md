# 02 · Org Design for AI-First Companies

There is no single "correct" org chart for an AI-first company — the right
structure depends on whether AI is your product, your production process,
or a feature layered onto an existing business. What's consistent is the
set of design tensions every AI-first org has to resolve explicitly:
centralized vs. embedded AI talent, product-led vs. research-led
prioritization, and how much autonomy individual business units get to
make their own AI bets. This module gives you the structural patterns and
the decision criteria for choosing among them.

## 1. Three org design archetypes

| Archetype | Structure | Best fit | Main risk |
|---|---|---|---|
| Centralized AI org | One AI org reporting to a CAIO/CTO, serving all business units as an internal service | Company where AI capability needs to be consistent and shared across many similar use cases | Slower response to business-unit-specific needs; can become a bottleneck |
| Embedded model | AI talent distributed into business units, reporting to unit leaders, with a thin central standards function | Company where AI use cases are highly differentiated by business unit | Duplicated effort, inconsistent standards, harder to build shared platform (Level 3 Module 5) |
| Hybrid ("hub and spoke") | Central hub owns platform/standards/governance; embedded "spokes" own business-unit-specific application | Most large, multi-business-unit companies past a certain scale | Requires genuinely clear division of authority (see Level 3 Module 9) or it collapses into either pure model under pressure |

Most companies that start centralized (because that's how the first AI team
formed) drift toward hybrid as they scale past roughly 3-4 business units
with distinct AI needs — plan for that transition rather than being
surprised by it.

## 2. Where AI reports, and why it matters

| Reporting line | Signal it sends | Typical fit |
|---|---|---|
| CAIO/Chief AI Officer, reporting to CEO | AI is core strategy, not a support function | Company where AI is the primary competitive lever (see Module 1's positioning matrix) |
| Under CTO | AI is primarily a technical capability | Company where AI is mostly infrastructure/efficiency, not customer-facing differentiation |
| Under Chief Product Officer | AI is primarily a product capability | Company where AI-powered features are the main output, less emphasis on internal efficiency use cases |
| Under CDO (Chief Data Officer) | AI is treated as an extension of data strategy | Company earlier in maturity, where data infrastructure is still the binding constraint |

The reporting line is a real signal to the rest of the organization about
what AI *is* to the company — a mismatch (e.g., AI reporting to a CDO focused
on internal data quality, while the company's actual strategy depends on
AI-driven customer products) creates friction that shows up as
under-resourced product-facing AI work.

## 3. Designing for the research/applied split at scale

As covered at the team level in Level 3 Module 4, the research-vs-applied
distinction becomes an org design question at company scale: how much
distance should sit between people doing exploratory, longer-horizon work
and people shipping this quarter's roadmap.

| Pattern | Structure | Trade-off |
|---|---|---|
| Fully integrated | Research and applied engineers on the same team, same roadmap | Fast transfer of new techniques into product; research gets pulled into firefighting, loses long-horizon focus |
| Separate research org, handoff process | Dedicated research org publishes/prototypes, applied teams productionize | Protects research focus; handoff friction often kills good research before it reaches product |
| Rotational | Engineers spend defined stints (e.g., 2 of every 8 quarters) in a research capacity | Balances both; requires deliberate management, or "rotational" quietly becomes "permanent applied" |

Company size and AI maturity should drive this choice — a company with
fewer than ~40 AI ICs rarely benefits from a fully separate research org;
the overhead of maintaining two structures exceeds the focus benefit.

## 4. Signs your org design is wrong for your current stage

- **Every cross-business-unit AI decision requires a VP-level meeting** —
  sign that centralization has gone too far relative to the diversity of
  use cases.
- **Three business units independently build the same capability** — sign
  that embedding has gone too far without the hub layer from the hybrid
  model (see Level 3 Module 5's platform framework).
- **The most senior AI researcher spends most of their week in product
  status meetings** — sign the research/applied split needs more
  separation, not less.
- **A CAIO role exists but has no budget authority** — a title without
  structural power that will not survive the first real cross-functional
  conflict.

## Worked example

A mid-size insurance company, Palisade Mutual, grew its AI org from a single
central team of 12 to supporting five business units (claims, underwriting,
fraud, customer service, and a new usage-based-insurance telematics
product) over three years, without ever revisiting the original fully
centralized structure. By year three, the underwriting business unit —
whose AI needs were both the most mature and the most differentiated from
the others — was routing around the central team entirely, hiring its own
"data analysts" who were, in practice, doing unsupervised ML engineering
work outside any shared standard or governance review.

The CTO, applying this module's framework, reorganized into a hybrid model:
a central hub of 9 people retained ownership of the shared model registry,
eval framework, and governance sign-off (per Level 3 Modules 5 and 9), while
each business unit got 2-4 embedded AI engineers reporting into that unit's
leadership with a dotted line to the hub for technical standards. The
underwriting unit's shadow "data analyst" hires were formally reclassified
and brought under the shared governance process — a move that surfaced, in
the resulting audit, an underwriting model already in limited production
that had never gone through any bias testing. The gap was closed within
one quarter, avoiding what would very plausibly have been a regulatory
finding if a state insurance examiner had found it first.

## Exercise

Take your own organization (or Palisade Mutual, pre-reorg).

1. **Classify your current structure** against the three archetypes in
   section 1. If it doesn't cleanly match one, describe the specific hybrid
   you actually have, including where it's ambiguous.
2. **Evaluate your AI reporting line** against section 2 — does it match
   what AI actually *is* to your company's strategy (per Module 1's
   positioning matrix), or is there a mismatch worth flagging?
3. **Check for the four warning signs** in section 4 against your own org.
   For any present, name the specific structural change (not just "improve
   communication") that would address it.
