[Perspective API documentation](../README.md) > [API Reference Docs](README.md) > **Attributes**

# Attributes

An attribute (previously known as "models") is a label on which a comment is scored. For example, the some attributes scored by Perspective API include as `TOXICITY`, `PROFANITY`, `FLIRTATION`, and more. [See all attribute types](#all-attribute-types). Attributes can be in-production or experimental.

[Join the perspective-announce email group](https://groups.google.com/forum/#!forum/perspective-announce) to stay in the loop on important information about new attributes, updates to existing attributes, and deprecations.

## Production attributes

Production attributes have been tested across multiple domains and trained on hundreds of thousands of human-annotated comments.

We recommend using production attributes for your API requests.

## Experimental attributes

Experimental attributes have not been tested as thoroughly as production attributes. If using these attributes, you’ll need to update your code when an attribute changes from experimental to production. We typically give one month’s notice before deprecating experimental attributes.

We recommend using experimental attributes only in non-production environments.

### Important notes on using experimental attributes

Once experimental attributes are deprecated and production attributes are created, the experimental attribute will stop working. If that happens, you will need to update the API call's attribute name to the new production attribute name.

Experimental attributes will make even more mistakes than production attributes. They may not have been tested for issues, such as unintended bias. For these attributes in particular, we strongly recommend a human be tasked with identifying and correcting errors.

## Specifying language

See the `languages` field description in the [Methods](#api-methods) section to learn about how to specify language in your request. If you are using a production attribute, language is auto-detected if not specified in the request.

### Languages in production 

Currently, Perspective API has production `TOXICITY` and `SEVERE_TOXICITY` attributes in the following languages:

+ English (en)
+ Spanish (es)
+ French (fr)
+ German (de)
+ Portuguese (pt)
+ Italian (it)

### Experimental attributes for other language(s)

Developing Perspective API's attributes for production takes some time. We are actively working on expanding to more languages in both experimental and production attributes and will update here when new languages are available.

Only use the experimental attribute(s) if you are interested in testing and are willing to change your code once the production attributes are available. If you are not sure, please wait until a production attribue is ready which we will announce via perspective-announce@.

## All attribute types

### Toxicity attributes
 
| Attribute name | Type | Description | Language |
| -------------------- | ---- | ----------- | -------- |
| `TOXICITY` | prod. | Rude, disrespectful, or unreasonable comment that is likely to make people leave a discussion. | en, fr, es, de, it, pt | 6 |
| `SEVERE_TOXICITY` | prod. | A very hateful, aggressive, disrespectful comment or otherwise very likely to make a user leave a discussion or give up on sharing their perspective. This attribute is much less sensitive to comments that include positive uses of curse words, for example. A labelled dataset and details of the methodology can be found in the same toxicity dataset that is available for the toxicity attribute. | en, fr, es, de, it, pt |
| `TOXICITY_FAST` | exp. | This attribute is similar to `TOXICITY`, but has lower latency and lower accuracy in its predictions. Unlike `TOXICITY`, this attribute returns summary scores as well as span scores. This attribute uses character-level n-grams fed into a logistic regression, a method that has been surprisingly effective at detecting abusive language. | en |
| `IDENTITY_ATTACK` | exp. | Negative or hateful comments targeting someone because of their identity. | en, de, it, pt |
| `IDENTITY_ATTACK_EXPERIMENTAL` | exp. | &nbsp; | fr, es |
| `INSULT` | exp. | Insulting, inflammatory, or negative comment towards a person or a group of people. | en, de, it, pt |
| `INSULT_EXPERIMENTAL` | exp. | &nbsp; | fr, es |
| `PROFANITY` | exp. | Swear words, curse words, or other obscene or profane language. | en, de, it, pt |
| `PROFANITY_EXPERIMENTAL` | exp. | &nbsp; | fr, es |
| `THREAT` | exp. | Describes an intention to inflict pain, injury, or violence against an individual or group. | en, de, it, pt |
| `THREAT_EXPERIMENTAL` | exp. | &nbsp; | fr, es |
| `SEXUALLY_EXPLICIT` | exp. |Contains references to sexual acts, body parts, or other lewd content. | en |
|`FLIRTATION` | exp. | Pickup lines, complimenting appearance, subtle sexual innuendos, etc. | en |
 
### New York Times attributes

These attributes are experimental because they are trained on a single source of comments&mdash;New York Times (NYT) data tagged by their moderation team&mdash;and therefore may not work well for every use case. 

| Attribute name | Type | Description | Language |
| -------------------- | ---- | ----------- | -------- |
| `ATTACK_ON_AUTHOR` | exp. | Attack on the author of an article or post. | en |
| `ATTACK_ON_COMMENTER` | exp. | Attack on fellow commenter. | en |
| `INCOHERENT` | exp. | Difficult to understand, nonsensical. | en |
| `INFLAMMATORY` | exp. | Intending to provoke or inflame. | en |
| `LIKELY_TO_REJECT` | exp. | Overall measure of the likelihood for the comment to be rejected according to the NYT's moderation. | en |
| `OBSCENE` | exp. | Obscene or vulgar language such as cursing. | en |
| `SPAM` | exp. | Irrelevant and unsolicited commercial content. | en |
| `UNSUBSTANTIAL` | exp. | Trivial or short comments. | en |


## Attribute architecture

Most of our attributes are [Convolutional Neural Network](https://en.wikipedia.org/wiki/Convolutional_neural_network) (CNN) trained with [word-vector](https://www.tensorflow.org/tutorials/word2vec) inputs. You can also train your own [deep CNN for text classification](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow/) on our [public toxicity dataset](https://figshare.com/articles/Wikipedia_Talk_Labels_Toxicity/4563973), and explore our [open-source attribute training tools](https://github.com/conversationai/conversationai-models) to train your own attributes. Our [Toxicity Kaggle Competition](https://kaggle.com/c/jigsaw-toxic-comment-classification-challenge) also has lots of useful resources to help build your own attributes.

## Model cards

For each production attribute, we aim to publish an associated "Model card" that shares details about intended usage, attribute training processes, and evaluation results.

[View the current model cards](model-cards/README.md).

## All reference materials

Read more about the Perspective API and how to use it.

* [Key concepts](key-concepts.md)
* **Attributes**
   * [Model cards](model-cards/README.md)
* [Methods](methods.md)
   * [Scoring comments](methods.md#scoring-comments-analyzecomment)
   * [Sending feedback](methods.md#sending-feedback-suggestcommentscore)
* [API client libraries](clients.md)
* [Limits and errors](limits.md)

