# Perspective Comment Analyzer API

The Perspective API is part of the [Conversation AI](https://conversationai.github.io) research effort that aims to help increase empathy, participation, and quality in online conversation at scale.

This repository contains the necessary documentation to start using the Perspective Comment Analyzer API.

## Using Perspective API

+ [Get started with Perspective API](quickstart.md)
+ [Glossary](glossary.md)
+ [Score normalizaion guide](score_normalization.md)
+ [API reference](api_reference.md)
+ [Contribution guidelines](CONTRIBUTING.md)

Download the [example data CSV](/example_data/perspective_wikipedia_2k_score_sample_20180829.csv).

Help improve the Perspective API by leveraging the `DoNotStore` flag to ensure that all submitted comments are automatically deleted after scores are returned and/or the `SuggestCommentScore` method to submit corrections.

### Demos

Example demo code:

+ [A simple server](https://github.com/conversationai/perspectiveapi-simple-server) that can hold your API key and access the Perspective API.
+ [An example of an authorship experience](https://github.com/conversationai/perspectiveapi-authorship-demo) gives an author feedback as they type.
+ [A proxy to the API](https://github.com/conversationai/perspectiveapi-proxy) with access restrictions and a simple UI to debug calls to the API. 
+ [Conversation AI - Moderator](https://github.com/conversationai/conversationai-moderator) a comment moderation system that provide hint and assist UI for moderators based on a plugable model of computational assistants, including support for using Perspective API models. There are also plugins to support moderation of different platforms, e.g.:
   + [Discourse plugin](https://github.com/conversationai/conversationai-moderator-discourse)
   + [WordPress plugin](https://github.com/conversationai/conversationai-moderator-wordpress)
   + [Reddit plugin](https://github.com/conversationai/conversationai-moderator-reddit) &ndash; incomplete, as it does not yet support actions

## About this project

If you would like to receive email updates about the API&mdash;for example when we add new models, or deprecate old ones&mdash;you can subscribe to the [perspective-announce Google Group](https://groups.google.com/forum/#!forum/perspective-announce/join). You will receive email updates from perspective-announce@googlegroups.com. This list will be used only to share release information and will never be used to ask you login details of any kind.

For support and to contact us, visit [support.perspectiveapi.com](https://support.perspectiveapi.com/). 

The Perspective API is provided under the [Google Privacy Policy](https://www.google.com/intl/en/policies/privacy/), and the [Google Cloud API terms of service](https://www.google.com/intl/en/policies/terms/).


