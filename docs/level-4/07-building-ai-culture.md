# 07 · Building AI Culture

Every framework in this program — governance checklists, portfolio
scoring, incident runbooks — only works if the organization's actual
day-to-day behavior matches what's written down. Culture is what happens
when nobody's checking: whether an engineer flags a concerning eval result
or quietly hopes it resolves itself, whether a product manager routes a
new AI feature through governance intake or skips it because the deadline
is tight. This module covers building the specific cultural conditions that
make the rest of this program actually stick, rather than becoming
documentation nobody follows under pressure.

## 1. The culture-practice gap diagnostic

Before investing in culture initiatives, diagnose where the actual gap is.
"We need better AI culture" is too vague to act on; these four questions
usually locate the real problem.

| Question | What a "yes" reveals |
|---|---|
| Do people report bad results (a failed experiment, a governance red flag) as readily as good ones? | Psychological safety around negative findings — the single highest-leverage culture indicator |
| Would a junior engineer feel comfortable escalating a senior engineer's skipped eval step? | Whether hierarchy suppresses safety-relevant dissent |
| Do teams under deadline pressure skip governance steps, and does anyone notice when they do? | Whether governance is a genuine practice or theater that collapses under pressure |
| Can someone describe a time leadership visibly changed a decision because of an AI risk finding? | Whether risk-flagging has ever actually mattered, or is treated as symbolic |

Run this as an honest internal survey or a set of structured interviews,
not a leadership self-assessment — leadership's view of the culture and
the actual lived experience of ICs are often meaningfully different, and
the gap itself is diagnostic.

## 2. Incentive alignment — the most underused lever

Culture statements ("we value responsible AI") change nothing if
performance reviews, promotions, and bonuses reward only shipped features
and not the practices that make shipping safe. Audit specifically:

| Incentive | Common misalignment | Fix |
|---|---|---|
| Performance review criteria | Rewards velocity/features shipped only | Add explicit criteria: quality of eval practice, governance compliance, honest reporting of failures |
| Promotion criteria | Promotes people who ship visible wins, not people who prevented invisible failures | Recognize and promote based on documented risk-catches and process improvements, not just launches |
| Team-level recognition | Public praise only for successful launches | Publicly recognize a team that killed a bad idea early or caught an incident before it escalated |
| Manager incentives | Managers rewarded purely on team output | Include team governance-compliance rate as a factor in manager evaluation |

The clearest tell of misalignment: if the engineer who quietly shipped a
feature by skipping the eval step gets promoted faster than the one who
delayed a launch two weeks to fix a bias-testing gap, no amount of stated
values will produce the behavior you actually want.

## 3. Leadership behaviors that set the real culture

Stated values are cheap; visible leadership behavior under real pressure is
what people actually calibrate to.

- **Publicly kill or delay something leadership wanted**, when a
  governance or quality finding warrants it — this is the single most
  powerful signal available, and it can't be faked or delegated.
  Employees remember the one time a launch was actually delayed for a
  finding far more than any number of "we take this seriously" statements.
- **Ask about failures in the same tone as successes** in leadership
  reviews and all-hands — if the CEO's questions are always "what did we
  ship" and never "what did we catch," that asymmetry propagates down
  every level of the organization within a quarter.
- **Model uncertainty honestly.** An executive who says "I don't know if
  this AI bet will pay off, here's how we'll find out" builds more trust
  than false confidence, and licenses the same honesty at every level
  below.

## 4. Structural culture supports

Behavior and incentives matter most, but a few structural supports make
the right behavior easier to sustain:

- **A no-blame incident process** (Level 3 Module 6) that people actually
  believe is no-blame, verified by whether people volunteer information
  proactively rather than only when caught.
- **Protected time for the "negative results first" practice** (Level 2
  Module 1's weekly experiment review) — a habit that only survives if it's
  actually protected from being the first thing cut under deadline pressure.
- **A visible, used escalation path** for AI risk concerns that bypasses
  the direct chain of command when needed — people need to trust it exists
  and won't cost them their standing to use, which requires it to have
  actually been used successfully at least once, visibly.

## Worked example

A consumer electronics company, Brightline Devices, had a well-documented
AI governance framework (built following Level 3 Module 2's template) that
looked strong on paper — checklists, review cadences, an incident process.
An internal culture survey, run at the new Chief AI Officer's request,
revealed a stark gap: 68% of ML engineers surveyed said they had, at some
point, skipped or rushed a governance review step to meet a deadline, and
only 12% said they would feel comfortable telling their manager they'd done
so.

Digging into why: the company's promotion cycle that year had promoted two
engineers specifically for shipping features ahead of schedule, in both
cases by compressing the governance review timeline — a fact senior
leadership hadn't connected to the survey results until the CAIO put both
findings side by side in a single presentation.

The response, over two quarters: promotion criteria were explicitly revised
to include governance-compliance history as a documented factor, reviewed
by the same committee; and the CAIO publicly delayed a high-visibility
product launch by three weeks after a late-stage bias-testing gap was
found, explicitly citing the incident in the next company all-hands as an
example of the process working as intended rather than a failure to hide.
A follow-up survey two quarters later showed the "comfortable escalating a
skipped step" figure had risen from 12% to 41% — still imperfect, but a
concrete, measured sign that the incentive change plus the visible
leadership action were shifting real behavior, not just restating values.

## Exercise

Take your own organization (or Brightline Devices, pre-survey).

1. **Run the four-question diagnostic** in section 1, as honestly as you
   can, ideally by actually asking a few ICs rather than answering from a
   leadership perspective alone.
2. **Audit one incentive** from section 2 (performance review, promotion,
   or recognition) for the specific misalignment described, and write the
   one concrete change you'd propose.
3. **Name one real, specific instance** (or design a plausible near-term
   one) where leadership could visibly delay or kill something for a
   governance or quality reason — per section 3, this needs to be
   concrete and public, not a general statement of values.
