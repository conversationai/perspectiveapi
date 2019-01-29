# Toxicity 
Toxicity classifies rude, disrespectful, or unreasonable comment that is likely to make people leave a discussion. This model is a Convolutional Neural Network (CNN) trained with word-vector inputs. You can also train your own deep CNN for text classification on our public toxicity dataset, and explore our open-source model training tools to train your own models.


## Overview

![](https://github.com/conversationai/perspectiveapi/blob/lucy-model-card/model_cards/auc_wipd.png)



## Intended use


#### Human-assisted moderation
Make moderation easier with an ML assisted tool that helps prioritize comments for moderation, and create custom tasks for automated actions.
&nbsp;

#### Author feedback
Assist authors in real-time when their comments might violate your community guidelines or be may be perceived as “Toxic” to the conversation. Use simple feedback tools when the assistant gets it wrong.
&nbsp;

#### Read better comments
Organize comments on topics that are often difficult to discuss online. Build new tools that help people explore the conversation.
&nbsp;


## Uses to avoid

#### Fully automated moderation
Make moderation easier with an ML assisted tool that helps prioritize comments for moderation, and create custom tasks for automated actions.
&nbsp;

#### Character judgement
This model only helps detect Toxicity in what a person said, and is not intended to detect anything about the individual who said it.
&nbsp;



## Model details

#### Training data
Proprietary from Perspective API, which includes comments from a online forums such as Wikipedia and New York Times, with crowdsourced labels of whether the comment is “toxic”, defined as “a rude, disrespectful, or unreasonable comment that is likely to make people leave a discussion”.

#### Values
Community, Transparency, Inclusivity, Privacy, and Topic neutrality. Because of privacy considerations, the model does not take into account user history when making judgments about toxicity.
&nbsp;


## Evaluation data

#### Overall evaluation data
The overall evaluation result (shown above) is calculated using the held out test set associated with the training set for the specific model. Note that this means that each new model version is likely to have a different training and testing set, so overall results are not directly comparable across models.
&nbsp;

#### Unintended bias evaluation data
The unintended bias evaluation result is calculated using a synthetically generated test set where a range of identity terms are swapped into template sentences, both toxic and non-toxic. Results are presented grouped by identity term. Note that this evaluation looks at only the identity terms present in the text, not the identities of comment authors or readers.
&nbsp;

#### Group factors
Identity terms referencing frequently attacked groups, focusing on sexual orientation, gender identity, and race.
&nbsp;

#### Caveats
Synthetic test data covers only a small set of very specific comments and identities. While these are designed to be representative of common use cases and concerns, it is not comprehensive.
&nbsp;

## Unitary Identity Subgroup Evaluation
To measure unintended bias, we calculate three separate ROC-AUC results for each identity. Each result captures a different type of unintended bias and each is calculated by restricting the data set to different subsets:

| Test set   | Description                         |
|----------------|-------------------------------|
|Subgroup AUC|Here, we restrict the data set to only the examples that mention the specific identity subgroup. A low value in this metric means the model does a poor job of distinguishing between toxic and non-toxic comments that mention the identity.
|BPSN AUC         |Here, we restrict the test set to the non-toxic examples that mention the identity and the toxic examples that do not. A low value in this metric means that the model confuses non-toxic examples that mention the identity with toxic examples that do not, likely meaning that the model predicts higher toxicity scores than it should for non-toxic examples mentioning the identity.  
|BNSP AUC         |Here, we restrict the test set to the toxic examples that mention the identity and the non-toxic examples that do not. A low value here means that the model confuses toxic examples that mention the identity with non-toxic examples that do not, likely meaning that the model predicts lower toxicity scores than it should for toxic examples mentioning the identity.|

[See our full results for our Toxicity models here, including results for more identity terms and more intersectional results.](https://docs.google.com/spreadsheets/d/13edevE6WQLhEQ7r3nY4Z1leJZ-M5BbO_4UUQwc33Hr4/edit?usp=sharing)&nbsp;
![](https://github.com/conversationai/perspectiveapi/blob/lucy-model-card/model_cards/1f.png)


## Intersectional Identity Subgroup Evaluation

![](https://github.com/conversationai/perspectiveapi/blob/lucy-model-card/model_cards/1g.png)


#### Get involved
If you have any questions, feedback, or additional things you'd like to see in the model card,
[please reach out to us at here.](https://docs.google.com/forms/d/e/1FAIpQLScgwNY8PAsVxwYRSknUUHBU2Lai85rqeOuD17lTDWmDEUqq3Q/viewform)

