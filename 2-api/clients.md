[Perspective API documentation](../README.md) > [API Reference Docs](README.md) > **Client libraries**

# API client libraries

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

## All reference materials

Read more about the Perspective API and how to use it.

* [Key concepts](key-concepts.md)
* [Attributes](models.md)
   * [Attribute cards](model-cards/README.md)
* [Methods](methods.md)
   * [Scoring comments](methods.md#scoring-comments-analyzecomment)
   * [Sending feedback](methods.md#sending-feedback-suggestcommentscore)
* **API client libraries**
* [Limits and errors](limits.md)
