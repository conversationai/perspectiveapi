[Back to Conversation AI Overview](https://conversationai.github.io/) | [Back to Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md)

# Perspective API Quickstart

## Prerequisites

You'll need a Google Cloud project to authenticate (but not host) your API requests. Visit the [Google Cloud console](https://console.developers.google.com/) and either use an existing project (if you have one), or follow these steps to create a new project:

1. Sign in with your Google account, if necessary.

1. Click the "Project" drop-down at the top of the page and then click **New Project**.

1. Create a "Project name"

1. Choose the parent location on Google Cloud for this project.

1. Click **Create**. The project is now included in the "Project" drop-down at the top of the page.

## Enable the API

1. Enable the API via command line or the web UI.
    1. Command line:
       `gcloud services enable commentanalyzer.googleapis.com`
    1. Web UI: navigate to the [Perspective API's overview page](https://console.developers.google.com/apis/api/commentanalyzer.googleapis.com/overview) and click **Enable**.

1. Authenticate your requests. Although there are multiple ways to authenticate your API requests, we provide guidance for two: creating a service account (recommended) or generating an API key (may be faster).
   + _Create a service account (recommended)._ Create a Google account which represents an application. This provides flexibility of authentication across programming languages, platforms, and use cases:
      1. Go to the [API credentials page](https://console.developers.google.com/apis/credentials), click **Create credentials** and choose "Service account key".
	  1. (Optional) For more information about which selections to make when setting up the service account or about how to use the command line, visit [Getting Started with Authentication](//cloud.google.com/docs/authentication/getting-started).
   + _Generate an API key (may be faster)._ This option may be best if you are new to working with APIs or want to test the Perspective API.
      + **Warning**: If you make requests from a client-side language like JavaScript, your API key will be exposed to all visitors. We strongly recommend that you [add key restrictions](https://cloud.google.com/docs/authentication/api-keys#api_key_restrictions) so that only your production server can use that key.
      + It typically takes only a few minutes for a new API key to have access after the API is enabled, but it can take up to an hour. Until the API key is enabled, you may get errors in the form of "API Key not found. Please pass a valid API key."

For information on all authentication options, visit [Cloud’s Authentication Overview](//cloud.google.com/docs/authentication/).

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

## Stay updated

Subscribe to our [perspectiveapi-announce@ Google Group](https://groups.google.com/forum/#!forum/perspective-announce/join) to get notified when we make changes to the API.

For support and to contact us, visit our [support site](https://support.perspectiveapi.com). 
