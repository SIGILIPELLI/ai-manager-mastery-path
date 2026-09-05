# 02 · AI Governance & Compliance

Governance is not a document your legal team writes and your engineers
ignore. Done well, it's the set of checkpoints that catch a problem while it
still costs an afternoon to fix, instead of after launch when it costs a
regulator's attention. As a manager overseeing AI work, you don't need to
become a lawyer — you need to know which regulatory categories apply to
what you're building, and run a repeatable internal process that produces
evidence, not just good intentions.

## 1. The regulatory landscape, at manager altitude

You don't need case law. You need to know which regime plausibly applies to
your system, because that determines what evidence you must be able to
produce on request.

| Regime | Applies to | What it requires in practice |
|---|---|---|
| EU AI Act | Any AI system used in or affecting the EU market, tiered by risk | High-risk systems (hiring, credit, health) need conformity assessment, documentation, human oversight, logging |
| US sectoral rules (e.g., ECOA, FCRA, HIPAA, EEOC guidance) | Credit, employment, health, insurance decisions in the US | Adverse-action explanations, non-discrimination testing, data handling per sector rules |
| State AI laws (e.g., Colorado AI Act, NYC Local Law 144) | Automated employment decisions, consumer-facing high-risk AI in that state | Bias audits (often annual, third-party), notice to affected individuals |
| GDPR / state privacy laws | Any system processing personal data of covered individuals | Lawful basis for processing, right to explanation for automated decisions, data minimization |
| Sector-specific supervisory guidance (e.g., banking regulators on model risk) | Regulated financial institutions | Formal model risk management (validation, ongoing monitoring, documented limitations) |

The manager-level skill is triage: for any given system, ask "does this
touch credit, employment, health, housing, or another protected decision
category, and does it touch EU or a state with a specific AI statute?" If
yes to either, treat it as high-risk regardless of how the engineering team
classifies it technically.

## 2. The governance intake checklist

Require this before a model or LLM feature goes to production, not before it
starts development — you want it early enough to change course cheaply.

| Question | Why it matters | Who answers |
|---|---|---|
| Does this system make or materially inform a decision about a person (hiring, credit, benefits, pricing, moderation)? | Determines regulatory tier | Product owner |
| What data trained or informs it, and do we have rights to use it this way? | Data provenance and consent gaps are the most common post-launch surprise | Data lead |
| Has it been tested for disparate impact across protected groups? | Required by several regimes; also just good practice | ML lead |
| Can we produce a plain-language explanation of a specific decision if asked? | Adverse-action and right-to-explanation requirements | ML lead + product |
| Is there a human review step before an adverse decision takes effect? | Often a legal requirement, not just a best practice | Product owner |
| Who is accountable if this system causes harm, and how would we find out? | Determines whether monitoring exists at all | Engineering manager |
| Is there a documented decommission/rollback plan? | High-risk systems generally require an exit path | Engineering manager |

Score each row red/yellow/green. Anything red blocks launch; anything
yellow needs an owner and a date, tracked the same way you'd track an
open incident.

## 3. Building the internal review process

A governance review that only exists on paper the week before a regulator
asks about it is worse than none — it signals the org talks about
compliance without practicing it. Build a lightweight, real cadence:

| Stage | Timing | Output |
|---|---|---|
| Intake review | Before development starts | Risk tier assigned (low/medium/high); if high, legal and privacy are looped in now |
| Pre-launch review | 2-4 weeks before planned launch | Completed intake checklist; bias test results; explanation capability confirmed |
| Post-launch audit | 90 days after launch, then annually | Are the pre-launch assumptions still true? Has usage drifted into a new decision category? |
| Incident-triggered review | Any time a governance-relevant incident occurs | Root cause; whether other systems share the same exposure |

The single highest-leverage habit: maintain one **system-of-record
inventory** listing every AI system in production, its risk tier, its last
review date, and its owner. Most organizations that fail an audit don't
fail because a system was non-compliant — they fail because they couldn't
produce a complete list of what they had running at all.

## 4. Common manager mistakes

- **Treating governance as a one-time gate.** Models drift, data sources
  change, and a system's actual use often diverges from its intended use
  (a "recommendation" tool quietly becomes a de facto decision-maker because
  staff stop overriding it). Reviews must recur.
- **Routing everything through legal instead of triaging first.** Legal
  time is scarce; sending every low-risk internal tool through full review
  trains the org to route around governance entirely. Triage low-risk items
  quickly so legal's time goes to genuinely high-risk systems.
- **No paper trail for "we decided this was low risk."** If a regulator or
  auditor later disagrees with your risk tiering, the only defense is a
  documented, reasoned decision made at the time — not a reconstruction
  after the fact.

## Worked example

A mid-size fintech, Larkspur Lending, built an LLM-based tool to help loan
officers draft explanations for declined applications, intended purely as a
drafting aid with a human required to edit and approve before sending. Six
months post-launch, the compliance team ran the quarterly audit required by
this module's process and found that officers were approving the LLM draft
unedited 94% of the time — the tool had become the de facto decision
explanation, not a drafting aid, without anyone deciding that.

Because the intake checklist had flagged this as touching a protected
decision category (credit) at launch, a human-review step and a monitoring
metric ("edit rate on drafts") were already in place — the drift was
caught within the first quarterly cycle, not discovered externally. The
fix was operational, not technical: officers were required to document a
specific reason for any unedited approval, and edit rate became a tracked
KPI reported to the head of lending. Edit rate rose to 61% within two
months, and — more importantly — the org had documented evidence, dated
before any complaint arose, that it had identified and corrected functional
drift in a high-risk system. That documentation is exactly what regulators
ask for first.

## How It Actually Works

The Larkspur drift — a drafting aid becoming a de facto decision-maker at a
94% unedited-approval rate — happens through the exact same automation-
complacency mechanism covered in Level 1's risk basics module, but it's
worth tracing why it's specifically *undetectable* without a monitoring
metric built in advance. Nothing about the system's behavior changed
between launch and month six: the LLM kept generating the same kind of
draft, at the same quality, with the same human-review step nominally in
place. What changed was the loan officers' behavior — as they experienced
the drafts being correct often enough, their subjective confidence rose
faster than the model's actual reliability, and the review step degraded
from genuine scrutiny to a formality, exactly as predicted by the
rubber-stamping pattern in Level 2's responsible-AI checklist. This is
precisely why "edit rate" has to be instrumented *before* launch: the drift
produces no error, no support ticket, no system log entry distinguishing a
carefully-reviewed approval from a rubber-stamped one — the only trace it
leaves is a statistical pattern in how often humans change the output, and
that pattern is invisible unless someone is already measuring it.

The system-of-record inventory's outsized importance follows from a
different mechanical fact about audits: an auditor or regulator cannot ask
about a system they don't know exists, so an organization's actual
compliance exposure is bounded by what it can produce a complete list of,
not by what any individual system's paperwork says. A single system with
excellent documentation but sitting outside the inventory is functionally
invisible to the governance process — it will never be pulled into a
review cycle, never get a risk tier, never surface in an audit response
unless someone happens to remember it exists. This is why organizations
fail audits over an incomplete list rather than over a specific system's
non-compliance: the inventory is the mechanism that converts "we have a
governance process" from a claim about intentions into a claim that's
actually verifiable against every system currently running.

## Exercise

Pick an AI system in your organization (or Larkspur Lending's drafting
tool, above, at month 1).

1. **Run the intake checklist** in section 2 against it. Score every row and
   flag any red or yellow items with an owner and date.
2. **Classify its regulatory exposure** using the table in section 1. Name
   the specific regime(s) that plausibly apply and why.
3. **Write the one-paragraph entry** that would go in your system-of-record
   inventory for this system: risk tier, last review date, owner, and next
   scheduled review.
