[Perspective API documentation](../README.md) > [API Reference Docs](README.md) > **Key concepts**

# Key concepts

To best understand the reference documentation, you must first know these key concepts.

## Attribute

A comment label used for review. The most popular attributes are the toxicity and severe toxicity models.

## Comment

A **comment** is the text to be scored. Each API request contains a single
comment. A comment could be a single post to a web page's comments section,
a forum post, a message to a mailing list, a chat message, etc.

## Model

 A **model** is a dimension that the comment is scored on; for example,
 "toxic," "obscene," "thoughtful," "off-topic," etc. This is also sometimes referred to
 as an **attribute** or **model attribute**.

### Model attribute scores

The API can return **model attribute scores** in different formats, known as
**score types**. Currently, the only score type supported is a probability score
between 0 and 1, with higher values indicating greater likelihood of the attribute
label.

### Summary Score

A model's **summary score** provides an overall score for the entire
comment. While the API may return multiple span scores for a given input, it
will always return exactly one summary score.

## Span

A **span** is a continuous section of text. The API can return **span scores**, which are
model scores for particular subparts of the request's comment. For example, if the API only
found one sentence in a paragraph to be "toxic," it could return a high "toxic" span score
for the span corresponding to that sentence, while giving a low "toxic" span score to the
rest of the comment.

### Span scores

Model scores for particular subparts of the request's comment. For example, if the API only found one sentence in a paragraph to be "toxic", it could return a high "toxic" span score for the span corresponding to that sentence while giving a low "toxic" span score to the rest of the comment. This score is only available for some models.

## Context

*(Coming soon)* **Context** is a representation of the conversation context
for the comment; for example, an article that is being commented on, or
another comment that is being replied to. It is used in the analysis of the
comment text; for example, when determining the "off-topic" model score.

**Note**: you can send context with your requests, however our current models
are not making use of it&mdash;so sending context won't change any model's
scores.

## Toxicity

One of the attributes that Perspective can score. Toxicity is defined as "a rude,
disrespectful, or unreasonable comment that is likely to make you leave a discussion."

## All reference materials

Read more about the Perspective API and how to use it.

* **Key concepts**
* [Models and attributes](models.md)
   * [Model cards](model-cards/README.md)
* [Methods](methods.md)
   * [Scoring comments](methods.md#scoring-comments-analyzecomment)
   * [Sending feedback](methods.md#sending-feedback-suggestcommentscore)
* [API client libraries](clients.md)
* [Limits and errors](limits.md)

