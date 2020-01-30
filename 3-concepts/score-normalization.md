[Perspective API documentation](../README.md) >  [Concepts](README.md) > **Score normalization and feedback**

# Score normalization and feedback

Score normalization of our attributes is intended to do two things:

*   Provide a way to interpret the scores of an attribute as a probability
    (e.g. how likely is it that the comment will be perceived as toxic).
*   Enable attributes to be improved without any action needed by most clients,
    Without normalization, clients using the attribute would have to change the
    thresholds they use each time our attributes are retrained with additional
    examples.


## When did score-normalizing start happening?

*   [v1 of score normalization](/releases/score_normalization_v1.md) on 2017-06-13
    introduced score normalization for all attributes.
*   [v2 of score normalization](/releases/score_normalization_v2_for_toxicity.md) on
    2017-08-15: fixes will go live for our normalization of `TOXICITY` scores
    (other attributes are not affected).


## How is score normalization done?

Our normalization process applies a version of [probability calibration by
isotonic regression](http://scikit-learn.org/stable/modules/calibration.html) to
make the scores approximate probabilities. For example, so that a toxicity score
of **0.80** can be interpreted as a belief that **80%** of people would consider
the comment to be toxic.

However, as we introduce additional data, the basic distribution of how many
toxic comments there are can change. Because attributes are far from perfect, this
would result in a shift in the calibration scores. To control for this, we
perform callibration on a randomly selected 50/50 class split. of course, this
control is not perfect: if the newly introduced examples are differently
difficult to previous ones, some change in scores is still likely.
However, in practice, we think this will be reasonably stable, and clients will
be able to have the same 'sense' of what a threshold means.

We are always looking for better ways to provide stability, so if you know of
better ways to do this, please
[open an issue on GitHub](https://github.com/conversationai/perspectiveapi/issues).

## About score feedback

Our machine learning attributes are not perfect and will make errors. our
attributes will be unable to detect patterns of toxicity it has not seen
before, and it will falsely detect comments similar to patterns of previous
toxic conversations. To help improve the machine learning, the API supports
sending our team suggested scores and corrections.

## Reporting issues with scores
 
### Reporting via API

To report feedback on attribute scores, submit feedback as a request to the API
using [`SuggestCommentScore`](api_reference.md#suggestcommentscore-request).

Since all submissions are stored and used to improved the API, do not use this for private
data (i.e. for data that is not accessible publicly), or if the data submitted contains
content written by someone under 13 years old.
 
### Reporting in bulk

To manually submit corrections in bulk, you can use
[this form](https://docs.google.com/forms/d/e/1FAIpQLScAivfFHiwq08JfsHuIkTbdECLK0nSmyBi4JMvaqDrom2aVQw/viewform?c=0&w=1).
Read more about this process in the [Contribution guidelines](CONTRIBUTING.md).

