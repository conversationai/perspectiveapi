[Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md) > [Contribution guidelines](README.md) > **Labeled data**

# Contributing labeled data

Perspective API is built on a multitude of data sources from across the internet,
but you can also contribute data from your own community.

### Why contribute labeled data

Submitting labeled data lets the Perspective API team train the models on more
comments, and makes it possible for the API to improve and learn from your
particular use-case.

### What types of datasets are useful?

A useful dataset is either very large or has high-quality, distributed labels.

**Important note**: Please do not include any personally identifiable information
(i.e. names, usernames, email addresses, etc.) in the datasets you share.

#### Large datasets

Datasets with more than 100,000 comments with labels or datasets with more than
1 million comments without labels.

#### Labeled datasets

If sharing a labeled dataset, it must have:

+ A good quantity and distribution of labels. This includes at least 20,000
examples of labels being looked for (e.g. toxic comments or rejected comments).
Having 100,000 different labels which only occur once is not useful.
+ High agreement with a professional reviewer. Have someone on your team or a
professional re-review the labels for 100 examples. For the data to be useful,
the re-review should agree with the original labeling more than 75% of the time.

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
| `community_id` | unique id for community or section (e.g. health, news, tech) |
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
