[Perspective API documentation](../README.md) > [API Reference Docs](README.md) > **Methods**

# API Methods

A method is a procedure associating a message (or request) with an object (which consists of data and behavior). Once run, a method returns a new object.

There are two methods available for Perspective API, where each method is a different type of request a user can send:

+ [`AnalyzeComment`](#scoring-comments-analyzecomment), where a user sends a request for a comment to be analyzed, and a score is returned
+ [`SuggestCommentScore`](#sending-feedback-suggestcommentscore), where a user can suggest a better score for a comment

## Scoring comments: `AnalyzeComment`

To send a comment scoring request to the API, post a request object to this endpoint:

```
https://commentanalyzer.googleapis.com/v1alpha1/comments:analyze
```

If you're using API key authentication, append `?key=YOUR_API_KEY` to the end of the request. See the [get started guide](../1-get-started/README.md) for an example.

### `AnalyzeComment` request

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

| Field | Description |
| ----- | ----------- |
| `comment.text` | **(required)** The text to score. This is assumed to be utf8 raw text of the text to be checked. Emoji and other non-ascii characters can be included (HTML will probably result in lower performance). |
| `comment.type` | *(optional)* The text type of `comment.text`. Either `"PLAIN_TEXT"` or `"HTML"`. Currently only `"PLAIN_TEXT"` is supported.
| `context.entries` | *(optional)* A list of objects providing the context for `comment`. Currently not supported by the API. |
| `context.entries[].text` | *(optional)* The text of a context object. The maximum size of context entry is 1MB. |
| `context.entries[].type` | *(optional)* The text type of the corresponding context text. Same type as `comment.text`. Currently only `"PLAIN TEXT"` is supported. |
| `requestedAttributes`    | **(required)** A map from attribute name to a configuration object. See the [attributes section](models.md#all-attribute-types) for a list of available attribute names. If no configuration options are specified, defaults are used, so the empty object `{}` is a valid (and common) choice. You can specify multiple attribute names here to get scores from multiple attributes in a single request. |
| `requestedAttributes[name].scoreType` | *(optional)* The score type returned for this attribute. Currently, only `"PROBABILITY"` is supported. Probability scores are in the range `[0,1]`. |
| `requestedAttributes[name].scoreThreshold` | *(optional)* The API won't return scores that are below this threshold for this attribute. By default, all scores are returned. |
| `spanAnnotations` | *(optional)* A boolean value that indicates if the request should return spans that describe the scores for each part of the text (currently done at per-sentence level). Defaults to false. |
| `languages` | *(optional)* A list of [ISO 631-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) two-letter language codes specifying the language(s) that `comment` is in (for example, `"en"`, `"es"`, `"fr"`, `"de"`, etc). If unspecified, the API will auto-detect the comment language. If language detection fails, the API returns an error. **Note:** You can find languages currrently supported [here](models.md). There is no simple way to use the API across languages with production support and languages with experimental support only. |
| `doNotStore` | *(optional)* Whether the API is permitted to store `comment` and `context` from this request. Stored comments will be used for future research and community attribute building purposes to improve the API over time. We also plan to provide dashboards and automated analysis of the comments submitted, which will apply only to those stored. Defaults to false (request data may be stored). **Warning**: This should be set to true if data being submitted is private (i.e. not publicly accessible), or if the data submitted contains content written by someone under 13 years old. |
| `clientToken` | *(optional)* An opaque token that is echoed back in the response. |
| `sessionId` | *(optional)* An opaque session ID. This should be set for authorship experiences by the client side so that groups of requests can be grouped together into a session. This should not be used for any user-specific id. This is intended for abuse protection and individual sessions of interaction. |
| `suggestCommentScore` | *(optional)* Used to notify the Perspective API team of specific biases, in order to help us improve our attribute. Many kinds of toxic language are disproportionately represented in our dataset, which leads to some obviously incorrect scores, as well as unintended biases. Use this method to help us correct them. |

Note that only `comment.text` and `requestedAttributes` are required.

### `AnalyzeComment` response

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

| Field | Description |
| ----- | ----------- |
| `attributeScores` | A map from attribute name to per-attribute score objects. The attribute names will mirror the request's `requestedAttributes`.
| `attributeScores[name].summaryScore.value` | The attribute summary score for the entire comment. All attributes will return a `summaryScore` (unless the request specified a `scoreThreshold` for the attribute that the `summaryScore` did not exceed). |
| `attributeScores[name].summaryScore.type` | This mirrors the requested `scoreType` for this attribute. |
| `attributeScores[name].spanScores` | A list of per-span scores for this attribute. These scores apply to different parts of the request's `comment.text`. **Note:** Some attributes may not return `spanScores` at all. |
| `attributeScores[name].spanScores[].begin` | Beginning of the text span in the request comment. |
| `attributeScores[name].spanScores[].end` | End of the text span in the request comment. |
| `attributeScores[name].spanScores[].score.value` | The attribute score for the span delimited by `begin` and `end`. |
| `attributeScores[name].spanScores[].score.type` | Same as `summaryScore.type`. |
| `languages` | Mirrors the request's `languages`. If no languages were specified, the API returns the auto-detected language. |
| `clientToken` | Mirrors the request's `clientToken`. |

### `AnalyzeComment` example

This is a request for the `TOXICITY` and `UNSUBSTANTIAL` attributes for a comment that's explicitly in English.

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
 
The response contains the `TOXICITY` and `UNSUBSTANTIAL` attribute scores. Each attribute has a single overall `summaryScore` as well as two `spanScores`.

Both attributes return the same spans in this case: the span `[0,31)` (corresponding to "What kind of idiot name is foo?") and the span `[32,56)` (corresponding to "Sorry, I like your name."). However, attributes may not always return the same spans.

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

## Sending feedback: `SuggestCommentScore`

The `SuggestCommentScore` endpoints submits feedback to the API in the form of a
suggested score. You can use this method if you disagree with a score and would
like to improve the attribute. All submissions to `SuggestCommentScore` are stored
and used to improve the API and related services. This method should **not** be
used for private data (i.e., for data that is not accessible publicly), or if the
data submitted contains content written by someone under 13 years old.

To send a suggested score to the API, post a request object to this endpoint:
```
https://commentanalyzer.googleapis.com/v1alpha1/comments:suggestscore
```
### `SuggestCommentScore` request

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

| Field | Description |
| ----- | ----------- |
| `comment`      | **(required)** Same as `AnalyzeComment` request. |
| `context`      | *(optional)* Same as `AnalyzeComment` request. |
| `attributeScores` | Similar to `AnalyzeComment` response. This holds the attribute scores that the client believes the comment should have. It has the same format as the `attributeScores` field in the `AnalyzeComment` response, as it's what the client believes is the correct "answer" for what this comment should be scored as. The client can specify just summary scores, just span scores, or both. |
| `languages`    | *(optional)* Same as `AnalyzeComment` request. |
| `communityId`  | *(optional)* Opaque identifier associating this score suggestion with a particular community. If set, this field allows us to differentiate suggestions from different communities, as each community may have different norms. |
| `clientToken`  | An opaque token that is echoed back in the response. |

#### `SuggestCommentScore` response

```
{
  "clientToken": string
}
```

| Field | Description |
| ----- | ----------- |
| `clientToken` | Mirrors the request's `clientToken`. |

### `SuggestCommentScore` example

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

## All reference materials

Read more about the Perspective API and how to use it.

* [Key concepts](key-concepts.md)
* [Attributes](models.md)
   * [Model cards](model-cards/README.md)
* **Methods**
   * [Scoring comments](methods.md#scoring-comments-analyzecomment)
   * [Sending feedback](methods.md#sending-feedback-suggestcommentscore)
* [API client libraries](clients.md)
* [Limits and errors](limits.md)

