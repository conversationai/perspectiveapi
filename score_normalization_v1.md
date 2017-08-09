# Perspective API score normalization change

On **Tuesday, 2017-06-13**, Perspective will begin to return /normalized/ scores
by default. With this change, the score values from **all** of our models will
shift. See [What's changing and why?](#whats-changing-and-why) for details on
the change.

You **need to take action** if you use specific thresholds in your application
(for example, holding high-scoring comments for human moderation, auto-approving
low-scoring comments, or color-coding comments based on score).

You **don't** need to take action if you only use the scores to sort or rank
comments, though you may want to notify your users that the score values are
changing.


## When is it happening?

We plan to change our models to return normalized scores by default on
**Tuesday, 2017-06-13** around 1pm EDT, (10am PDT, 5pm UTC).

We will send a message to
[perspective-announce](http://groups.google.com/forum/#!forum/perspective-announce)
once the rollout is complete.


## What should I do?

To avoid using out-of-date score thresholds in your application, you can:
* Consult the [score mappings](#score-mappings) to update your thresholds.
* Configure your application for a
  [controlled migration](#i-want-to-control-when-i-migrate).


## What's changing and why?

Our normalization process applies a version of [probability
calibration](http://scikit-learn.org/stable/modules/calibration.html) to make
the scores approximate probabilities. For example, so that a toxicity score of
**0.80** can be interpreted as a belief that **80%** of people would consider
the comment to be toxic.

### Benefits of score normalization with probability calibration

Score normalization has a number of benefits:

* **Interpretability**: When using probability calibration specfically, the
  calibrated scores can be intepreted as probabilities. Currently, our models
  return scores between 0 and 1, *but* they aren't all properly calibrated as
  probabilities. For example, while a score of 0.4 indicates a higher confidence
  than a score of 0.2, a non-normalized 0.4 **doesn't** necessarily mean that
  the model thinks the comment is more likely to be non-toxic than toxic,
  despite 0.4 being less than the 0.5 (50%) mark. Probability calibration
  improves interpretability in this regard.
* **Consistency over time**: "Raw" scores can shift as we change the underlying
  models or training datasets. This is problematic for usecases involving *score
  thresholds*: the same score threshold can result in a different
  precision/recall performance for a new version of a model. Applying a
  normalization process to updated models minimizes this disruption.
* **Consistency across models**: With non-normalized scores, score ranges for
  different models can have very different *characteristics*. Users would need
  to evaluate each models' behavior to get a "feel" for what constitutes a high
  or low score. Normalization should make all our models' score ranges more
  consistent with each other.

Once the migration to normalized scores is complete, future model updates should
be less disruptive, models will be more consistent across the API, and the score
values can be more accurately interpreted as probabilites.

### Implementation details

We are
using [isotonic regression](https://en.wikipedia.org/wiki/Isotonic_regression)
for probability calibration. The data used for computing the regression is a
50/50 class-balanced subset of the test set.

The class balance of the dataset used for calibration can greatly affect the
calibration results. As a dataset changes over time, its class balance can also
vary. Different datasets can also have very different class balances. In order
to achieve our goal of consistency over time and across models, we chose to use
a stable class balance in computing the calibration.

Why a 50/50 balance? In machine learning, datasets used for training should
match the real world distribution as closely as possible, and the same holds for
calibration data. For example, if obscenity in comments is actually very rare,
using a calibration dataset with a 50/50 balance will result in elevated scores.
Because we're aiming to build generally useful models, we don't *know* the real
world distribution. So, an even 50% balance is a natural choice. We have also
found that a 50/50 balance of data tends to result in the full 0 to 1 range
being meaningful.


## I want to control when I migrate

You can control when you migrate to normalized scores by requesting **versioned
model attribute names**. Using this method, you can atomically update your
application to use updated thresholds and receive normalized scores.

A controlled migration process would be:
1.  Configure your application to use versioned, non-normalized attribute names.
2.  After the rollout on 2017-06-13, re-configure your application to use
    unversioned, normalized attribute names along with updating your score
    thresholds, according to the [score mappings](#score-mappings).

Use the following versioned attribute names for the non-normalized scores:
* TOXICITY@2
* LIKELY\_TO\_REJECT@1
* ATTACK\_ON\_AUTHOR@1
* ATTACK\_ON\_COMMENTER@1
* INCOHERENT@1
* INFLAMMATORY@1
* OBSCENE@1
* OFF_TOPIC@1
* SPAM@1
* UNSUBSTANTIAL@1

Notes:

* When you request a versioned attribute, the attribute names in the [response
  object]
  (https://github.com/conversationai/perspectiveapi/blob/master/api_reference.md#analyzecomment-response)
  will also include the version (e.g., you'll get scores for `TOXICITY@2`
  instead of just `TOXICITY`). This allows you request multiple versions of the
  same attribute. However, most users will probably want to remove this version
  specification from the attribute name (for example, by using a regex to remove
  `@.*` from the attribute name).
* If you want to migrate to normalized scores now, you can do so by using the
  next version of the attributes listed above: `TOXICITY@3`, and the `..@2` for
  the rest.
* We plan to **remove** the versioned attributes for the non-normalized scores
  on Tuesday, 2017-07-11, so please plan to complete your migration by then.


## Score mappings

These tables show how the score values are changing. You can use these tables to
update your score thresholds. For example, if your moderation interface
currently uses a red border for comments with TOXICITY score > 0.50, you would
change that threshold to be ~0.71 instead.

### TOXICITY

non-normalized | normalized
-------------- | ----------
0.00 | 0.00
0.05 | 0.01
0.10 | 0.03
0.15 | 0.09
0.20 | 0.13
0.25 | 0.27
0.30 | 0.34
0.35 | 0.44
0.40 | 0.63
0.45 | 0.66
0.50 | 0.71
0.55 | 0.83
0.60 | 0.87
0.65 | 0.87
0.70 | 0.92
0.75 | 0.95
0.80 | 0.97
0.85 | 0.98
0.90 | 1.00
0.95 | 1.00
1.00 | 1.00

### LIKELY\_TO\_REJECT

non-normalized | normalized
-------------- | ----------
0.00 | 0.00
0.05 | 0.25
0.10 | 0.41
0.15 | 0.53
0.20 | 0.59
0.25 | 0.65
0.30 | 0.70
0.35 | 0.74
0.40 | 0.77
0.45 | 0.81
0.50 | 0.83
0.55 | 0.86
0.60 | 0.88
0.65 | 0.89
0.70 | 0.92
0.75 | 0.92
0.80 | 0.95
0.85 | 0.97
0.90 | 0.97
0.95 | 0.98
1.00 | 1.00


### ATTACK\_ON\_COMMENTER

non-normalized | normalized
-------------- | ----------
0.00 | 0.00
0.05 | 0.04
0.10 | 0.08
0.15 | 0.11
0.20 | 0.14
0.25 | 0.17
0.30 | 0.20
0.35 | 0.24
0.40 | 0.26
0.45 | 0.28
0.50 | 0.30
0.55 | 0.34
0.60 | 0.38
0.65 | 0.46
0.70 | 0.59
0.75 | 0.61
0.80 | 0.68
0.85 | 0.73
0.90 | 0.79
0.95 | 0.91
1.00 | 0.97


### ATTACK\_ON\_AUTHOR

non-normalized | normalized
-------------- | ----------
0.00 | 0.00
0.05 | 0.02
0.10 | 0.03
0.15 | 0.04
0.20 | 0.05
0.25 | 0.05
0.30 | 0.06
0.35 | 0.07
0.40 | 0.09
0.45 | 0.10
0.50 | 0.12
0.55 | 0.14
0.60 | 0.17
0.65 | 0.20
0.70 | 0.23
0.75 | 0.29
0.80 | 0.36
0.85 | 0.43
0.90 | 0.54
0.95 | 0.65
1.00 | 0.99


### INCOHERENT

non-normalized | normalized
-------------- | ----------
0.00 | 0.00
0.05 | 0.13
0.10 | 0.20
0.15 | 0.26
0.20 | 0.31
0.25 | 0.35
0.30 | 0.39
0.35 | 0.43
0.40 | 0.44
0.45 | 0.46
0.50 | 0.47
0.55 | 0.49
0.60 | 0.51
0.65 | 0.53
0.70 | 0.56
0.75 | 0.60
0.80 | 0.65
0.85 | 0.69
0.90 | 0.75
0.95 | 0.83
1.00 | 1.00


### INFLAMMATORY

non-normalized | normalized
-------------- | ----------
0.00 | 0.00
0.05 | 0.08
0.10 | 0.11
0.15 | 0.13
0.20 | 0.15
0.25 | 0.18
0.30 | 0.19
0.35 | 0.21
0.40 | 0.25
0.45 | 0.27
0.50 | 0.29
0.55 | 0.33
0.60 | 0.37
0.65 | 0.41
0.70 | 0.44
0.75 | 0.47
0.80 | 0.55
0.85 | 0.61
0.90 | 0.66
0.95 | 0.74
1.00 | 0.96


### OBSCENE

non-normalized | normalized
-------------- | ----------
0.00 | 0.00
0.05 | 0.02
0.10 | 0.03
0.15 | 0.03
0.20 | 0.04
0.25 | 0.05
0.30 | 0.05
0.35 | 0.06
0.40 | 0.07
0.45 | 0.08
0.50 | 0.10
0.55 | 0.12
0.60 | 0.14
0.65 | 0.18
0.70 | 0.23
0.75 | 0.32
0.80 | 0.46
0.85 | 0.66
0.90 | 0.94
0.95 | 0.99
1.00 | 1.00


### OFF_TOPIC

non-normalized | normalized
-------------- | ----------
0.00 | 0.00
0.05 | 0.10
0.10 | 0.26
0.15 | 0.30
0.20 | 0.35
0.25 | 0.40
0.30 | 0.42
0.35 | 0.44
0.40 | 0.47
0.45 | 0.49
0.50 | 0.49
0.55 | 0.52
0.60 | 0.54
0.65 | 0.57
0.70 | 0.59
0.75 | 0.59
0.80 | 0.60
0.85 | 0.61
0.90 | 0.62
0.95 | 0.67
1.00 | 0.82


### SPAM

non-normalized | normalized
-------------- | ----------
0.00 | 0.00
0.05 | 0.01
0.10 | 0.01
0.15 | 0.02
0.20 | 0.02
0.25 | 0.03
0.30 | 0.04
0.35 | 0.04
0.40 | 0.05
0.45 | 0.06
0.50 | 0.07
0.55 | 0.08
0.60 | 0.10
0.65 | 0.12
0.70 | 0.15
0.75 | 0.19
0.80 | 0.25
0.85 | 0.34
0.90 | 0.46
0.95 | 0.67
1.00 | 1.00


### UNSUBSTANTIAL

non-normalized | normalized
-------------- | ----------
0.00 | 0.00
0.05 | 0.18
0.10 | 0.38
0.15 | 0.46
0.20 | 0.54
0.25 | 0.59
0.30 | 0.61
0.35 | 0.64
0.40 | 0.68
0.45 | 0.69
0.50 | 0.73
0.55 | 0.73
0.60 | 0.75
0.65 | 0.76
0.70 | 0.78
0.75 | 0.80
0.80 | 0.83
0.85 | 0.83
0.90 | 0.86
0.95 | 0.89
1.00 | 0.99
