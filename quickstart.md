[Back to Conversation AI Overview](https://conversationai.github.io/) | [Back to Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md)

# Perspective API Quickstart

1.  **Create a Google Cloud project.** Go to the [Google Cloud console](https://console.developers.google.com/) to create a new project. You can also use an existing project, if you have one.

    *Note*: Your application doesn't need to be *hosted* on Google Cloud, but you will still need a Google Cloud project to authenticate your API requests.

2.  **Enable the API.** Go to the [Perspective API's overview page](https://console.developers.google.com/apis/api/commentanalyzer.googleapis.com/overview) and click **_Enable_**.
    
4.  **Generate an API key.** To authenticate your requests, you'll need to generate credentials for your project. Using an API key is the simplest option. Go to the [API credentials page](https://console.developers.google.com/apis/credentials), click **_Create credentials_**, and choose "API Key".

    *Warning*: If you make requests from a client-side language like JavaScript, your API key will be exposed to all visitors. It's strongly recommended that you [proxy the request through a server](https://github.com/conversationai/perspectiveapi-proxy), so that the key is hidden from browsers. Adding restrictions to the key in the Cloud console will not work, because the requests will come from arbitrary IP addresses, and the referer headers can be spoofed by abusers. Proxying the request is the only way to protect the key.
    
    Note that it typically takes only a few minutes for a new API key to have access after the API is enabled, but it can on occasion take up to an hour; until the API key is enabled, you may get errors of the form "API Key not found. Please pass a valid API key".

5.  **Make an AnalyzeComment request.**

    Use the API key you generated in the previous step as the `key` param in this curl command:

    ```shell
    $ curl -H "Content-Type: application/json" --data \
        '{comment: {text: "what kind of idiot name is foo?"},
          languages: ["en"],
          requestedAttributes: {TOXICITY:{}} }' \
        https://commentanalyzer.googleapis.com/v1alpha1/comments:analyze?key=YOUR_KEY_HERE
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
