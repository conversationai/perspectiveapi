[Back to Conversation AI Overview](https://conversationai.github.io/) | [Back to Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md)

# Perspective API reference

 * [Using the API](#using-the-api)
 * [Key concepts](#key-concepts)
 * [Models](#models)
 * [Methods](#methods)
   * [Scoring comments](#scoring-comments-analyzecomment)
   * [Sending feedback](#sending-feedback-suggestcommentscore)
 * [API client libraries](#api-client-libraries)
 * [Privacy and Terms of Service](#privacy-and-terms-of-service)

## Using the API

First, follow the [quickstart guide](quickstart.md) to enable the API for your
project, generate an API key, and ensure you're able to make a successful
request.

### Quota and character length Limits

You can check your quota limits by going to [your google cloud project's Perspective API page](https://console.cloud.google.com/apis/api/commentanalyzer.googleapis.com/quotas), and check
your projects quota usage at
[the cloud console quota usage page](https://console.cloud.google.com/iam-admin/quotas).

The maximum text size per request is 3000 bytes.

## Key concepts

*   A **comment** is the text to be scored. Each API request contains a single
    comment. A comment could be a single post to a web page's comments section,
    a forum post, a message to a mailing list, a chat message, etc.

*   A **model** is a dimension that the comment is scored on, for example,
    "toxic", "obscene", "thoughtful", "off-topic", etc. This is also sometimes referred to
    as an **attribute** or **model attribute**.

*   The API can return **model attribute scores** in different formats, known as
    **score types**. The default score type is a probability score between 0 to
    1, with higher values indicating greater likelihood of the attribute label.

*   A **span** is a continuous section of text. The API can return **span
    scores**, which are model scores for particular subparts of the request's
    comment. For example, if the API only found one sentence in a paragraph to
    be "toxic", it could return a high "toxic" span score for the span
    corresponding to that sentence while giving a low "toxic" span score to the
    rest of the comment.

*   A model's **summary score** provides an overall score for the entire
    comment. While the API may return multiple span scores for a given input, it
    will always return exactly one summary score.

*   *(Coming soon)* **Context** is a representation of the conversation context
    for the comment (for example, an article which is being commented on, or
    another comment that is being replied to). It is used in the analysis of the
    comment text, for example when determining the "off-topic" model score.

    *Note:* you can send context with your requests, however our current models
    are not making use of it, so sending context won't change any model's
    scores.

## Models

### Toxicity and subtypes model definitions

These models are the only one with production support in a couple of languages. See the for the full list.

*   **TOXICITY**: rude, disrespectful, or unreasonable comment that is likely to
    make people leave a discussion.
*   **SEVERE_TOXICITY**: a very hateful, aggressive, disrespectful comment or otherwise very likely to make a user leave a       discussion or give up on sharing their perspective. This model is much less sensitive to
    comments that include positive uses of curse-words for example. A labelled dataset
    and details of the methodolgy can be found in the same [toxicity dataset](https://figshare.com/articles/Wikipedia_Talk_Labels_Toxicity/4563973) that is
    available for the toxicity model.
    
The toxicity subtypes models are only available as experimental models. 
    
*   **IDENTITY_ATTACK**: negative or hateful comments targeting someone because of their identity.
*   **INSULT**: insulting, inflammatory, or negative comment towards a person
    or a group of people.
*   **PROFANITY**: swear words, curse words, or other obscene or profane
    language.
*   **THREAT**: describes an intention to inflict pain, injury, or violence
    against an individual or group.
*   **SEXUALLY_EXPLICIT**: contains references to sexual acts, body parts, or
    other lewd content.
*   **FLIRTATION**: pickup lines, complimenting appearance, subtle sexual
    innuendos, etc.
    
See the [Toxicity and sub-attribute annotation guidelines](https://github.com/conversationai/conversationai.github.io/blob/master/crowdsourcing_annotation_schemes/toxicity_with_subattributes.md) for more details.

To get a sense of the scores our TOXICITY models give on actual comments, see [this CSV
of scored
comments](example_data/perspective_wikipedia_2k_score_sample_20180829.csv).
These 2,000 comments are from Wikipedia talk page discussions, randomly sampled
from our [Kaggle
competition](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/data).

Sorting by each model's scores gives a sense of the model's behavior. These
examples may differ quite a bit from the types of comments in your particular
use case, so we strongly recommend evaluating on your own data as well.

### Model architecture

Most of our models are [Convolutional Neural Network](https://en.wikipedia.org/wiki/Convolutional_neural_network) (CNN)
trained with [word-vector](https://www.tensorflow.org/tutorials/word2vec) inputs. You can also train your own
[deep CNN for text classification](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow/) on [our public toxicity dataset](https://figshare.com/articles/Wikipedia_Talk_Labels_Toxicity/4563973), and explore [our open-source model training tools](https://github.com/conversationai/conversationai-models) to train your own models.

[Our Toxicity Kaggle Competition](https://kaggle.com/c/jigsaw-toxic-comment-classification-challenge)
has lots of useful resources to help build your own models.
Note that there are many kinds of toxic language that are disproportionately
represented in our dataset, which leads to some obviously incorrect scores, as well as unintended biases.
Please use the [SuggestCommentScore](#suggestcommentscore-request) method to
help improve the model.

### Model Cards
For each production model, we aim to publish an associated "Model Card" that shares details
about model training and evaluation results. Current model cards are posted
[here](model_cards/README.md).

### Production Toxicity models

We recommend using **production models**. They have been tested
across multiple domains and trained on hundreds of thousands of comments tagged
by thousands of human moderators. Below you will find language support and attribute name for your API request.

Production Model                  | Supported Languages
----------------------------------|-----------------------
TOXICITY                          | en, fr, es
SEVERE_TOXICITY                   | en, fr, es

### Experimental Toxicity models

The following models are experimental models. Only use these if you are
interested in testing an experimental model and are willing to change your code once the
production models are available. These have not been tested as
thoroughly as their production counterparts. If you would like to support Perspective in new languages, you can contribute data [here](https://docs.google.com/forms/d/e/1FAIpQLScAivfFHiwq08JfsHuIkTbdECLK0nSmyBi4JMvaqDrom2aVQw/viewform)

Experimental Model                | Supported Languages
----------------------------------|-----------------------
TOXICITY_EXPERIMENTAL             | de, it, pt
SEVERE_TOXICITY_EXPERIMENTAL      | de, it, pt
IDENTITY_ATTACK                   | en
IDENTITY_ATTACK_EXPERIMENTAL      | fr, de, es, it, pt
INSULT                            | en
INSULT_EXPERIMENTAL               | fr, de, es, it , pt
PROFANITY                         | en
PROFANITY_EXPERIMENTAL            | fr, de, es, it, pt
THREAT                            | en
THREAT_EXPERIMENTAL               | fr, de, es, it, pt
SEXUALLY_EXPLICIT                 | en
FLIRTATION                        | en

Please refer to the rest of the documentation bellow to appropriately set the
language field in your request. Currently if you want to use the API on an experimental language and another production language (e.g. TOXICITY French and German) there is no simple way to do that. You can
either (1) change how you call the API depending on the comment language, or (2)
wait until these models join the production track, when they'll be handled automatically.

### More experimental models

The following models are experimental. They were targeted for a single usecase,
so may not generalize to your usecase well. They may be deprecated or removed
with little notice (typically a few months).

#### New York Times moderation models

The following experimental models were trained on New York Times data tagged by
their moderation team.

*   **ATTACK_ON_AUTHOR**: Attack on the author of an article or post.
*   **ATTACK_ON_COMMENTER**: Attack on fellow commenter.
*   **INCOHERENT**: Difficult to understand, nonsensical.
*   **INFLAMMATORY**: Intending to provoke or inflame.
*   **LIKELY_TO_REJECT**: Overall measure of the likelihood for the comment to
    be rejected according to the NYT's moderation.
*   **OBSCENE**: Obscene or vulgar language such as cursing.
*   **SPAM**: Irrelevant and unsolicited commercial content.
*   **UNSUBSTANTIAL**: Trivial or short comments.

#### TOXICITY_FAST

*   **TOXICITY_FAST**: This model is similar to the TOXICITY model, but has
    lower latency and lower accuracy in its predictions. Unlike TOXICITY, this
    model returns summary scores as well as span scores. This model uses
    character-level n-grams fed into a logistic regression, a method that has
    has been surprisingly
    [effective at detecting abusive language](https://dl.acm.org/citation.cfm?id=2883062).

### Versions

Models are versioned. We re-retrain them and release a new version when we get enough new trusted examples, either from [our demo](https://www.perspectiveapi.com) or from other clients of the API who ask us use their examples to make the models better (see the `AnalyzeComment` and `SuggestCommentScore` methods below). To use a specific version of a model, use a model name of the form `MODEL_NAME@VERSION_NUMBER`. If a request does not specify a `@VERSION_NUMBER` at the end of a model name, it will use the latest version of the model. The latest version numbers are in the following table.

Model Attribute Name | Latest Version Name
---------------------|-----------------------
TOXICITY             | TOXICITY@6
SEVERE_TOXICITY      | SEVERE_TOXICITY@2
IDENTITY_ATTACK      | IDENTITY_ATTACK@2
INSULT               | INSULT@2
PROFANITY            | PROFANITY@2
SEXUALLY_EXPLICIT    | SEXUALLY_EXPLICIT@2
THREAT               | THREAT@2
FLIRTATION           | FLIRTATION@2
ATTACK_ON_AUTHOR     | ATTACK_ON_AUTHOR@2
ATTACK_ON_COMMENTER  | ATTACK_ON_COMMENTER@2
INCOHERENT           | INCOHERENT@2
INFLAMMATORY         | INFLAMMATORY@2
LIKELY_TO_REJECT     | LIKELY_TO_REJECT@2
OBSCENE              | OBSCENE@2
SPAM                 | SPAM@1
UNSUBSTANTIAL        | UNSUBSTANTIAL@2

Announcements about new  models and versions of models (and depricated stuff) are sent to the: [`perspective-announce email group`](https://groups.google.com/forum/#!forum/perspective-announce); subscribe to stay up to date.

## Methods

### Scoring comments: `AnalyzeComment`

To send a comment scoring request to the API, post a request object to this
endpoint:

> **POST** https://commentanalyzer.googleapis.com/v1alpha1/comments:analyze

*Note:* If you're using API key authentication, append `?key=YOUR_API_KEY` to
the end of the request. See the [quickstart](quickstart.md) guide for an
example.

#### `AnalyzeComment` request

```
{
  "comment": {
    "text": string,
    "type": string
  },
  "context": {
    "entries": [{
      "text": string,
      "type": string
    }]
  },
  "requestedAttributes": {
    string: {
      "scoreType": string,
      "scoreThreshold": float
    },
  },
  "languages": [string],
  "doNotStore": bool,
  "clientToken": string,
  "sessionId": string,
}
```

Field | Description
----- | -----------
`comment.text`           | **(required)** The text to score. This is assumed to be utf8 raw text of the text to be checked. Emoji and other non-ascii characters can be included (raw HTML will probably result in lower performance). The maximum size of comment.text request is 3000 bytes.
`comment.type`           | *(optional)* The text type of `comment.text`. Either "PLAIN_TEXT" or "HTML". Currently only "PLAIN_TEXT" is supported.
`context.entries`        | *(optional)* A list of objects providing the context for `comment`. Currently ignored by the API.
`context.entries[].text` | *(optional)* The text of a context object. The maximum size of context entry is 1MB.
`context.entries[].type` | *(optional)* The text type of the corresponding context text. Same type as `comment.text`.
`requestedAttributes`    | **(required)** A map from model's attribute name to a configuration object. See the [models section](#models) for a list of available model attribute names. If no configuration options are specified, sensible defaults are used, so the empty object `{}` is a valid (and common) choice. You can specify multiple model names here to get scores from multiple models in a single request.
`requestedAttributes[name].scoreType`      | *(optional)* The score type returned for this model attribute. Currently, only "PROBABILITY" is supported. Probability scores are in the range `[0,1]`.
`requestedAttributes[name].scoreThreshold` | *(optional)* The API won't return scores that are below this threshold for this model attribute. By default, all scores are returned.
`spanAnnotations`        | *(optional)* A boolean value that indicates if the request should return spans that describe the scores for each part of the text (currently done at per sentence level). Defaults to false.
`languages`              | *(optional)* A list of [ISO 631-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) two-letter language codes specifying the language(s) that `comment` is in (for example, "en", "es", "fr", "de", etc). If unspecified, the API will autodetect the comment language. If language detection fails, the API returns an error. *Note:* Currently, all production models only support English, Spanish, and French. There is no simple way to use the API across languages with production support and languages with experimental support only.
`doNotStore`             | *(optional)* Whether the API is permitted to store `comment` and `context` from this request. Stored comments will be used for future research and community model building purposes to improve the API over time. We also plan to provide dashboards and automated analysis of the comments submitted, which will apply only to those stored. Defaults to **false** (request data may be stored). **Important note:** This should be set to true if data being submitted is private (i.e. not publicly accessible), or if the data submitted contains content written by someone under 13 years old.
`clientToken`            | *(optional)* An opaque token that is echoed back in the response.
`sessionId`              | *(optional)* An opaque session id. This should be set for authorship experiences by the client side so that groups of requests can be grouped together into a session. This should not be used for any user-specific id. This is intended for abuse protection and individual sessions of interaction.

Note that only `comment.text` and `requestedAttributes` are required.

#### `AnalyzeComment` response

```
{
  "attributeScores": {
    string: {
      "summaryScore": {
        "value": float,
        "type": string
      },
      "spanScores": [{
        "begin": int,
        "end": int,
        "score": {
           "value": float,
           "type": string
        }
      }]
    }
  },
  "languages": [string],
  "clientToken": string
}
```

Field | Description
----- | -----------
`attributeScores` | A map from model attribute name to per-attribute score objects. The attribute names will mirror the request's `requestedAttributes`.
`attributeScores[name].summaryScore.value` | The model attribute summary score for the entire comment. All attributes will return a `summaryScore` (unless the request specified a `scoreThreshold` for the attribute that the `summaryScore` did not exceed).
`attributeScores[name].summaryScore.type`  | This mirrors the requested `scoreType` for this attribute.
`attributeScores[name].spanScores`         | A list of per-span scores for this attribute. These scores apply to different parts of the request's `comment.text`. **Note:** Some attributes may not return `spanScores` at all.
`attributeScores[name].spanScores[].begin`   | Beginning of the text span in the request comment.
`attributeScores[name].spanScores[].end`     | End of the text span in the request comment.
`attributeScores[name].spanScores[].score.value` | The attribute score for the span delimited by `begin` and `end`.
`attributeScores[name].spanScores[].score.type`  | Same as `summaryScore.type`.
`languages` | Mirrors the request's `languages`. If no languages were specified, the API returns the auto-detected language.
`clientToken` | Mirrors the request's `clientToken`.

#### `AnalyzeComment` example

This is a request for the "TOXICITY" and "UNSUBSTANTIAL" models for a comment
that's explicitly in English.

```json
// Request
{
  "comment": {
     "text": "What kind of idiot name is foo? Sorry, I like your name."
  },
  "languages": ["en"],
  "requestedAttributes": {
    "TOXICITY": {},
    "UNSUBSTANTIAL": {}
  }
}
```

The response contains the "TOXICITY" and "UNSUBSTANTIAL" model scores. Each
attribute has a single overall `summaryScore` as well as two `spanScores`.

Both models return the same spans in this case: the span `[0, 31)` (corresponding
to "What kind of idiot name is foo?") and the span `[32, 56)` (corresponding to
"Sorry, I like your name."). Models may not always return the same spans,
however.

```json
// Response
{
  "attributeScores": {
    "TOXICITY": {
      "summaryScore": {
        "value": 0.8627961,
        "type": "PROBABILITY"
      }
    },
    "UNSUBSTANTIAL": {
      "spanScores": [
        {
          "begin": 0,
          "end": 31,
          "score": {
            "value": 0.52690625,
            "type": "PROBABILITY"
          }
        },
        {
          "begin": 32,
          "end": 55,
          "score": {
            "value": 0.9106685,
            "type": "PROBABILITY"
          }
        }
      ],
      "summaryScore": {
        "value": 0.69036055,
        "type": "PROBABILITY"
      }
    }
  },
  "languages": [
    "en"
  ]
}
```

### Sending feedback: `SuggestCommentScore`

The `SuggestCommentScore` endpoints submits feedback to the API in the form of a
suggested score. You can use this method if you disagree with a score and would
like to improve the model. All submissions to `SuggestCommentScore` are stored
and used to improve the API and related services. This method should **not** be
used for private data (i.e. for data that is not accessible publicly), or if the
data submitted contains content written by someone under 13 years old.

> **POST** https://commentanalyzer.googleapis.com/v1alpha1/comments:suggestscore

#### `SuggestCommentScore` request

```
{
  "comment": {
    "text": string,
    "type": string
  },
  "context": {
    "entries": [{
      "text": string,
      "type": string
    }]
  },
  "attributeScores": {
    string: {
      "summaryScore": {
         "value": float,
         "type": string
      },
      "spanScores": [{
        "begin": int,
        "end": int,
        "score": {
           "value": float,
           "type": string
        }
      }]
    }
  },
  "languages": [string],
  "communityId": string,
  "clientToken": string
}
```

Field | Description
----- | -----------
`comment`      | **(required)** Same as `AnalyzeComment` request.
`context`      | *(optional)* Same as `AnalyzeComment` request.
`attributeScores` | Similar to `AnalyzeComment` response. This holds the attribute scores that the client believes the comment should have. It has the same format as the `attributeScores` field in the `AnalyzeComment` response, as it's what the client believes is the correct "answer" for what this comment should be scored as. The client can specify just summary scores, just span scores, or both.
`languages`    | *(optional)* Same as `AnalyzeComment` request.
`communityId`  | *(optional)* Opaque identifier associating this score suggestion with a particular community. If set, this field allows us to differentiate suggestions from different communities, as each community may have different norms.
`clientToken`  | An opaque token that is echoed back in the response.

#### `SuggestCommentScore` response

```
{
  "clientToken": string
}
```

Field | Description
----- | -----------
`clientToken` | Mirrors the request's `clientToken`.

#### `SuggestCommentScore` example

This is a request stating that the comment has a "TOXICITY" summary score of 0.

```json
// Request
{
  "comment": {
    "text": "I guess it comes down a simple choice: Get busy living, or get busy dying."
  },
  "attributeScores": {
    "TOXICITY": {
      "summaryScore": {
        "value": 0
      }
    },
  },
  "communityId": "/forum/movies",
  "clientToken": "comment-53922"
}
```

The response is not particularly interesting:

```json
// Response
{
  "clientToken": "comment-53922"
}
```

## API client libraries

You can generate API client libraries using the [Google API Client
Libraries](https://developers.google.com/api-client-library/). The API Client
Libraries have been released for many languages. Here, we walk through a few
versions.

### Python

Here's an example with the [Python
version](https://developers.google.com/api-client-library/python/start/get_started)
of the Google API Client Libraries. First, install the library following [the
directions here](https://github.com/google/google-api-python-client).)

Then try this:

```python
from googleapiclient import discovery

API_KEY='replace-this-with-your-API-key'

# Generates API client object dynamically based on service name and version.
service = discovery.build('commentanalyzer', 'v1alpha1', developerKey=API_KEY)

analyze_request = {
  'comment': { 'text': 'friendly greetings from python' },
  'requestedAttributes': {'TOXICITY': {}}
}

response = service.comments().analyze(body=analyze_request).execute()

import json
print json.dumps(response, indent=2)
```

You should see something like:

```json
{
  "languages": ["en"],
  "attributeScores": {
    "TOXICITY": {
      "summaryScore": {
        "type": "PROBABILITY",
        "value": 0.012669894
      }
    }
  }
}
```

Our friendly greeting got a low toxicity score, whew.

### Node.js

Here's an example with the Node.js version of the API Client Libraries. First,
install the library (the NPM package is
[`googleapis`](https://www.npmjs.com/package/googleapis); see [their
docs](https://github.com/google/google-api-nodejs-client/) for details).

Then try this:

```javascript
var googleapis = require('googleapis');

API_KEY = 'copy-your-api-key-here'
DISCOVERY_URL = 'https://commentanalyzer.googleapis.com/$discovery/rest?version=v1alpha1'

googleapis.discoverAPI(DISCOVERY_URL, (err, client) => {
  if (err) throw err;
  var analyzeRequest = {
    comment: {text: 'Jiminy cricket! Well gosh durned it! Oh damn it all!'},
    requestedAttributes: {'TOXICITY': {}}
  };
  client.comments.analyze({key: API_KEY, resource: analyzeRequest}, (err, response) => {
    if (err) throw err;
    console.log(JSON.stringify(response, null, 2));
  });
});
```

You should see something like:

```json
{
  "attributeScores": {
    "TOXICITY": {
      "spanScores": [
        {
          "score": {
            "value": 0.4445836,
            "type": "PROBABILITY"
          }
        }
      ],
      "summaryScore": {
        "value": 0.4445836,
        "type": "PROBABILITY"
      }
    }
  },
  "languages": [
    "en"
  ]
}
```

Which shows that our old timey exclamations get lower toxicity scores.

There is also a ready-made Node.js client, which can be installed from
NPM:

```
npm install perspective-api-client
```

See the docs [on the project's GitHub page](https://github.com/sloria/perspective-api-client).

## Related research
Perspective is part of the [Conversation-AI research project](https://conversationai.github.io/). You can email your research-related questions to conversationai-questions@google.com.

## Support
For Perspective support questions and to contact us, see: https://support.perspectiveapi.com/.


## Privacy and Terms of Service

The Perspective API is provided under the [Google Privacy Policy](https://www.google.com/intl/en/policies/privacy/), and the [Google Cloud API terms of service](https://www.google.com/intl/en/policies/terms/).
