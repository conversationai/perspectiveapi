# Perspective Comment Analyzer API documentation

<img align="right" src="img/logo.png" alt="Perspective API logo" />The Perspective API is part of the [Conversation AI](https://conversationai.github.io) research effort that
aims to help increase empathy, participation, and quality in online conversation at scale.

This repository contains the necessary documentation to start using the Perspective Comment Analyzer API. 

**NOTE**: While there are example calls to the API and demos in this repository, the code for the API is not open source.

## Using Perspective API

1. [Get started with Perspective API](1-get-started/)
   + [About](1-get-started/about.md)
   + [Sample requests](1-get-started/sample.md)
   + [Support](1-get-started/support.md)
1. [API Reference](2-api/)
   + [Key concepts](2-api/key-concepts)
   + [Clients](2-api/clients.md)
   + [Models and attributes](2-api/models.md)
      + [Model cards](2-api/model-cards/README.md)
   + [Methods](2-api/methods.md)
   + [Limits and errors](2-api/limits.md)
1. [Concepts](3-concepts/)
   + [Score normalizaion guide](3-concepts/score-normalization.md)
1. [Case studies](4-case-studies/)
   + [The New York Times](4-case-studies/nyt.md)
1. [Contribution guidelines](5-contribute/)
   + [How to label data](5-contribute/label-data.md)
   + [Privacy](5-contribute/privacy.md)
1. [Contact us](6-contact/)

Download the [example data CSV](example_data/perspective_wikipedia_2k_score_sample_20180829.csv).

### Releases and updates

#### Wednesday, August 23, 2017

[Perspective API score normalization: fixes for Toxicity](releases/20170823-score_normalization_v2.md)

#### Tuesday, June 13, 2017
[Perspective API score normalization change](releases/20170613-score_normalization_v1.md)

### Improve the API

Help improve the Perspective API by leveraging the `DoNotStore` flag to ensure that all submitted
comments are automatically deleted after scores are returned and/or the `SuggestCommentScore` method 
to submit corrections.

## About this project

Perspective was created by Jigsaw and Google’s Counter Abuse Technology team in a collaborative research project called [Conversation-AI](https://conversationai.github.io/). We open source experiments, models, and research data to explore the strengths and weaknesses of ML as a tool for online discussion.

You can email your research-related questions to [conversationai-questions@google.com](mailto:conversationai-questions@google.com).

![Jigsaw logo](img/jigsaw-logo.jpg)

## Privacy and Terms of Service

The Perspective API is provided under the [Google Privacy Policy](https://www.google.com/intl/en/policies/privacy/),
and the [Google Cloud API terms of service](https://www.google.com/intl/en/policies/terms/).
