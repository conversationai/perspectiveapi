[Back to Conversation AI Overview](https://conversationai.github.io/) | [Back to Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md)

# Glossary

These are the terms you must know to understand the Perspective API and documentation.

### Attribute

An **attribute** or **model attribute** is a comment label used for review.
The most popular attribute is "toxicity".

This was previously known also as "model".

### Comment

A **comment** is the text to be scored. Each API request contains a single
comment. A comment could be a single post to a web page's comments section,
a forum post, a message to a mailing list, a chat message, etc.

### Context (coming soon)

_(Coming soon)_ **Context** is a representation of the conversation context
for the comment, such as an article that is being commented on, or another
comment that is being replied to. It is used in the analysis of the
comment text, such as when determining the "off-topic" model score.

**Note**: you can send context with your requests, however our current models
are not making use of it. At this time, sending context won't change a model's
scores.

### Method

A **method** is a procedure associating a message (or request) with an
object (which consists of data and behavior). A method request will return
a new object.

For example, the [`AnalyzeComment` method](methods.md#scoring-comments-analyzecomment)
sends a request to score the comment object. The comment object includes
comment text, context, and more. The method then return the attribute span
scores.


### Score types

**Score types** are different formats for the API to return model attribute
scores. Currently, the only score type supported is the probability score
type with a value between 0 and 1. Higher values indicating greater likelihood
of the attribute label.

### Span

A **span** is a continuous section of text. The API can return span scores,
which are model scores for particular subparts of the request's comment.

### Span scores

A **span score** is a score type for subparts of the request's comment.

For example, if the API only found one sentence in a paragraph to be "toxic",
it could return a high "toxic" span score for the span corresponding to that
sentence while giving a low "toxic" span score to the rest of the comment.
This score is only available for some models.

### Summary Score

A model's **summary score** provides an overall score for the entire comment.
While the API may return multiple span scores for a given input, it will
always return exactly one summary score.

### Toxicity

**Toxicity** is an attribute which Perspective can score. Toxicity is defined
as "a rude, disrespectful, or unreasonable comment that is likely to make you
leave a discussion."
