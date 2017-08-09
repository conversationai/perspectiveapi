# Score Normalization and Stable Model Updates


## What is score normalization for?

Score normalization of our models is intended to do two things:

*   Provide a way to interpret the scores of a model as a probability (e.g.
    that the comment will be considered toxic).
*   Enable models to be improved, e.g. without normalization, clients using the
    model would have to change the thresholds they use each time our models are retrained with additional examples.


## When did score-normalizing start happening?

*   [v1 of score normalization](score_normalization_v1.md) on 2017-06-13
    we introduced score normalization for all models.
*   [v2 of score normalization](score_normalization_v2_for_toxicity.md) on
    2017-08-15 we will fix our normalization of TOXICITY scores (other models
    are not affected).


## And how to you do it?

Our normalization process applies a version of [probability calibration by
isotonic regression](http://scikit-learn.org/stable/modules/calibration.html) to
make the scores approximate probabilities. For example, so that a toxicity score
of **0.80** can be interpreted as a belief that **80%** of people would consider
the comment to be toxic.

However, as we introduce additional data, the basic distribution of how many
toxic comments there are can change. Because models are far from perfect, this
would result in a shift in the calibration scores. To control for this, we
perform callibration on a randomly selected 50/50 class split. of course, this
control is not perfect: if the newly introduced examples are differently
difficult to previous ones, some change in scores is still likely.
However, in practice, we think this will be reasonably stable, and clients will be able to have the same 'sense' of what a threshold means.

We are always looking for better ways to provide stability, so if you know of better ways to do this, please do [file an issue](https://github.com/conversationai/perspectiveapi/issues).
