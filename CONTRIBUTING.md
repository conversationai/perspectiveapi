# How to contribute

We'd love to accept your patches and contributions to this project. There are
just a few small guidelines you need to follow.

## Contributor License Agreement

Contributions to this project must be accompanied by a Contributor License
Agreement. You (or your employer) retain the copyright to your contribution,
this simply gives us permission to use and redistribute your contributions as
part of the project. Head over to <https://cla.developers.google.com/> to see
your current agreements on file or to sign a new one.

You generally only need to submit a CLA once, so if you've already submitted one
(even if it was for a different project), you probably don't need to do it
again.

## Code reviews

All submissions, including submissions by project members, require review. We
use GitHub pull requests for this purpose. Consult [GitHub Help] for more
information on using pull requests.

[GitHub Help]: https://help.github.com/articles/about-pull-requests/

## Contributing labeled data

Perspective API is built on a multitude of data sources from across the internet,
but you can also contribute data from your own community.

### Why contribute labeled data

Submitting labeled data lets the Perspective API team train the models on more
comments, and makes it possible for the API to improve and learn from your
particular use-case. For instance, if Perspective isn't yet available in your
language, uploading data can help speed up the process of making models available
in your language.

### Where to contribute

Upload data using [this form](https://docs.google.com/forms/d/e/1FAIpQLScAivfFHiwq08JfsHuIkTbdECLK0nSmyBi4JMvaqDrom2aVQw/viewform?c=0&w=1)
to help make the API better. All data must be anonymized, and you can choose
to list or not list your organization as the source.

If you are already using Perspective and would like to send labeled data on an
ongoing basis or would like to send labeled data directly to the API instead of
in a batch upload, you can do so using the
[suggest comment score upload method](https://support.perspectiveapi.com/s/article/score-feedback).
 
### Formatting data for uploads

You can organize the data in many formats (CSV, JSON, even a spreadsheet) for
training by the API, but the ideal data format (particularly for large datasets)
is as a newline delimited JSON file. This file is also called JSON-lines, where
each line is a valid JSON entry. More info at [ndjson.org](https://ndjson.org).
 
While all you need are fields for `comment_text` and `labels`, having more
context can help you in the long run. For this reason, we recommend labeling
with some of the following fields:

| FIELD | DESCRIPTION |
| -- | -- |
| `source` | name of source/publication/section |
| `comment_id` | unique id for the comment |
| `article_id` | unique id for the article |
| `community_id`` | unique id for community or section (e.g. health, news, tech) |
| `parent_id` | null, or comment_id of parent in thread |
| `comment_text` | text of the comment |
| `labels` | list of strings of labels associated with this comment |

Labels can include rejection reasons like "toxic", "off-topic"; positive labels, e.g.
"editors-pick" etc; user-flags, e.g. "flagged-as-spam-by-user"; or anything else you
think adds information that could help make a conversation better by knowing.

As JSON-lines, this would look something like:
 
```json
{ "source": "politics chat", "article_id": "90163", "comment_author_id": "4acf39f1e2", "parent_id": "47210", "comment_text": "You are a stupid idiot", "comment_id": "47212", "labels": ["obscene"]}

{ "source": "politics chat", "article_id": "90163", "comment_author_id": "e9af5bb45", "parent_id": "47212", "comment_text": "You, are the real dummy here! fool!", "comment_id": "47213", "labels": ["personal_attack"]}
```

It may be helpful to have context for the comments too, e.g. the article the comment
is on. For example, add content to a file named `articles.json` with these fields:

| FIELD | DESCRIPTION |
| -- | -- |
| `source` | name of source/publication/section |
| `article_id` | unique id for the article |
| `article_title` | title of article |
| `article_text` | text of the article |
| `author` | name of the article author (helps identify comments that attack the author) |
