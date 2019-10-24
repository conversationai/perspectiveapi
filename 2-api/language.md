[Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md) > [API Reference Docs](README.md) > **Languages**

# Languages served by Perspective API

## Languages in production 

Currently, Perspective API has production `TOXICITY` and `SEVERE_TOXICITY` models in the following languages:

+ English (en)
+ Spanish (es)
+ French (fr)

## Experimental models for other language(s)

Developing Perspective API's models for production takes some time. We are actively working on expanding to more languages in production. The following languages are those that are still being developed for production but ready for experimental use:

+ German (de)
+ Portuguese (pt)
+ Italian (it)

Only use the above model(s) if you are interested in testing an experimental model and are willing to change your code once the production models are available. If you are not sure, please wait until a production version is ready which we will announce via perspective-announce@.

If you wish to test new experimental models please refer to [model reference](/api/models.md). 

 ### Important notes on using experimental models:

Experimental versions will be deprecated. These models are experimental and will eventually stop working when the production versions are created, so you will need to update the model name you are calling when the final version is available.

Experimental versions will make even more mistakes than production models. They may not have been tested for issues including unintended bias and thus it is particularly important that they only be used in contexts where you have a human in the loop to identify and correct errors.

## All reference materials

Read more about the Perspective API and how to use it.

* [Key concepts](key-concepts.md)
* [Production and experimental models](models.md)
   * [Model cards](model-cards/README.md)
* [Methods](methods.md)
   * [Scoring comments](methods.md#scoring-comments-analyzecomment)
   * [Sending feedback](methods.md#sending-feedback-suggestcommentscore)
* [API client libraries](clients.md)
* **Languages**
* [Limits and errors](limits.md)

