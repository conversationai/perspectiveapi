# Perspective Comment Analyzer API

The Perspective API is part of the
[Conversation AI](https://conversationai.github.io) research effort that
aims to help increase empathy, participation, and quality in online
conversation at scale.

This GitHub repository contains a [quickstart guide](quickstart.md) and the [API
reference documentation](api_reference.md) for the Perspective Comment Analyzer
API.

Example demo code:

 * [A simple server](https://github.com/conversationai/perspectiveapi-simple-server)
   that can hold your API key and access the Perspective API.
 * [An example of an authorship
   experience](https://github.com/conversationai/perspectiveapi-authorship-demo)
   gives an author feedback as they type.
 * [A proxy to the API](https://github.com/conversationai/perspectiveapi-proxy)
   with access restrictions and a simple UI to debug calls to the API. 
 * [Conversation AI - Moderator](https://github.com/conversationai/conversationai-moderator) 
   a comment moderation system that provide hint and assist UI for moderators based 
   on a plugable model of computational assistants, including support for using 
   Perspective API models. There are also plugins to support moderation of different platforms, e.g.:
   * [plugin for Discourse](https://github.com/conversationai/conversationai-moderator-discourse)
   * [plugin for Wordpress](https://github.com/conversationai/conversationai-moderator-wordpress)
   * [plugin for Reddit](https://github.com/conversationai/conversationai-moderator-reddit)
     (incomplete, does not yet support actions)

If you would like to receive email updates about the API - for example when we
add new models, or deprecate old ones - you can subscribe to
[perspective-announce](https://groups.google.com/forum/#!forum/perspective-announce/join). You will
then receive email updates from perspective-announce@googlegroups.com.
This list will be used only to share release information, and will never be
used to ask you login details of any kind. For support and to contact us, see: https://support.perspectiveapi.com/. 

The Perspective API is provided under the [Google Privacy Policy](https://www.google.com/intl/en/policies/privacy/), and the [Google Cloud API terms of service](https://www.google.com/intl/en/policies/terms/).

Users can leverage the ‘DoNotStore’ flag to ensure that all submitted comments are automatically deleted after scores are returned and/or the ‘SuggestCommentScore’ method to submit corrections to improve Perspective over time.
