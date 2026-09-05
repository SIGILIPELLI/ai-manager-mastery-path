# 10 · Project — An AI Governance Framework for an Organization

This project pulls together Modules 1-9 into one deliverable: a complete AI
governance framework you could hand to a CEO or board and have them
understand exactly how your organization decides what's safe to build,
launch, and keep running. Rather than a hypothetical exercise, this module
walks through a full worked deliverable for a fictional company, Ridgeline
Analytics, so you can see the finished shape before adapting it to your own
organization.

## Company context

**Ridgeline Analytics** is a 340-person B2B SaaS company selling supply-
chain forecasting software to mid-size manufacturers. It runs four AI/ML
systems in production: a demand-forecasting model (core product), an
anomaly-detection alert system (core product), an internal sales-lead
scoring model (internal tool), and a newly launched LLM-based customer
support assistant. It has 22 AI/ML-adjacent employees across two pods plus
a two-person platform pair, no dedicated AI compliance role yet, and is
starting to sell into the EU, which is what triggered this governance
project.

## 1. System-of-record inventory

| System | Risk tier | Rationale | Owner | Last reviewed |
|---|---|---|---|---|
| Demand-forecasting model | Medium | Informs customer business decisions but with human review before action; no protected-class decision | Pod A lead | New — first review this cycle |
| Anomaly-detection alerts | Low-Medium | Flags for human review, doesn't act autonomously | Pod A lead | New |
| Sales-lead scoring | Low | Internal only, no customer-facing decision, no protected category | Pod B lead | New |
| LLM support assistant | Medium-High | Customer-facing, EU exposure, handles account data, could give incorrect operational guidance | Pod B lead | New (pre-launch review overdue — flagged) |

This inventory is the single artifact every later section depends on. It is
reviewed and re-tiered quarterly, and any new system is added at intake,
before development starts, per Module 2.

## 2. Governance intake checklist (applied to the support assistant, the highest-risk item)

| Question | Answer | Status |
|---|---|---|
| Makes/materially informs a decision about a person? | Advises customers on inventory actions; not a protected-class decision, but errors have real operational cost | Yellow |
| Data provenance and usage rights confirmed? | Trained on internal docs + customer conversation logs; customer ToS updated to cover this use | Green |
| Tested for disparate impact? | Not applicable in the traditional sense (no protected-class decision), but tested for consistent quality across customer company sizes | Green |
| Explanation capability for a specific output? | Can show source documents retrieved for any answer | Green |
| Human review before consequential action? | Currently answers directly with no review step for account-configuration guidance | **Red — blocking** |
| Accountability and monitoring owner named? | Pod B lead, but no monitoring dashboard live yet | Yellow |
| Rollback/decommission plan documented? | Feature flag exists; no formal rollback runbook written | Yellow |

**Governance decision: launch blocked** on the human-review gap for
account-configuration guidance specifically (a customer could otherwise
act on an incorrect answer with real operational consequences). Informational
Q&A responses (not configuration guidance) are approved to proceed. This
is exactly the kind of finding this process exists to catch before launch
rather than after a customer incident.

## 3. Review cadence

| Stage | Timing (Ridgeline's calendar) | Owner |
|---|---|---|
| Intake review | At project kickoff, all new systems | CoE liaison (see section 6) + pod lead |
| Pre-launch review | 3 weeks before launch date | CoE liaison, legal (for medium+ risk only) |
| Post-launch audit | 90 days post-launch, then every 2 quarters | CoE liaison |
| Incident-triggered review | Within 48 hours of any SEV1/SEV2 (per Module 6 taxonomy) | Incident commander + CoE liaison |

## 4. Incident severity taxonomy (adapted from Module 6 for Ridgeline)

| Severity | Ridgeline-specific example | Response |
|---|---|---|
| SEV1 | Support assistant gives incorrect inventory-configuration guidance a customer acts on, causing a stockout | Immediate rollback to Q&A-only mode; exec + affected customer notified within 4 hours |
| SEV2 | Demand-forecast accuracy drops >15% for a customer segment, undetected for a week | Root-cause within 24 hours; affected customers notified of the correction |
| SEV3 | Anomaly-detection alert misses a rare fraud-pattern edge case affecting one customer | Logged, fixed on normal sprint cadence |
| SEV4 | Known limitation: forecasting accuracy lower for customers with <6 months of order history | Documented in product materials, no active fix required |

## 5. ROI and monitoring commitments

The support assistant's business case (per Module 7) projected $180,000/
year in reduced support headcount need against a $210,000 build cost and
$95,000/year run cost. The governance framework requires this case be
re-validated at the 90-day post-launch audit using actual deflection data,
not just the pre-launch projection — governance and ROI tracking share the
same review calendar deliberately, so neither happens in isolation from the
other.

## 6. Organizational ownership

Ridgeline's governance framework is owned by a two-person "CoE liaison"
function (per Module 9's smallest sizing tier, appropriate for 22 AI ICs) —
not a full Center of Excellence yet, but a named, accountable pair with the
explicit mandate: (1) run the intake/pre-launch/post-launch review cadence,
(2) maintain the system-of-record inventory, (3) own the incident severity
taxonomy and postmortem process. Explicitly out of scope: model
architecture decisions, pod tooling choices, and product roadmap — those
stay with the pods.

## How It Actually Works

This capstone's design — a two-person liaison function with three
explicitly bounded jobs, sitting at 22 AI ICs — is a direct application of
the sizing and mandate mechanics from Modules 5 and 9, worth naming
explicitly. At this headcount, no real evidence of cross-pod duplication
has yet accumulated (Module 5's threshold for full platformization sits
much higher), so a full CoE would be building process ahead of the
organizational scar tissue that would tell it what to build — which is
exactly the "platform built too early" failure mode. The three jobs
assigned here (review cadence, inventory, incident taxonomy) are
specifically the ones that don't require pod-level technical duplication to
justify — they're coordination functions whose value comes from being
singular regardless of org size, the same logic that put the
model/experiment registry first in Module 5's priority order.

Ridgeline's framework structure also demonstrates why review cadence,
inventory, and severity taxonomy have to be owned by the *same* function
rather than split across three: each depends on the others to mean
anything. A review cadence without an inventory has no reliable list of
what needs reviewing on schedule; an incident taxonomy without a review
process that already tiered each system has to re-derive risk severity
from scratch during an active incident, exactly the worst moment to do it;
and an inventory nobody keeps current from ongoing reviews decays back into
the "we don't have a complete list" failure mode Module 2 identifies as the
actual cause of most failed audits. The three functions form a single
feedback loop — reviews populate and refresh the inventory, the inventory
determines review cadence, and both together determine how fast an
incident can be correctly triaged — which is why bundling them under one
small, accountable pair works at this scale, while splitting them across
uncoordinated owners would silently break the loop the first time one part
drifted out of sync with the others.

## Stretch goals

- Draft the actual pre-launch review document for the support assistant's
  blocked human-review gap: what specific control (a confirmation step, a
  confidence threshold, a category-based routing rule) would unblock it,
  and how you'd verify it's working before re-approving launch.
- Extend the system-of-record inventory to include a fifth, EU-specific
  column mapping each system against the EU AI Act's risk tiers explicitly,
  given that Ridgeline is newly selling into the EU market.
- Build the 90-day post-launch audit template as a reusable document (not
  specific to the support assistant) that any future Ridgeline system would
  use, including the ROI re-validation step from section 5.
- Adapt this entire framework to your own organization: produce your own
  system-of-record inventory, run the intake checklist against your
  highest-risk live system, and write the one governance gap you'd flag as
  blocking if you applied this process honestly today.
