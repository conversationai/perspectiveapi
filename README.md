# Perspective Comment Analyzer API

The Perspective API is part of the [Conversation AI](https://conversationai.github.io) research effort that
aims to help increase empathy, participation, and quality in online conversation at scale.

This repository contains the necessary documentation to start using the Perspective Comment Analyzer API.

## Using Perspective API

+ [Get started with Perspective API](1-get-started/)
   + [About](1-get-started/about.md)
   + [Glossary](1-get-started/glossary.md)
   + [Demos](1-get-started/demo.md)
   + [Sample requests](1-get-started/sample.md)
   + [Support](1-get-started/support.md)
+ [API Reference](2-api/)
   + [Key concepts](2-api/key-concepts)
   + [Clients](2-api/clients.md)
   + [Models](2-api/models.md)
   + [Methods](2-api/methods.md)
   + [Language support](2-api/language.md)
   + [Limits and errors](2-api/limits.md)
+ [Concepts](3-concepts/)
   + [Score normalizaion guide](3-concepts/score-normalization.md)
+ [Case studies](4-case-studies/)
   + [The New York Times](4-case-studies/nyt.md)
+ [Contribution guidelines](5-contribute/)
   + [How to label data](5-contribute/label-data.md)
   + [Privacy](5-contribute/privacy.md)
+ [Contact us](6-contact/)

Download the [example data CSV](example_data/perspective_wikipedia_2k_score_sample_20180829.csv).

### Improve the API

Help improve the Perspective API by leveraging the `DoNotStore` flag to ensure that all submitted
comments are automatically deleted after scores are returned and/or the `SuggestCommentScore` method 
to submit corrections.

## Related research

Perspective is part of the [Conversation-AI research project](https://conversationai.github.io/). You can
email your research-related questions to [conversationai-questions@google.com](mailto:conversationai-questions@google.com).

## Privacy and Terms of Service

The Perspective API is provided under the [Google Privacy Policy](https://www.google.com/intl/en/policies/privacy/),
and the [Google Cloud API terms of service](https://www.google.com/intl/en/policies/terms/).
