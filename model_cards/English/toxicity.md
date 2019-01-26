# Toxicity 
Toxicity classifies rude, disrespectful, or unreasonable comment that is likely to make people leave a discussion. This model is a Convolutional Neural Network (CNN) trained with word-vector inputs. You can also train your own deep CNN for text classification on our public toxicity dataset, and explore our open-source model training tools to train your own models.


## Performance overview

![](https://github.com/conversationai/perspectiveapi/blob/lucy-model-card/model_cards/auc.png)



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



## Model data

#### Training data
Proprietary from Perspective API, which includes comments from a online forums such as Wikipedia and New York Times, with crowdsourced labels of whether the comment is “toxic”.

#### Evaluation data
A synthetic test set generated using a template-based approach, where identity terms are swapped into a variety of template sentences.
&nbsp;

#### Caveats
Synthetic test data covers only a small set of very specific comments. While these are designed to be representative of common use cases and concerns, it is not comprehensive.
&nbsp;

## Fairness

#### Values
Community, Transparency, Inclusivity, Privacy, and Topic neutrality. Because of privacy considerations, the model does not take into account user history when making judgments about toxicity.
&nbsp;

#### Group factors
Identity terms referencing frequently attacked groups, focusing on sexual orientation, gender identity, and race.
&nbsp;

#### Evaluation data
Real data often has disproportionate amounts of toxicity directed at specific groups, while the synthetic test set ensures that we evaluate on data that represents both toxic and non-toxic statements referencing a variety of groups.
&nbsp;


## Unitary Identity Subgroup Evaluation
To measuring unintended bias, we calculate three separate ROC-AUC results, each on different subsets of the test set.
[See full list of test set results](https://docs.google.com/spreadsheets/d/13edevE6WQLhEQ7r3nY4Z1leJZ-M5BbO_4UUQwc33Hr4/edit?usp=sharing)&nbsp;
![](https://github.com/conversationai/perspectiveapi/blob/lucy-model-card/model_cards/1f.png)


## Intersectional Identity Subgroup Evaluation

![](https://github.com/conversationai/perspectiveapi/blob/lucy-model-card/model_cards/1g.png)

| Test set   | Description                         |
|----------------|-------------------------------|
|Subgroup AUC|Here, we restrict the test set to only the examples within the specific identity subgroup. A low value in this metric means the model does a poor job of distinguishing toxic and non-toxic comments within the group.     
|BPSN AUC         |Here, we restrict the test set to only the non-toxic examples within the identity subgroup and the toxic examples outside the group. A low value in this metric means that the model confuses non-toxic examples in the identity subgroup with toxic examples from other groups, likely meaning that the model predicts higher toxicity scores for non-toxic examples in the identity group than it should.  
|BNSP AUC         |Here, we restrict the test set to only the toxic examples within the identity subgroup and the non-toxic examples outside the group. A low value here means that the model confuses toxic examples in the identity subgroup with non-toxic examples from other groups, likely meaning that the model predicts lower toxicity scores for toxic examples in the identity group than it should.|
