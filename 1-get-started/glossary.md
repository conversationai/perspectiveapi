[Perspective API documentation](../README.md) > [Get Started](README.md) > **Glossary**

# Glossary

These are the terms you must know to understand the Perspective API and documentation.

### Attribute

A comment label used for review. The most popular attributes are the toxicity and severe toxicity models.

### Comment

The text to be scored. Each API request contains a single comment. A comment could be a single post to a web page's comments section, a forum post, a message to a mailing list, a chat message, etc.

### Model

A dimension that the comment is scored on, for example, "toxic", "obscene", "thoughtful", "off-topic", etc. This is also sometimes referred to as an attribute or model attribute. Models can be labeled `Prod`, meaning they are recommended for use, or experimental, meaning that they are still in development but are open for public use if you're comfortable using experimental, imperfect models. See our list of models here.

### Model summary score

An overall score for the entire comment. While the API may return multiple span scores for a given input, it will always return exactly one summary score.

### Span

A continuous section of text.

### Span scores

Model scores for particular subparts of the request's comment. For example, if the API only found one sentence in a paragraph to be "toxic", it could return a high "toxic" span score for the span corresponding to that sentence while giving a low "toxic" span score to the rest of the comment. This score is only available for some models.

### Toxicity

One of the attributes that Perspective can score. Toxicity is defined as "a rude, disrespectful, or unreasonable comment that is likely to make you leave a discussion."
