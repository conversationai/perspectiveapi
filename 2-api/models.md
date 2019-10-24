[Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md) > [API Reference Docs](README.md) > **Production and experimental models**

# Production and experimental models

This section details Perspective API’s production and experimental models, which are described in detail in the [All model types](#all-model-types) table below.

We recommend subscribing to [perspective-announce email group](https://groups.google.com/forum/#!forum/perspective-announce) to stay in the loop on important information about new models, updates to existing models, and deprecations. 

## Production models

We recommend using production models for your API request. Production models have been tested across multiple domains and trained on hundreds of thousands of human-annotated comments.

## Experimental models

We recommend reserving experimental models for non-production use cases. These models have not been tested as thoroughly as production models, and you’ll need to update your code when a model changes from experimental to production. We typically give one month’s notice before deprecating experimental models.

## Latest versions

We retrain models and release new versions periodically. To call a specific version of a model, use the format `MODEL_NAME@VERSION_NUMBER` in the `requestedAttributes` field.

If a request does not specify a `@VERSION_NUMBER` at the end of a model name, it uses the default version, which is often, but not always, the latest version of the model.
 
View the latest version numbers in the [All model types](#all-model-types) table below.

## Specifying language

See the `languages` field description in the [Methods](#api-methods) section below to learn about how to specify language in your request. If you are using a production model, language is autodetected if not specified in the request.

## All model types

### Toxicity models
 
| Model attribute name | Type | Description | Language | Latest version |
| -------------------- | ---- | ----------- | -------- | -------------- |
| `TOXICITY` | prod. | Rude, disrespectful, or unreasonable comment that is likely to make people leave a discussion. | en, fr, es | 6 |
| `TOXICITY_EXPERIMENTAL` | exp. | &nbsp; | de, it, pt | &nbsp; |
| `SEVERE_TOXICITY` | prod. | A very hateful, aggressive, disrespectful comment or otherwise very likely to make a user leave a discussion or give up on sharing their perspective. This model is much less sensitive to comments that include positive uses of curse words, for example. A labelled dataset and details of the methodology can be found in the same toxicity dataset that is available for the toxicity model. | en, fr, es | 2 |
| `SEVERE_TOXICITY_EXPERIMENTAL` | exp. | &nbsp; | de, it, pt | &nbsp; |
| `TOXICITY_FAST` | exp. | This model is similar to the `TOXICITY` model, but has lower latency and lower accuracy in its predictions. Unlike `TOXICITY`, this model returns summary scores as well as span scores. This model uses character-level n-grams fed into a logistic regression, a method that has been surprisingly effective at detecting abusive language. | en | &nbsp; |
| `IDENTITY_ATTACK` | exp. | Negative or hateful comments targeting someone because of their identity. | en | 2 |
| `IDENTITY_ATTACK_EXPERIMENTAL` | exp. | &nbsp; | fr, de, es, it, pt | &nbsp; |
| `INSULT` | exp. | Insulting, inflammatory, or negative comment towards a person or a group of people. | en | 2 |
| `INSULT_EXPERIMENTAL` | exp. | &nbsp; | fr, de, es, it , pt | &nbsp; |
| `PROFANITY` | exp. | Swear words, curse words, or other obscene or profane language. | en | 2 |
| `PROFANITY_EXPERIMENTAL` | exp. | &nbsp; | fr, de, es, it, pt | &nbsp; |
| `THREAT` | exp. | Describes an intention to inflict pain, injury, or violence against an individual or group. | en | 2 |
| `THREAT_EXPERIMENTAL` | exp. | &nbsp; | fr, de, es, it, pt | &nbsp; |
| `SEXUALLY_EXPLICIT` | exp. |Contains references to sexual acts, body parts, or other lewd content. | en | 2 |
|`FLIRTATION` | exp. | Pickup lines, complimenting appearance, subtle sexual innuendos, etc. | en | 2 |
 
### New York Times models

These models are experimental because they are trained on a single source of comments&mdash;New York Times (NYT) data tagged by their moderation team&mdash;and therefore may not work well for every use case. 

| Model attribute name | Type | Description | Language | Latest version |
| -------------------- | ---- | ----------- | -------- | -------------- |
| `ATTACK_ON_AUTHOR` | exp. | Attack on the author of an article or post. | en | 2 |
| `ATTACK_ON_COMMENTER` | exp. | Attack on fellow commenter. | en | 2 |
| `INCOHERENT` | exp. | Difficult to understand, nonsensical. | en | 2 |
| `INFLAMMATORY` | exp. | Intending to provoke or inflame. | en | 2 |
| `LIKELY_TO_REJECT` | exp. | Overall measure of the likelihood for the comment to be rejected according to the NYT's moderation. | en | 2 |
| `OBSCENE` | exp. | Obscene or vulgar language such as cursing. | en | 2 |
| `SPAM` | exp. | Irrelevant and unsolicited commercial content. | en | 1 |
| `UNSUBSTANTIAL` | exp. | Trivial or short comments. | en | 2 |


## Model architecture

Most of our models are [Convolutional Neural Network](https://en.wikipedia.org/wiki/Convolutional_neural_network) (CNN) trained with [word-vector](https://www.tensorflow.org/tutorials/word2vec) inputs. You can also train your own [deep CNN for text classification](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow/) on our [public toxicity dataset](https://figshare.com/articles/Wikipedia_Talk_Labels_Toxicity/4563973), and explore our [open-source model training tools](https://github.com/conversationai/conversationai-models) to train your own models. Our [Toxicity Kaggle Competition](https://kaggle.com/c/jigsaw-toxic-comment-classification-challenge) also has lots of useful resources to help build your own models.

## Model Cards

For each production model, we aim to publish an associated "Model Card" that shares details about intended usage, model training processes, and evaluation results.

[View the current model cards](model-cards/README.md).

## All reference materials

Read more about the Perspective API and how to use it.

* [Key concepts](key-concepts.md)
* **Production and experimental models**
   * [Model cards](model-cards/README.md)
* [Methods](methods.md)
   * [Scoring comments](methods.md#scoring-comments-analyzecomment)
   * [Sending feedback](methods.md#sending-feedback-suggestcommentscore)
* [API client libraries](clients.md)
* [Languages](languages.md)
* [Limits and errors](limits.md)

