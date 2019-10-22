# Concepts

## What is score normalization for?

Score normalization of our models is intended to do two things:

*   Provide a way to interpret the scores of a model as a probability (e.g. how
    likely is it that the comment will be perceived as toxic).
*   Enable models to be improved without any action needed by most clients,
    Without normalization, clients using the model would have to change the
    thresholds they use each time our models are retrained with additional
    examples.

[Read more](score-normalization.md)
