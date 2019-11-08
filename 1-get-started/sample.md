[Perspective API documentation](../README.md) > [Get Started](README.md) > **Sample requests**

# Sample requests

## Make an `AnalyzeComment` request
   
Run one of the sample API calls below to get scores directly from Perspective API models. You don’t need to build a model locally. 
   
The `AnalyzeComment` command issues an API request to analyze the `comment.text` field for the `requestedAttributes`, in this case the `TOXICITY` model. Use the API key you generated above as the `key` parameter.

Leverage the `DoNotStore` flag to ensure that all submitted comments are automatically deleted after scores are returned and/or the `SuggestCommentScore` method to submit corrections to improve Perspective over time.

Read the [API reference documentation](api_reference.md) for details on all of the request and response fields, as well as the available values for `requestedAttributes`. There are [experimental models](https://github.com/conversationai/perspectiveapi/blob/master/api_reference.md#models), such as "obscene", "attack on a commenter", "spam", etc., that you may also use.

### Using cURL

Make an `AnalyzeComment` request with cURL. The following command should work for most Mac and Linux users. You may need to install cURL to run this command.

Replace `YOUR_KEY_HERE` with your API key.
   
   ```shell
   $ curl -H "Content-Type: application/json" --data \
       '{comment: {text: "what kind of idiot name is foo?"},
          languages: ["en"],
          requestedAttributes: {TOXICITY:{}} }' \
       https://commentanalyzer.googleapis.com/v1alpha1/comments:analyze?key=YOUR_KEY_HERE
   ```

In the following response, the field `attributeScores.TOXICITY.summaryScore.value` gives the toxicity model's score for the comment. The comment received a score of 0.9 out of 1.0.

   ```shell
   {
      "attributeScores": {
         "TOXICITY": {
            "summaryScore": {
               "value": 0.9208521,
               "type": "PROBABILITY"
            }
         }
      },
      "languages": [
         "en"
      ]
   }
   ```

Learn more about model attribute scores the ["Key concepts" section of our API reference](api_reference.md#key-concepts).

### Using Python

Make an `AnalyzeComment` request with Python.

   ```shell
   import json 
   import requests 
   api_key = 'YOUR_KEY_HERE'
   url = ('https://commentanalyzer.googleapis.com/v1alpha1/comments:analyze' +    
       '?key=' + api_key)
   data_dict = {
       'comment': {'text': 'what kind of idiot name is foo?'},
       'languages': ['en'],
       'requestedAttributes': {'TOXICITY': {}}
   }
   response = requests.post(url=url, data=json.dumps(data_dict)) 
   response_dict = json.loads(response.content) 
   print(json.dumps(response_dict, indent=2))
   ```

You should see output similar to this:

   ```shell
   {
      "attributeScores": {
         "TOXICITY": {
            "summaryScore": {
               "value": 0.9208521,
               "type": "PROBABILITY"
            }
         }
      },
      "languages": [
         "en"
      ]
   }
   ```
   
### Using Node.js

To use Node.js, you must have installed `npm` and the
[`googleapis`](https://github.com/google/google-api-nodejs-client/) client:

```shell
npm install googleapis
```

Make an `AnalyzeComment` with Node.js:

```javascript
var googleapis = require('googleapis');

API_KEY = 'YOUR_KEY_HERE'
DISCOVERY_URL = 'https://commentanalyzer.googleapis.com/$discovery/rest?version=v1alpha1'

googleapis.discoverAPI(DISCOVERY_URL, (err, client) => {
  if (err) throw err;
  var analyzeRequest = {
    comment: {text: 'what kind of idiot name is foo?'},
    requestedAttributes: {'TOXICITY': {}}
  };
  client.comments.analyze({key: API_KEY, resource: analyzeRequest}, (err, response) => {
    if (err) throw err;
    console.log(JSON.stringify(response, null, 2));
  });
});
```

You should see output similar to this:

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
