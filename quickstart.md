[Back to Conversation AI Overview](https://conversationai.github.io/) | [Back to Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md)

# Perspective API Quickstart

1. You'll need a **Google Cloud project** to authenticate (but not necessarily host) your API requests. Go to the [Google Cloud console](https://console.developers.google.com/) and either use an existing project, or follow these steps to create a new one:

    1. Sign in with your Google account, if necessary.
    1. Click Create, or click the "Project" drop-down at the top of the page and then click **_New Project_**.
    1. Name the project.
    1. Click _Create_ again.
    
   The project is now included in the "Project" drop-down at the top of the page.

1. **Enable the API.** 
    1. Command line:
       `gcloud services enable commentanalyzer.googleapis.com`
       
       OR
       
    1. Web UI: navigate to the [Perspective API's overview page](https://console.developers.google.com/apis/api/commentanalyzer.googleapis.com/overview) and click **_Enable_**.
      
1. **Generate an API key.** To authenticate your requests, you'll need to generate credentials for your project. Using an API key is the simplest option. Go to the [API credentials page](https://console.developers.google.com/apis/credentials), click **_Create credentials_**, and choose "API Key".

    *Warning*: If you make requests from a client-side language like JavaScript, your API key will be exposed to all visitors. It's strongly recommended that you [add key restrictions](https://cloud.google.com/docs/authentication/api-keys#api_key_restrictions) so that only your production server can use that key.
    
    Note that it typically takes only a few minutes for a new API key to have access after the API is enabled, but it can on occasion take up to an hour; until the API key is enabled, you may get errors of the form "API Key not found. Please pass a valid API key".

1. **Make an AnalyzeComment request.**

    Use the API key you generated in the previous step as the `key` param in this curl command:

    ```shell
    $ curl -H "Content-Type: application/json" --data \
        '{comment: {text: "what kind of idiot name is foo?"},
          languages: ["en"],
          requestedAttributes: {TOXICITY:{}} }' \
        https://commentanalyzer.googleapis.com/v1alpha1/comments:analyze?key=YOUR_KEY_HERE
    ```
        
    You should see output similar to this:

    ```shell
    {
      "attributeScores": {
        "TOXICITY": {
          "summaryScore": {
            "value": 0.9014498,
            "type": "PROBABILITY"
          }
        }
      },
      "languages": [
        "en"
      ]
    }
    ```

    The curl command issued an API request to analyze the `comment.text` field for the `requestedAttributes`, in this case the `TOXICITY` model.

    In the response, the field `attributeScores.TOXICITY.summaryScore.value` gives the toxicity model's score for the comment. In this case, the comment got a 0.9 out of 1.0. A less mean-spirited comment should get a lower score.
    
Users can leverage the ‘DoNotStore’ flag to ensure that all submitted comments are automatically deleted after scores are returned and/or the ‘SuggestCommentScore’ method to submit corrections to improve Perspective over time.  

See the [API reference documentation](api_reference.md) for details on all of
the request and response fields, as well as the available values for
`requestedAttributes`. There are quite a few [experimental models](https://github.com/conversationai/perspectiveapi/blob/master/api_reference.md#models), such as "obscene", "attack on a commenter", "spam", etc, that you may find interesting.

Also, subscribe to our [perspectiveapi-announce@ Google Group](https://groups.google.com/forum/#!forum/perspective-announce/join) to get notified when we make changes to the API.

For support and to contact us, visit our [support site](https://support.perspectiveapi.com). 
