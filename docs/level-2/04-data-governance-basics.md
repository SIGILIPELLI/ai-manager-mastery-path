# 04 · Data Governance Basics

Data governance has an image problem. To most engineering teams it sounds
like a committee that slows things down, and to most managers it sounds
like something legal handles. Both readings are wrong in the same way: they
treat governance as paperwork rather than as **a set of pre-made decisions
about who may do what with which data**.

Made in advance, those decisions cost a few hours and unblock a team. Made
during an incident — a regulator's question, a customer deletion request, a
model trained on data it shouldn't have touched — they cost weeks and are
made badly under pressure.

For AI work specifically, governance stops being optional the moment data
gets *copied into a model*. A row in a database can be deleted. A pattern
learned from that row is much harder to remove, and "we'll just retrain"
turns out to mean six weeks and a re-validation cycle.

## 1. The five questions governance answers

If your organisation can answer these five for a given dataset, it has
governance, whatever it calls the process. If it can't, it has a policy
document.

| Question | Concretely | Symptom when unanswered |
|---|---|---|
| **Who owns it?** | A named person who can approve access and is accountable for quality | Requests bounce between teams for weeks |
| **Who may use it, for what?** | Documented purposes; a route to request new ones | Everyone gets everything, or nobody gets anything |
| **Where did it come from?** | Source system, collection basis, transformations applied | Nobody can explain a number to an auditor |
| **How good is it?** | Agreed thresholds for completeness, freshness, accuracy | Silent model degradation |
| **How long may we keep it?** | Retention period and deletion mechanism per category | Data hoarding, and deletion requests that can't be honoured |

The **purpose** question is the one AI work breaks most often. Data
collected to deliver a service is not automatically data you may train a
model on — that is a different purpose, and in several jurisdictions it
requires a different legal basis. This is not a technicality; it is the
most common reason a finished model cannot ship.

## 2. Ownership: the two-role model

Governance fails when "the data team owns the data." They own the pipes,
not the decisions. Split ownership into two roles per data domain
(customer, transactions, support, HR) and name real people.

| Role | Who it is | Decides | Does not decide |
|---|---|---|---|
| **Data owner** | A business leader in the domain — e.g. VP Customer Support owns ticket data | Who may access it, for what purposes, how long it's retained, acceptable quality bar | Storage technology, pipeline design |
| **Data steward** | A hands-on person in or near that team | Definitions, quality checks, documentation, day-to-day access provisioning | Policy, purpose approval |

A one-page domain record is enough to start:

| Field | Example entry |
|---|---|
| Domain | Support tickets |
| Data owner | VP Customer Support (named) |
| Steward | Support Ops analyst (named) |
| Contains personal data? | Yes — names, emails, free-text describing accounts |
| Special categories? | Occasionally health references in free text — treat as sensitive |
| Approved purposes | Service delivery; internal analytics; **ML training on redacted text only** |
| Retention | 24 months, then delete; redacted derivatives 36 months |
| Quality bar | See section 4 |
| Last reviewed | Quarterly, date recorded |

Ten of these covers most mid-sized organisations. Producing them is a
two-week exercise, not a programme.

## 3. Access tiers

Binary access — you have it or you don't — pushes teams toward asking for
the maximum, because a second request is expensive. Tiers let people get
what they need quickly and reserve real scrutiny for real risk.

| Tier | Data | Typical approver | Turnaround target |
|---|---|---|---|
| **0 — Open** | Aggregated, anonymised, published internally | Self-serve | Immediate |
| **1 — Internal** | Business data, no personal identifiers | Steward | 1 day |
| **2 — Restricted** | Personal data, pseudonymised | Data owner | 3 days |
| **3 — Sensitive** | Direct identifiers, special categories, financial detail | Owner + privacy/legal | 10 days |

Two design rules matter more than the tier boundaries. **Default to the
lowest tier that answers the question** — most ML training does not need
direct identifiers, and a team that has never been asked will not
volunteer that. And **make tier 0 and 1 genuinely fast**, or the tiering
collapses back into "ask for everything at once."

## 4. Data quality as an SLA, not an aspiration

"Improve data quality" is unmanageable. Quality thresholds per dataset,
monitored, with a named owner, are manageable. Four dimensions cover the
overwhelming majority of ML failures.

| Dimension | Definition | Example threshold | Who is paged |
|---|---|---|---|
| **Completeness** | Share of records with all required fields | ≥98% of tickets have a category | Steward |
| **Freshness** | Age of the newest record when the pipeline runs | Under 6 hours | Data engineering |
| **Validity** | Share of values conforming to the expected type/range | ≥99.5% pass schema checks | Data engineering |
| **Consistency** | Agreement between systems that should match | Account counts within 0.5% of billing | Steward + owner |

The manager's contribution here is not setting the numbers — it is
insisting that the thresholds exist, are monitored automatically, and have
a named recipient for the alert. An unmonitored threshold is a wish.

## 5. Lineage — and why you should care

Lineage is the record of where a number came from: source system, every
transformation, every dataset it fed. It sounds like an engineering nicety
until one of these three moments arrives.

| Moment | Question you will be asked | Without lineage |
|---|---|---|
| Audit or regulator inquiry | "What data informed this decision?" | Weeks of archaeology, uncertain answer |
| Data incident | "Which models used the corrupted table?" | Retrain everything, or hope |
| Deletion request | "Prove this person's data is gone" | You cannot |

You don't need a lineage platform to start. You need the ML team to record,
for every model that reaches production, the datasets and versions it was
trained on. That single habit answers most of the second row and much of
the first.

## 6. Governance specific to AI training data

Four issues that ordinary data governance misses because it predates
model training.

| Issue | The question | A workable default |
|---|---|---|
| **Purpose creep** | Was this data collected for a use compatible with training? | Explicit "ML training" purpose flag per domain; absent = not approved |
| **Deletion propagation** | A customer asks for erasure — what happens to models trained on their data? | Delete from stores; document that models are retrained on a defined cycle; record the cycle length |
| **Third-party & synthetic data** | May we use scraped, licensed, or vendor-supplied data commercially? | Licence review before ingestion, not before launch |
| **Vendor data flows** | Does data sent to an external model provider get retained or trained on? | Contractual no-training / zero-retention terms, verified in writing |

The deletion-propagation row is where good-faith organisations get caught.
"We delete the row" is usually a defensible answer *if* you can also state
the retraining cycle. It becomes indefensible when nobody has ever thought
about it and the honest answer is "the model still contains it, forever."

## Worked example

A 400-person healthtech company built a triage model to prioritise inbound
patient messages. Six months of ML work, strong offline results, executive
enthusiasm. Launch was scheduled for a Monday. It slipped by seven months.

The privacy review, run late because governance was treated as a
pre-launch checkbox, produced three findings:

1. **Purpose.** The message data had been collected under a consent notice
   covering "providing and improving our services." Counsel judged model
   training arguably covered, but the free-text field routinely contained
   clinical detail — a special category requiring an explicit basis the
   company did not have.
2. **Retention.** Messages were retained indefinitely because no one had
   ever set a period. The training set included messages from patients who
   had closed their accounts three years earlier.
3. **Lineage.** Asked which training records came from which source system,
   the team could not answer. The dataset had been assembled by a departed
   contractor from a joined export.

Finding 3 was the expensive one. Without lineage, the company could not
selectively remove the affected records — it could not even identify them.
The training set had to be rebuilt from source under a corrected process,
and the model retrained and re-validated.

| Cost of the seven-month delay | Estimate |
|---|---|
| Rebuild dataset + retrain + re-validate | ~$180,000 (2.5 FTE, 5 months) |
| Legal and external privacy counsel | ~$60,000 |
| Deferred benefit (triage savings, 7 months) | ~$310,000 |
| **Total** | **~$550,000** |

The governance work that would have prevented all three findings was
scoped afterwards at roughly **six weeks of one steward's time plus two
half-day workshops** — call it $25,000. It produced: domain records for
four datasets, a retention schedule, an ML-training purpose flag, and a
rule that training datasets record their source tables.

The pattern is worth naming because it repeats everywhere: **governance
was not skipped, it was deferred** — and deferred governance is discovered
at the least reversible moment, when the model already exists. The
manager's actionable lesson is a sequencing one. The privacy and purpose
review belongs at the point the dataset is assembled, not at the point the
model is ready. It costs almost nothing at the start and it is the single
highest-leverage schedule change available to you.

## Exercise

Choose one dataset your team uses, or plans to use, for an AI project.

1. **Fill in the domain record** from section 2. Every blank you cannot
   fill without asking someone is a governance gap; list who you'd have to
   ask.
2. **Name the owner and steward** — actual people, not teams. If you cannot
   name an owner, that is the first thing to fix, and it is a
   fifteen-minute conversation, not a programme.
3. **Answer the purpose question explicitly.** Under what basis was this
   data collected, and does that basis cover model training? Write the
   answer down and get one person outside your team to agree with it.
4. **Set four quality thresholds** using section 4, and for each name who
   receives the alert when it's breached.
5. **Run the deletion test.** Ask: if a customer requested erasure today,
   what would happen to their data in our training sets and in models
   already deployed? Write down the actual current answer, not the
   aspirational one.
6. **Pick the one gap** from the above with the worst
   consequence-times-likelihood, and put a specific fix on next month's
   plan with a named owner.
