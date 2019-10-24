# Perspective API score normalization: fixes for Toxicity

On **Wednesday, 2017-08-23**, we updated the scores for the TOXICITY model
in the Perspective API. All other models are not affected.

**You may need to take action** if you use specific thresholds for the Toxicity
model in your application (for example, holding high-scoring comments for human
moderation, auto-approving low-scoring comments, or color-coding comments based
on score), and you want to ensure that the threshold is unchanged.

You **don't** need to take action if you only use the scores to sort or rank
comments, though you may want to notify your users that the score values are
changing.


## When is it happening?

We updated the Toxicity scores on **Wednesday, 2017-08-23**. We will send a message to
[perspective-announce](http://groups.google.com/forum/#!forum/perspective-announce)
once the rollout is complete.


## What should I do?

To avoid using out-of-date score thresholds for Toxicity in your application,
you can:
* Consult the [toxicity score mappings](#score-mappings) below to update your
  thresholds.
* Configure your application for a
  [controlled migration](#i-want-to-control-when-i-migrate).


## What's changing and why?

TL;DR: The latest calibration gives less extreme scores than the previous
calibration - it increases the scores that used to fall in the low end of the
score range, and lowers the scores at the highest end.

Our normalization process applies a version of [probability
calibration](http://scikit-learn.org/stable/modules/calibration.html) to make
the scores approximate probabilities. For example, so that a toxicity score of
**0.80** can be interpreted as a belief that **80%** of people would consider
the comment to be toxic.

And yeah, sorry we're doing this again. Our first attempt at doing this wasn't
quite right for the case when we have many annotations per example. Given we
have the distribution of crowd-worker ratings for the Toxicity model, we
realised we should be calibrating directly on those (we were initially,
accidentally, calibrating on the judgement of > 50% of participants rating the
example toxic - subtle, but a little different!). For other models based on the
NYT annotations, our callibration was already correct because there was only a
single decision, not a distribution of them.


## I want to control when I migrate

You can control when you migrate to normalized scores by requesting **versioned
model names**.

If you want to migrate to fixed normalized scores now, you can do so by using
the next version of the model listed above: `TOXICITY@4`.

A controlled migration process for moving to new normalized score later
involves:
1.  Configure your application to use a versioned model name before the
    rollout.
    * Request `TOXICITY@3` for the current default model (you are currently
    using `TOXICITY@3` if you just request `TOXICITY`). This was our first
    attempt at calibration.
2.  Within 3 months after the rollout (by 2017-11-15), re-configure your
    application to use the unversioned model name (`TOXICITY`), along with
    updating your score thresholds, according to the [score
    mappings below](#score-mappings).

Notes:

* When you request a versioned model, the model names in the [response
  object](https://github.com/conversationai/perspectiveapi/blob/master/api_reference.md#analyzecomment-response)
  will also include the version (e.g., if you request `TOXICITY@3` you'll get
  scores for `TOXICITY@3` instead of just `TOXICITY`). This allows you to
  request multiple versions of the same model. However, most users will probably
  want to remove this version specification from the model name (for
  example, by using a regex to remove `@.*` from the model name).


## Score mappings

These tables show how the score values are changing. You can use these tables to
update your score thresholds. For example, if your moderation interface
currently uses a red border for comments with TOXICITY score > 0.85, you would
change that threshold to be ~0.78 instead.


### TOXICITY

The following tables can be used to help identify how you want to change any
thresholds associated with the TOXICITY models.


| TOXICITY@3         | TOXICITY@4         |
| ------------------ | ------------------ |
| kinda normalized   | better normalized  |
| (until 2017-08-15) | (after 2017-08-15) |
| 0.00 | 0.00 |
| 0.05 | 0.28 |
| 0.10 | 0.37 |
| 0.15 | 0.39 |
| 0.20 | 0.47 |
| 0.25 | 0.48 |
| 0.30 | 0.49 |
| 0.35 | 0.52 |
| 0.40 | 0.55 |
| 0.45 | 0.59 |
| 0.50 | 0.61 |
| 0.55 | 0.62 |
| 0.60 | 0.62 |
| 0.65 | 0.67 |
| 0.70 | 0.70 |
| 0.75 | 0.74 |
| 0.80 | 0.75 |
| 0.85 | 0.78 |
| 0.90 | 0.84 |
| 0.95 | 0.88 |
| 1.00 | 0.98 |


TOXICITY@2 | TOXICITY@4
------------------- | ------------------
not normalized | better normalized
(before 2017-06-13) | (after 2017-08-15)
0.00 | 0.00
0.05 | 0.13
0.10 | 0.23
0.15 | 0.33
0.20 | 0.37
0.25 | 0.48
0.30 | 0.51
0.35 | 0.57
0.40 | 0.63
0.45 | 0.67
0.50 | 0.70
0.55 | 0.77
0.60 | 0.80
0.65 | 0.80
0.70 | 0.86
0.75 | 0.87
0.80 | 0.91
0.85 | 0.94
0.90 | 0.95
0.95 | 0.98
1.00 | 1.00


TOXICITY@2 | TOXICITY@3 | TOXICITY@4
------------------- | ------------------- | ------------------
not normalized | kinda normalized | better normalized
(before 2017-06-13) | (until 2017-08-15) | (after 2017-08-15)
0.00 | 0.00 | 0.00
0.05 | 0.01 | 0.13
0.10 | 0.03 | 0.23
0.15 | 0.09 | 0.33
0.20 | 0.13 | 0.37
0.25 | 0.27 | 0.48
0.30 | 0.34 | 0.51
0.35 | 0.44 | 0.57
0.40 | 0.63 | 0.63
0.45 | 0.66 | 0.67
0.50 | 0.71 | 0.70
0.55 | 0.83 | 0.77
0.60 | 0.87 | 0.80
0.65 | 0.87 | 0.80
0.70 | 0.92 | 0.86
0.75 | 0.95 | 0.87
0.80 | 0.97 | 0.91
0.85 | 0.98 | 0.94
0.90 | 1.00 | 0.95
0.95 | 1.00 | 0.98
1.00 | 1.00 | 1.00
