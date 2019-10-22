[Back to Conversation AI Overview](https://conversationai.github.io/) | [Back to Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md)

# Perspective API reference

 * [Using the API](#using-the-api)
 * [Key concepts](key-concepts.md)
 * [Models](#production-and-experimental-models)
 * [Methods](#api-methods)
   * [Scoring comments](#scoring-comments-analyzecomment)
   * [Sending feedback](#sending-feedback-suggestcommentscore)
 * [API client libraries](#api-client-libraries)
 * [Privacy and Terms of Service](#privacy-and-terms-of-service)

## Using the API

First, follow the [quickstart guide](/get-started/README.md) to enable the API for your
project, and ensure you're able to make a successful request.

### Quota and character length limits

#### Quota limit

By default, we set the quota to 1 QPS for all Perspective projects.

Check your quota limits by going to [your google cloud project's Perspective API page](https://console.cloud.google.com/apis/api/commentanalyzer.googleapis.com/quotas), and check your project's quota usage at
[the cloud console quota usage page](https://console.cloud.google.com/iam-admin/quotas).

Visit the Perspective API Support page to [request a quota increase](https://support.perspectiveapi.com/s/request-quota-increase).

#### Character limit

The maximum text size per request is 3000 bytes.

## Support

For Perspective support questions and to contact us, see: https://support.perspectiveapi.com/.

