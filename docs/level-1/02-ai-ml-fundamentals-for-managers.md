# 02 · AI/ML Fundamentals for Managers

You don't need to write a line of Python to manage AI work well, but you do
need enough of a mental model to ask sharp questions, catch an unrealistic
timeline, and tell the difference between "the model needs more data" and
"the model needs a different approach entirely." This module builds that
mental model from the ground up, entirely in plain language, using the
vocabulary your data science and ML teams actually use in meetings.

## 1. The three flavors of "AI" you'll manage

"AI" is an umbrella term covering several genuinely different kinds of
systems, each with different cost, risk, and timeline profiles. Knowing
which one a given project actually is changes almost everything about how
you plan it.

| Category | What it is | Example | Typical build cost/time |
|---|---|---|---|
| **Classical machine learning** | Statistical models trained on structured, tabular data to predict a number or category | Predicting customer churn from account history | Weeks; often the cheapest and most reliable option |
| **Deep learning / computer vision / traditional NLP** | Neural networks trained on unstructured data (images, audio, text) for a narrow task | Detecting defects in product photos | Months; needs labeled data and specialized talent |
| **Large language models (LLMs) / GenAI** | Massive pre-trained models adapted via prompting, fine-tuning, or retrieval, for open-ended language tasks | A chatbot, a document summarizer, a coding assistant | Days to weeks to prototype, but much longer to make reliable enough for production |

The most common management mistake at this stage is treating all three as
interchangeable "AI projects" with the same estimation rules. An LLM demo
can look impressively finished in an afternoon and still be months away from
production-safe; a classical ML model can look unglamorous and ship reliably
in three weeks. Ask your team which category you're actually in before you
promise a date.

## 2. How a model actually gets built (the non-technical version)

Every AI/ML project, regardless of category, moves through the same broad
stages. You will hear these terms constantly — this is what each one means
and, critically, why it matters to you as the manager.

| Stage | What happens | What you need to watch for |
|---|---|---|
| **Data collection** | Gathering the raw examples the model will learn from | Is there *enough* data? Is it *representative* of the real-world cases you care about? |
| **Data labeling / preparation** | Cleaning, structuring, and (for supervised learning) attaching the "correct answer" to each example | Labeling is often the single most underestimated cost in a project plan |
| **Training / fine-tuning** | The model adjusts its internal parameters to get better at predicting the labeled examples | This is iterative — expect several rounds, not one |
| **Evaluation** | Measuring how well the model performs on data it hasn't seen before | The evaluation metric must reflect the business goal, not just be "whatever's easy to compute" |
| **Deployment** | Making the trained model available to real users or systems | Deployment infrastructure (serving, monitoring, rollback) is often a separate, non-trivial project |
| **Monitoring & retraining** | Watching the model's real-world performance and updating it as data or conditions change | Models degrade over time ("drift") — this is not optional maintenance, it's part of the product |

## 3. Key vocabulary, translated

Your team will use these terms constantly. You do not need to compute any of
them yourself, but you do need to understand what a data scientist means
when they report them to you.

| Term | Plain-language meaning | Why you should care |
|---|---|---|
| **Training data** | The examples the model learns from | Garbage in, garbage out — this is where most real-world failures originate |
| **Overfitting** | The model memorized the training examples instead of learning the general pattern | An overfit model looks great in testing and fails in production — a classic false-confidence trap |
| **Accuracy / precision / recall** | Different ways of scoring "how often is the model right," each emphasizing different kinds of mistakes | Ask which metric your team is optimizing for — "accuracy" alone is often the wrong one (see Module 2 of Level 2 for the deep dive) |
| **Inference** | Actually running the trained model to get a prediction, in production | This is the ongoing compute cost — distinct from the one-time training cost |
| **Fine-tuning** | Taking an existing, pre-trained model and further training it on your own data | Usually far cheaper than training a model from scratch — ask why "from scratch" is on the table if it is |
| **Hallucination** | An LLM generating plausible-sounding but false or fabricated content | A named, expected failure mode of LLMs — not a bug to be "fixed" away entirely, only mitigated (see Module 9) |
| **Model drift** | A deployed model's performance degrading over time as real-world data shifts away from training data | The reason "we shipped it, we're done" is never true for AI systems |

## Worked example

A fraud-detection team reports: "Our new model has 99.5% accuracy." A
manager unfamiliar with the fundamentals in this module might celebrate. A
manager who understands them asks the next question: "What percentage of
our transactions are actually fraudulent?" If the answer is 0.3%, a model
that *always* predicts "not fraud" would already score 99.7% accuracy — better
than the "impressive" 99.5% — while catching zero fraud. The right follow-up
questions are about **recall** (of all the real fraud cases, how many did we
catch?) and **precision** (of everything we flagged as fraud, how many
actually were?), not the headline accuracy number. This single question —
"what's the baseline, and is accuracy even the right metric?" — is one of
the highest-leverage habits an AI manager can build, and it costs nothing to
ask.

## How It Actually Works

The reason accuracy alone can be misleading isn't a communication problem —
it's a direct consequence of how models are actually scored during
training. Most classifiers are optimized against a loss function that
treats every example roughly equally, and accuracy is just "fraction of
examples scored correctly" computed the same way. When one class (fraud,
churn, defect) is rare, a model can drive that loss down almost entirely by
getting good at predicting the *majority* class, because that's where nearly
all the loss-reducing opportunity lives — there's very little training
signal pushing it to also nail the rare class, since getting the rare cases
wrong barely moves the average. This is precisely why the fraud model in
the worked example can plateau at "predict not-fraud" behavior: gradient
descent found a local minimum that happens to coincide with a degenerate,
useless strategy, and nothing in a plain accuracy metric penalizes that.
Precision and recall exist because they decompose the confusion matrix
(true/false positives and negatives) into two separate signals that a
majority-class shortcut can't simultaneously game — a model that always
predicts "not fraud" scores 0% recall on the fraud class no matter how high
its accuracy climbs, which is why asking for recall specifically closes off
the shortcut.

Overfitting has a similarly mechanical explanation: a model with enough
parameters (a deep network, a high-degree decision tree, an LLM being
fine-tuned on a small dataset) has enough capacity to essentially memorize
the training set's noise along with its real pattern, because nothing in the
optimization process distinguishes "signal" from "coincidental quirk of
these specific examples" — both reduce training loss identically. The only
way to detect this is to evaluate on data the optimization process never
saw, which is why "hold out a test set and never let training touch it" is
a hard rule, not a best practice: any leakage between train and test data
collapses the one signal (a gap between training performance and held-out
performance) that reveals memorization is happening. Model drift is the
production-time mirror of this: the real-world data distribution keeps
moving away from whatever distribution the model was validated against, so
a model that was honestly evaluated at launch degrades for reasons that have
nothing to do with a bug — the input distribution itself changed underneath
a fixed set of learned parameters.

## Exercise

Find (or imagine, based on a plausible scenario) a real metric your team or
organization has reported for an AI/ML system — an accuracy score, a "success
rate," a user-satisfaction number. Write down: (1) what category of AI/ML
system it is (classical ML, deep learning, or LLM/GenAI) using the table
above, (2) what the *baseline* would be if you did nothing or used the
simplest possible rule, and (3) two clarifying questions you would now ask
the team about how that metric was computed, based on the vocabulary in
section 3.
