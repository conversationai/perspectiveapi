# Toxicity 
The toxicity model classifies whether a comment is a rude, disrespectful, or unreasonable comment that is likely to make people leave a discussion.


## Overview

![](https://github.com/conversationai/perspectiveapi/blob/lucy-model-card/model_cards/auc_wipd.png)
The [ROC](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) curve for the current TOXICITY model (TOXICITY@6). This shows True Positive Rate (y-axis) vs. False Positive Rate (x-axis).


## Intended use


#### Human-assisted moderation
Make moderation easier with an ML assisted tool that helps prioritize comments for human moderation, and create custom tasks for automated actions. See our [moderator tool](https://github.com/conversationai/conversationai-moderator) as an example.
&nbsp;

#### Author feedback
Assist authors in real-time when their comments might violate your community guidelines or be may be perceived as “Toxic” to the conversation. Use simple feedback tools when the assistant gets it wrong. See our [authorship demo](https://github.com/conversationai/perspectiveapi-authorship-demo) as an example.
&nbsp;

#### Read better comments
Organize comments on topics that are often difficult to discuss online. Build new tools that help people explore the conversation. 
&nbsp;


## Uses to avoid

#### Fully automated moderation
Perspective is not intended to be used for fully automated moderation. Machine learning models will always make some mistakes, so it is essential to build in systems for humans to catch and correct those mistakes.  
&nbsp;

#### Character judgement
In order to maintain user privacy, the TOXICITY model only helps detect toxicity in an individual statement, and is not intended to detect anything about the individual who said it. In addition, Perspective does not use prior information about an individual to inform toxicity predictions.
&nbsp;



## Model details

#### Training data
Proprietary from Perspective API, which includes comments from online forums such as Wikipedia and New York Times, with crowdsourced labels of whether the comment is “toxic”, defined as “a rude, disrespectful, or unreasonable comment that is likely to make people leave a discussion”.

#### Model architecture
The model is a Convolutional Neural Network (CNN) trained with GloVe word embeddings, which are fine-tuned during training. You can also train your own deep CNN for text classification on our [public toxicity dataset](https://conversationai.github.io/), and explore our [open-source model training tools](https://github.com/conversationai/conversationai-models) to train your own models.

#### Values
[Community, Transparency, Inclusivity, Privacy, and Topic neutrality](https://conversationai.github.io/). These values guide our product and research decisions. 
&nbsp;


## Evaluation data

#### Overall evaluation data
The overall evaluation result (shown above) is calculated using the held out test set associated with the training set for the specific model. Note that this means that each new model version is likely to have a different training and testing set, so overall results are not directly comparable across models.
&nbsp;

#### Unintended bias evaluation data
The unintended bias evaluation result is calculated using a synthetically generated test set where a range of identity terms are swapped into template sentences, both toxic and non-toxic. Results are presented grouped by identity term. Note that this evaluation looks at only the identity terms present in the text. We do not look at the identities of comment authors or readers to protect the privacy of these users. 
&nbsp;

#### Group factors
Identity terms referencing frequently attacked groups, focusing on sexual orientation, gender identity, and race.
&nbsp;

#### Caveats
The current synthetic test data covers only a small set of very specific comments and identities. While these are designed to be representative of common use cases and concerns, it is not comprehensive.
&nbsp;

## Unitary Identity Subgroup Evaluation
To measure unintended bias, we calculate three separate ROC-AUC results for each identity. Each result captures a different type of unintended bias and each is calculated by restricting the data set to different subsets:

| Test set   | Description                         |
|----------------|-------------------------------|
|Subgroup AUC|Here, we restrict the data set to only the examples that mention the specific identity subgroup. A low value in this metric means the model does a poor job of distinguishing between toxic and non-toxic comments that mention the identity.
|BPSN AUC         |Here, we restrict the test set to the non-toxic examples that mention the identity and the toxic examples that do not. A low value in this metric means that the model confuses non-toxic examples that mention the identity with toxic examples that do not, likely meaning that the model predicts higher toxicity scores than it should for non-toxic examples mentioning the identity.  
|BNSP AUC         |Here, we restrict the test set to the toxic examples that mention the identity and the non-toxic examples that do not. A low value here means that the model confuses toxic examples that mention the identity with non-toxic examples that do not, likely meaning that the model predicts lower toxicity scores than it should for toxic examples mentioning the identity.|

Below are unintended bias evaluation results for a subset of identities for two versions of our model, the initial TOXICITY@1, launched in February 2017, and the latest TOXICITY@6, launched in August 2018. [See our results for all versions of Toxicity models here, including results for more identity terms and more intersectional results.](https://docs.google.com/spreadsheets/d/13edevE6WQLhEQ7r3nY4Z1leJZ-M5BbO_4UUQwc33Hr4/edit?usp=sharing)&nbsp;
![](perspectiveapi/model_cards/unitary.png)


## Intersectional Identity Subgroup Evaluation
The intersectional evaluation shows results for comments mentioning two identities.  
![](https://github.com/conversationai/perspectiveapi/blob/lucy-model-card/model_cards/intersectional.png)


#### Get involved
If you have any questions, feedback, or additional things you'd like to see in the model card,
[please reach out to us here.](https://docs.google.com/forms/d/e/1FAIpQLScgwNY8PAsVxwYRSknUUHBU2Lai85rqeOuD17lTDWmDEUqq3Q/viewform)

