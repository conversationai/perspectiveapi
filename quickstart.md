[Back to Conversation AI Overview](https://conversationai.github.io/) | [Back to Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md)

# Perspective API Quickstart

## Prerequisites

You'll need a Google Cloud project to authenticate (but not necessarily host) your API requests. Go to the [Google Cloud console](https://console.developers.google.com/) and either use an existing project, or follow these steps to create a new one:

1. Sign in with your Google account, if necessary.

1. Click **Create**, or click the "Project" drop-down at the top of the page and then click **New Project**.

1. Name the project.

1. Click **Create** again. The project is now included in the "Project" drop-down at the top of the page.

## Enable the API

1. Enable the API via command line or the web UI.
    1. Command line:
       `gcloud services enable commentanalyzer.googleapis.com`
    1. Web UI: navigate to the [Perspective API's overview page](https://console.developers.google.com/apis/api/commentanalyzer.googleapis.com/overview) and click **Enable**.

1. Generate an API key to authenticate your requests.
   
   Go to the [API credentials page](https://console.developers.google.com/apis/credentials), click **Create credentials**, and choose "API Key".

   > **Warning**: If you make requests from a client-side language like JavaScript, your API key will be exposed to all visitors. We strongly recommend that you [add key restrictions](https://cloud.google.com/docs/authentication/api-keys#api_key_restrictions) so that only your production server can use that key.
	
   Note that it typically takes only a few minutes for a new API key to have access after the API is enabled, but it can on occasion take up to an hour. Until the API key is enabled, you may get errors of the form "API Key not found. Please pass a valid API key."

## Make an `AnalyzeComment` request
   
Run one of the sample API calls below to get scores directly from Perspective API models. You don’t need to build a model locally. 
   
The `AnalyzeComment` command issues an API request to analyze the `comment.text` field for the `requestedAttributes`, in this case the `TOXICITY` model. Use the API key you generated above as the `key` parameter.

Leverage the `DoNotStore` flag to ensure that all submitted comments are automatically deleted after scores are returned and/or the `SuggestCommentScore` method to submit corrections to improve Perspective over time.

Read the [API reference documentation](api_reference.md) for details on all of the request and response fields, as well as the available values for `requestedAttributes`. There are [experimental models](https://github.com/conversationai/perspectiveapi/blob/master/api_reference.md#models), such as "obscene", "attack on a commenter", "spam", etc., that you may also use.

### Using cURL

Make an `AnalyzeComment` request with cURL. The following command should work for most Mac and Linux users. You may need to install cURL to run this command.
   
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

## Stay updated

Subscribe to our [perspectiveapi-announce@ Google Group](https://groups.google.com/forum/#!forum/perspective-announce/join) to get notified when we make changes to the API.

For support and to contact us, visit our [support site](https://support.perspectiveapi.com). 
