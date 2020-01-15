[Perspective API documentation](../README.md) > [API Reference Docs](README.md) > **Limits**

# Limits and errors

The Perspective API uses limits and quotas to protect the system from receiving more data than it can handle, and to ensure equitable distribution of the system resources. These limits and quotas are subject to change.

You may encounter an error if your request exceeds the limit.

## Quota limit

By default, we set the quota to 1 QPS for all Perspective projects.

Check your quota limits by going to [your Google Cloud project's Perspective API page](https://console.cloud.google.com/apis/api/commentanalyzer.googleapis.com/quotas), and check your project's quota usage at
[the cloud console quota usage page](https://console.cloud.google.com/iam-admin/quotas).

Visit the Perspective API Support page to [request a quota increase](https://support.perspectiveapi.com/s/request-quota-increase).

## Character limit for requests

The maximum text size per request is 3000 bytes.

## All reference materials

Read more about the Perspective API and how to use it.

* [Key concepts](key-concepts.md)
* [Attributes](models.md)
   * [Attribute cards](model-cards/README.md)
* [Methods](methods.md)
   * [Scoring comments](methods.md#scoring-comments-analyzecomment)
   * [Sending feedback](methods.md#sending-feedback-suggestcommentscore)
* [API client libraries](clients.md)
* **Limits and errors**
