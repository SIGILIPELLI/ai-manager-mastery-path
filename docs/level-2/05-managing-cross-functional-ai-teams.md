# 05 · Managing Cross-Functional AI Teams

An AI initiative of any consequence needs at least five functions: data
science, engineering, product, legal or compliance, and design. They run on
different clocks, are measured on different things, and — critically —
disagree about what "done" means. Data science is done when a metric clears
a bar. Engineering is done when it survives production. Legal is done when
the risk is documented and accepted. Design is done when a person can use
it without being misled.

None of these is wrong. The failure is treating them as one team with one
definition of done, and discovering the mismatch at integration time.

Your job is not to make everyone agree. It is to make the disagreements
happen **early, in a named forum, with a named decider** — instead of late,
in a Slack thread, with everyone assuming someone else decided.

## 1. The five parties and what each is really optimising

| Function | Optimising for | Their nightmare | Their clock |
|---|---|---|---|
| **Data science / ML** | Model quality on a defined metric | Shipping something that doesn't work and being blamed for it | Weeks per experiment; irregular |
| **Engineering / platform** | Reliability, latency, maintainability | Being handed a notebook and told to productionise it by Friday | Sprints; predictable |
| **Product** | User outcome and business metric | Building something correct that nobody uses | Roadmap quarters |
| **Legal / compliance / privacy** | Defensibility; no unacceptable exposure | Finding out after launch | Reactive; slow when surprised, fast when warned |
| **Design / UX** | Comprehensible, appropriately trusted experience | A confident-sounding system that misleads users | Ahead of build |

Read the "nightmare" column twice. Most cross-functional friction is one
party trying to avoid its nightmare in a way that creates another's. Legal
delays because it was surprised; engineering resists because it inherits
unmaintainable work; data science over-researches because shipping a weak
model is the failure it's punished for. Address the fear and the behaviour
usually changes without a process fix.

## 2. Decision rights: the matrix worth writing down

Ambiguous decision rights cost more time on AI projects than on ordinary
software, because more decisions sit genuinely between functions. Write
this once, at kickoff, and revisit it only when something breaks.

**A** = accountable, single owner and final call · **C** = must be
consulted before deciding · **I** = informed after

| Decision | DS/ML | Eng | Product | Legal | Design | AI Manager |
|---|---|---|---|---|---|---|
| What problem we're solving | C | I | **A** | I | C | C |
| Whether the data may be used | C | I | C | **A** | I | C |
| Model approach and architecture | **A** | C | I | I | I | I |
| Precision/recall operating point | C | I | C | C | C | **A** |
| Whether quality is good enough to ship | C | C | C | C | C | **A** |
| How the output is shown to users | I | C | C | C | **A** | I |
| Production readiness (deploy/no-deploy) | C | **A** | I | I | I | C |
| Go-live date | C | C | **A** | C | I | C |
| Rollback in an incident | C | **A** | I | I | I | I |
| Accepting residual risk | C | I | C | **A** | I | C |

Three rows deserve comment, because they are the ones most often assigned
wrongly.

- **The operating point is yours.** As Module 02 established, where to sit
  on the precision/recall trade-off is a business judgement about the
  relative cost of misses and false alarms. Delegating it to ML is
  delegating a business decision to people who were never given the cost
  numbers.
- **"Good enough to ship" is also yours**, and it must be decided against a
  bar written *before* the results arrived. Otherwise the bar becomes
  whatever the model achieved.
- **Production readiness belongs to engineering, and it is a veto.** If
  engineering says the system cannot be operated safely, that is not a
  negotiation with the launch date.

## 3. The handoffs where AI projects die

Four seams. Each has a cheap, specific fix.

| Handoff | What goes wrong | The fix |
|---|---|---|
| Problem → hypothesis | Product asks for "an AI feature"; ML builds a technically sound answer to an unasked question | A written problem statement with the business metric, signed by product and ML before work starts |
| Data → model | Model trained on a hand-assembled extract nobody can reproduce | Training data comes from a pipeline, versioned, from day one — never from a one-off export |
| Model → production | A notebook is thrown over the wall; engineering rebuilds it, behaviour changes | Engineering sits in the experiment review from week one and owns the serving path from the first shadow deploy |
| Production → users | Users don't trust it, or trust it far too much | Design involved before the model is finished, not after; the interface expresses uncertainty |

The model→production seam is the expensive one. The usual pattern —
research to a notebook, then hand off — reliably produces a rewrite plus a
behaviour discrepancy nobody can explain. Having engineering present from
the first experiment review costs a couple of hours a week and removes an
entire failure class.

## 4. Cadence design

Meetings are the mechanism you have. Design them deliberately: too few and
the seams fail silently; too many and the specialists stop doing the work.

| Forum | Frequency | Who | Purpose | Timebox |
|---|---|---|---|---|
| Experiment review | Weekly | ML, eng, product, you | Results, decisions, queue re-ranking (Module 01) | 45 min |
| Integration sync | Weekly | ML + eng leads | Serving path, feature parity, skew | 30 min |
| Risk & compliance check-in | Biweekly | Legal, privacy, you | Surface issues early; no surprises | 30 min |
| Design review | At milestones | Design, product, ML | How outputs and uncertainty are presented | 60 min |
| Steering / stakeholder update | Monthly | Sponsor, function leads | Business metric, risks, decisions needed | 45 min |

The biweekly compliance check-in is the highest-return item on this list
and the one most often skipped. Legal is slow when surprised and fast when
pre-briefed. Thirty minutes a fortnight converts a launch-blocking review
into a series of small, already-anticipated confirmations.

## 5. Translating between functions

A large share of your value is translation. The same fact, phrased for each
audience:

| Fact | For engineering | For legal | For the sponsor |
|---|---|---|---|
| Model is 78% precise at 60% recall | 40% of flagged items are false positives; the review queue needs capacity for ~1,200/week | The system errs toward over-flagging; every action is human-reviewed before it affects a customer | We'll catch 3 in 5 cases; 2 in 5 reviews will be unnecessary — net saving of about $40k a month |
| We can't fully explain individual predictions | Feature attributions available, not causal | We can produce contributing factors per decision, plus a documented appeal route | We can always explain the general logic and give a person a specific reason on request |
| The model will degrade over time | Drift monitoring plus a retrain trigger | Performance is monitored continuously with a documented intervention threshold | It's a system we operate, not a project we finish — hence the ongoing run cost |

Notice that none of these is a simplification that loses the truth. That is
the standard: if a translation would embarrass you when the audience later
learns the detail, it was spin, not translation.

## Worked example

An insurance company built a claims-triage model to route incoming claims
into fast-track, standard, and investigate. Eight people across five
functions, four months in, and the project was two months late with no
launch date.

The manager's diagnosis, from one week of listening:

- **ML** had optimised overall routing accuracy and was proud of 84%. Nobody
  had told them that a misrouted fraud case cost roughly 60 times what a
  misrouted routine claim did, so the metric they optimised was the wrong
  one.
- **Engineering** had learned about the project six weeks earlier and had
  found that three of the model's features were computed from a batch
  warehouse table unavailable at claim intake. A quarter of the model could
  not be served at all.
- **Legal** had not been engaged. In this jurisdiction, adverse automated
  decisions on insurance claims required an explanation and an appeal path.
- **Design** had produced screens showing a confidence percentage next to
  each routing recommendation. User testing found adjusters treated 71% as
  "the system is fairly sure" and stopped checking — the opposite of the
  intended effect.
- **Product** had promised a launch date to the COO based on the ML team's
  "model's basically done."

Every function had done competent work. The project was still failing,
because nothing forced these four facts into the same room.

What she changed, over three weeks:

1. **Wrote the decision-rights matrix** in section 2 and walked it through
   with all five leads in a single 90-minute session. The operating-point
   row alone triggered the cost conversation that reset the metric: with
   fraud misroutes priced at 60× routine ones, the optimal threshold was
   far more conservative on the investigate class, and overall accuracy
   *fell* to 79% while expected cost dropped sharply.
2. **Moved engineering into the weekly experiment review.** The feature
   availability problem would have surfaced in week two rather than week
   eighteen. Three features were dropped; the retrained model lost about
   two points and became servable.
3. **Started the biweekly compliance check-in.** Legal's requirement turned
   out to be satisfiable: a reason code per decision plus a documented
   human-review route. Six weeks of work, but known six weeks earlier.
4. **Sent design back** with a specific brief: express uncertainty without
   a number that reads as authority. The revised screen showed the two most
   relevant policy factors and a plain "review recommended" flag. Adjuster
   override rates rose to a healthy 18% from 4%.
5. **Retracted the launch date** and replaced it with two gates: legal
   sign-off, and a two-week shadow deploy showing production quality within
   two points of offline.

It launched eleven weeks later. The instructive part is that nothing was
solved by better modelling. Four of the five fixes were forums and decision
rights — the cheapest interventions available to a manager, and the ones
that only work if applied before the seams fail.

## Exercise

Take a current cross-functional AI initiative, or design one for a
plausible project.

1. **Fill in the decision-rights matrix** from section 2 for your project.
   Then — this is the actual exercise — send it to each function lead and
   ask them to mark any row where they disagree with the accountable
   party. Every disagreement you find is a late-stage conflict you just
   avoided.
2. **Identify which of the four handoffs** in section 3 is currently
   weakest on your project, and write down the specific evidence that led
   you to pick it.
3. **Audit your cadence** against section 4. Note which forums exist, which
   are missing, and — separately — which exist but are attended by the
   wrong people.
4. **Write one translation.** Take a real technical fact about your system
   and write the engineering, legal, and sponsor versions. Check each
   against the embarrassment test in section 5.
5. **Name your one veto-holder.** Who on your project can say "not ready"
   and have it stick? If nobody can, that is the finding.
