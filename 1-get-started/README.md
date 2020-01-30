[Perspective API documentation](../README.md) > **Get Started**

# Get started with Perspective API

Perspective API uses machine learning models to score the perceived impact a comment might have on a conversation. Developers and publishers can use this score to give realtime feedback to commenters or help moderators do their job, or allow readers to more easily find relevant information.

## Prerequisites

You need a Google Cloud project to authenticate (but not necessarily host) your API requests. Go to the [Google Cloud console](https://console.developers.google.com/) and use an existing project or follow these steps to create a new one:

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

## What's next?

+ [About the API](about.md)
+ [Sample requests](sample.md)
+ [Support](support.md)
