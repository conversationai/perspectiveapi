[Perspective API documentation](../README.md) > **Concepts**

# Concepts

## Score normalization

We use score normalization for our attributes, which is intended to do two
things:

*   Provide a way to interpret the scores of an attribute as a probability
    (e.g. how likely is it that the comment will be perceived as toxic).
*   Enable attributes to be improved without any action needed by most clients,
    Without normalization, clients using the attribute would have to change the
    thresholds they use each time our attributes are retrained with additional
    examples.

[Read more about score normalization](score-normalization.md)
