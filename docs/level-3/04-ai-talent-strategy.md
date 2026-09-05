# 04 · AI Talent Strategy

AI talent is expensive, scarce, and unusually mobile — a strong ML engineer
gets recruiter messages weekly, and the skills that make someone good at
research are not the same skills that make someone good at shipping
production systems. Treating "AI hiring" as one undifferentiated pipeline is
the single most common strategic mistake at this level. This module gives
you a framework for defining the roles you actually need, structuring
career ladders that retain senior talent, and building a hiring process
that filters for the right thing.

## 1. The AI role taxonomy

Job titles in this space are inconsistent across companies. Anchor your
hiring and org design to what the role actually does, not the title a
candidate's resume uses.

| Role | Core skill | Where they add value | Common mis-hire |
|---|---|---|---|
| Research scientist | Novel modeling, published or publishable work | Genuinely new capability, competitive differentiation | Hired for a role that's really "apply an existing off-the-shelf model" |
| Applied ML engineer | Adapting known techniques to your data and product | Most day-to-day model-building work | Expected to also do research-level innovation on a production timeline |
| ML/MLOps engineer | Production infrastructure, deployment, monitoring | Making models reliable and observable in production | Treated as "just DevOps," under-involved in model design decisions |
| Data engineer | Pipeline reliability, data quality at scale | The unglamorous 60% of most AI projects' actual effort | Understaffed relative to ML headcount, becomes the bottleneck |
| AI/LLM product engineer | Prompt engineering, eval design, product integration | GenAI features specifically — a distinct skill from classical ML | Assumed to be interchangeable with a general software engineer |

A useful diagnostic: if your team is struggling to ship and the honest
answer is "we don't have enough research talent," you likely have the
titles right but the ratio wrong — most orgs need far more applied/MLOps/
data engineering capacity than research capacity.

## 2. Career ladders that actually retain senior ICs

The single biggest driver of senior ML talent attrition is a career ladder
that forces a choice between "stay technical" and "get promoted," because
the only visible path upward is management. Build a real dual-track ladder.

| Level | IC track title | Manager track title | What distinguishes this level (IC) |
|---|---|---|---|
| Mid | ML Engineer II | — | Owns a model or feature end-to-end with review |
| Senior | Senior ML Engineer | Eng Manager | Sets technical direction for a project; mentors 2-3 others |
| Staff | Staff ML Engineer | Senior Eng Manager | Sets technical direction across a pod; decisions with org-wide cost/risk implications |
| Principal | Principal ML Engineer / Distinguished Engineer | Director of AI | Technical authority spanning multiple pods; often the person a VP calls before a big bet |

The IC track must have real compensation and real authority parity with the
equivalent management level — if a Staff engineer earns less and has less
influence over roadmap than an Engineering Manager two levels below them in
tenure, your best technical people will eventually take a management job
they don't actually want, or leave.

## 3. Hiring process design for AI roles

Generic engineering interview loops under-select for AI-specific judgment.
Build in at least one signal for each of these, calibrated to the role:

| Signal | What it tests | How to test it without a take-home that burns a candidate's weekend |
|---|---|---|
| Problem framing | Can they turn a vague business ask into a falsifiable experiment? | Live case: "Marketing wants an AI tool that reduces churn — walk me through your first two weeks" |
| Statistical/eval judgment | Do they know when a result is real vs. noise or leakage? | Present a flawed eval setup, ask them to find the flaw |
| Production judgment (for applied/MLOps roles) | Do they think about failure modes, monitoring, rollback? | "This model just started giving worse recommendations in production — walk me through your first hour" |
| Communication to non-technical stakeholders | Can they explain a limitation without jargon or false confidence? | Ask them to explain a model's confidence interval to a simulated VP |

Skip generic LeetCode-style algorithm rounds for senior applied/research
roles unless the actual job involves that kind of work daily — they select
for a skill that correlates poorly with AI-specific job performance and
signal to strong candidates that you don't understand the role.

## 4. Retention levers beyond compensation

Compensation matters, but for AI talent specifically, three non-comp levers
show up repeatedly in exit interviews as decisive:

- **Compute and tooling access.** A senior researcher blocked by GPU quota
  or slow experiment infrastructure will look elsewhere faster than one
  underpaid but well-resourced.
- **Publication/external visibility policy.** Even applied engineers often
  care about conference talks, blog posts, or open-source contributions as
  part of their professional identity and market value. A blanket "no
  external communication" policy is a quiet but real retention cost.
- **Problem quality.** The best AI talent explicitly optimizes for working
  on hard, real problems over marginal comp increases — a common regret cited
  by managers who lose senior people is discovering, too late, that the
  person had been quietly assigned to maintenance work for two quarters.

## Worked example

A logistics company, Cartway Freight, was losing senior ML engineers at
roughly twice the rate of its broader engineering org — three departures in
five months from a 14-person team. Exit interviews all mentioned some
version of "no path forward except becoming a manager, and I don't want
that."

The VP of Engineering audited the ladder and found the informal reality:
the only titles above "ML Engineer" were "Engineering Manager" and
"Senior Engineering Manager." Two of the three departed engineers had been
doing clearly staff-level technical leadership (setting the eval standard
now used org-wide, leading the migration to a new feature store) with
neither the title nor the compensation band to reflect it.

The fix, over one quarter: introduced Staff and Principal IC titles with
compensation bands benchmarked at parity with the equivalent management
levels, and retroactively promoted two current ICs into the new levels
based on work already done. Additionally, the compute-provisioning process
— previously a two-week ticket queue — was rebuilt into a self-service
system with a manager-approved quota, cutting median wait time from 9 days
to same-day for requests within quota. Attrition on the team dropped to
zero over the following three quarters, and in the next round of exit
interviews across the broader org, two engineers cited the Cartway ML
team's new ladder as a reason they'd asked to transfer in rather than out.

## How It Actually Works

The forced-choice-into-management pattern at Cartway has a specific
structural cause worth naming: when only one axis of a job ladder (the
management track) carries both the compensation increases and the title
that signals seniority externally, every other form of value someone
creates — setting an eval standard the whole org now depends on, leading a
migration that changes what every pod builds on — has no ladder rung to
register on. That value is real and the org is visibly using it, but
because the level system has no vocabulary for it, it accumulates as
informal reputation rather than as anything that shows up in comp
benchmarking, external recruiting conversations, or the person's own
sense of whether they're progressing. A recruiter's outbound message
naming a concrete "Staff Engineer, $X" offer directly compares against
what the person actually has, while their org's informal "you're clearly
one of our best" has nothing to compare against — which is why the
departures were specifically the two people doing staff-level work without
a staff-level rung to stand on, not a random sample of the team.

The compute-quota fix reveals a related mechanism: for research and applied
ML work specifically, the rate at which someone can learn whether an idea
works is bottlenecked by how fast they can run an experiment, so a
two-week ticket queue doesn't just slow down one task, it compounds against
every subsequent decision that experiment's result would have informed —
each blocked experiment delays the next hypothesis in the queue behind it
(the same sequential dependency Module 01 of Level 2 covers for
experimentation cadence generally). A senior researcher's actual
productivity is throttled by that queue in a way salary cannot compensate
for, because no amount of pay increases the number of experiments they can
run per week — which is exactly why "blocked by GPU quota" surfaces in exit
interviews as decisive even for people who were not underpaid: the
constraint binds on a different resource than money can buy back.

## Exercise

Take your own AI org (or Cartway Freight, above, pre-fix).

1. **Map your current headcount** against the role taxonomy in section 1.
   Where is your actual mix skewed relative to what the work requires
   (e.g., too much research capacity relative to data engineering)?
2. **Audit your ladder** against section 2. Is there a real IC path to
   Staff/Principal with comp parity to the equivalent manager level, or is
   management the only visible path up?
3. **Pick one open or recent senior AI req** and redesign the interview loop
   using the four signals in section 3. Name specifically what you'd cut
   from the current loop and what you'd add.
