# 05 · AI Regulation & Policy at Scale

Level 3's governance module covered building a compliance process for a
single organization's systems. At the executive level, the problem compounds:
you're likely operating across multiple jurisdictions with different (and
sometimes conflicting) AI regulations, tracking a regulatory landscape that
is still being written in real time, and making capital-allocation
decisions — where to launch a product, how to architect a system — based on
regulatory exposure that may change materially before the system ships.
This module covers managing that at scale, including when and how to engage
in policy shaping rather than pure compliance.

## 1. Multi-jurisdiction exposure mapping

| Jurisdiction | Current posture (as of 2026) | Key obligation for high-risk AI |
|---|---|---|
| EU | Comprehensive, risk-tiered (AI Act), phased implementation | Conformity assessment, documentation, human oversight for high-risk categories |
| United States (federal) | Sectoral, no single comprehensive federal AI law; agency guidance (FTC, EEOC) plus executive orders that shift with administrations | Existing sectoral law (credit, employment, health) applies to AI decisions the same as any decision |
| US states | Increasingly active — comprehensive state AI laws (e.g., Colorado) and narrower ones (e.g., NYC automated employment decision tools) | Varies significantly; often requires bias audits and consumer notice |
| China | Algorithm registration and content requirements, especially for generative AI | Registration with regulators, content moderation obligations |
| Other major markets (UK, Canada, Japan, Brazil) | Mixed — ranging from principles-based guidance to emerging comprehensive frameworks | Varies; monitor actively rather than assuming parity with EU/US |

Build a live map — not a one-time legal memo — of which jurisdictions your
products actually operate in or serve customers from, cross-referenced
against which of your systems are high-risk per your governance inventory
(Level 3 Module 2). The intersection of "high-risk system" and "regulated
jurisdiction" is where executive attention belongs first.

## 2. The regulatory scenario-planning framework

Because AI regulation is actively being written, treat major product and
architecture decisions with explicit scenario planning rather than
betting on a single predicted regulatory outcome.

| Scenario | Probability-weighted planning question | Hedge |
|---|---|---|
| Regulation tightens faster than expected in a key market | Would this system require conformity assessment or documentation we don't currently produce? | Build documentation/audit trail capability now, even if not yet strictly required — it's cheaper to build in from the start |
| Regulation diverges sharply across jurisdictions | Can we operate one global system, or do we need jurisdiction-specific variants? | Architect for configurability (feature flags, jurisdiction-aware behavior) rather than hard-coding one global behavior |
| A specific enforcement action sets an unexpected precedent | Would our current practice survive the same scrutiny that triggered the action? | Track enforcement actions against comparable companies, not just statute text |

## 3. When and how to engage in policy shaping

Executives increasingly face a choice about whether to engage with
regulators and industry bodies proactively, not just react to finished
rules. This is a legitimate and often necessary executive function — done
transparently, it is not the same as regulatory capture, though the
distinction requires deliberate discipline.

| Engagement level | What it looks like | When appropriate |
|---|---|---|
| Monitor only | Track proposed regulation, no direct engagement | Small player, low regulatory sophistication needed yet |
| Industry association participation | Join a trade body's AI policy working group | Mid-size company wanting a voice without bearing sole responsibility for positions taken |
| Direct regulatory engagement | Respond to public comment periods, meet with regulators/staff | Company with material exposure to a specific rule, resources to engage substantively and transparently |
| Public advocacy | Public statements, testimony | Reserved for genuinely material issues where the company's perspective adds public value — overuse dilutes credibility |

The guiding principle for staying on the right side of legitimate policy
engagement versus self-serving capture: engage on rules that affect how AI
is regulated broadly and say so publicly, not on securing a carve-out
specific to your company that disadvantages competitors or the public.

## 4. Board reporting on regulatory exposure

Boards increasingly ask for a standing regulatory risk report, not a one-
time briefing. Structure it around:

- **Current exposure map** (section 1), updated quarterly.
- **Material regulatory changes since last report**, with a plain-language
  "what this means for us" — not a legal summary.
- **Open scenario-planning items** (section 2) with owners and target dates.
- **Any enforcement actions against comparable companies**, and an honest
  self-assessment of whether the same finding would apply internally.

## Worked example

A global HR-tech company, Windham Talent Systems, sells an AI-driven
candidate-screening product used by employers across the US, EU, and UK.
Its exposure map (section 1) flagged this specific product as high-risk in
all three jurisdictions — an automated employment decision tool under NYC
Local Law 144, a high-risk system under the EU AI Act, and subject to
increasing UK regulatory guidance on algorithmic hiring.

Rather than building three separate compliance regimes reactively as each
jurisdiction's requirements came due, the executive team applied the
scenario-planning framework in section 2 early: they built a single
architecture with jurisdiction-aware configuration (bias-audit reporting,
candidate notice language, and human-review requirements all
parameterized by jurisdiction) rather than a US-first product retrofitted
later. When Colorado's state AI law took effect with new bias-audit
disclosure requirements, Windham was able to comply within the existing
architecture in three weeks — a competitor building jurisdiction-specific
patches after the fact took four months and lost two enterprise accounts
during the gap when those customers' own compliance teams flagged the
delay as a vendor risk.

Windham also joined an HR-tech industry association's AI policy working
group (an "industry association" level of engagement per section 3),
publicly supporting a proposed federal framework for automated employment
decision tools specifically because it would have leveled the compliance
burden across the industry rather than advantaging Windham's own existing
architecture — a distinction their public comment letter stated explicitly,
which the CEO's team viewed as important for credibility with both
regulators and customers evaluating multiple vendors.

## Exercise

Take your own organization's highest-regulatory-exposure AI system (or
Windham's candidate-screening product, above, pre-architecture-decision).

1. **Build the exposure map** in section 1 for this system: which
   jurisdictions does it operate in, and what's the specific obligation in
   each?
2. **Run one scenario** from section 2 against this system — pick the
   scenario most plausible for your situation and state the specific hedge
   you'd invest in now.
3. **Decide your appropriate engagement level** from section 3, and justify
   in two sentences why a higher or lower level of engagement would be
   inappropriate for your company's current scale and exposure.
