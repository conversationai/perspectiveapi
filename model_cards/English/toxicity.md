# Toxicity 

    TOXICITY@6

Toxicity classifies rude, disrespectful, or unreasonable comment that is likely to make people leave a discussion. This model is a Convolutional Neural Network (CNN) trained with word-vector inputs. You can also train your own deep CNN for text classification on our public toxicity dataset, and explore our open-source model training tools to train your own models.


## Performance overview


Add image



## Intended use


**Human-assisted moderation**
Make moderation easier with an ML assisted tool that helps prioritize comments for moderation, and create custom tasks for automated actions. 

**Author feedback**
Assist authors in real-time when their comments might violate your community guidelines or be may be perceived as “Toxic” to the conversation. Use simple feedback tools when the assistant gets it wrong. 

**Read better comments**
Organize comments on topics that are often difficult to discuss online. Build new tools that help people explore the conversation. 


## Uses to avoid

**Fully automated moderation**
Make moderation easier with an ML assisted tool that helps prioritize comments for moderation, and create custom tasks for automated actions. 

**Character judgement**
This model only helps detect Toxicity in what a person said, and is not intended to detect anything about the individual who said it.



## Model data

**Training data**
Proprietary from Perspective API, which includes comments from a online forums such as Wikipedia and New York Times, with crowdsourced labels of whether the comment is “toxic”.

**Evaluation data**
A synthetic test set generated using a template-based approach, where identity terms are swapped into a variety of template sentences.

**Caveats**
Synthetic test data covers only a small set of very specific comments. While these are designed to be representative of common use cases and concerns, it is not comprehensive.


## Fairness

**Values**
Community, Transparency, Inclusivity, Privacy, and Topic neutrality. Because of privacy considerations, the model does not take into account user history when making judgments about toxicity.

**Group factors**
Identity terms referencing frequently attacked groups, focusing on sexual orientation, gender identity, and race.

**Evaluation data**
Real data often has disproportionate amounts of toxicity directed at specific groups, while the synthetic test set ensures that we evaluate on data that represents both toxic and non-toxic statements referencing a variety of groups.


## Quantitative Analysis

**Unitary terms 1-11**





| Test set   | Description                         |
|----------------|-------------------------------|
|Subgroup AUC|Here, we restrict the test set to only the examples within the specific identity subgroup. A low value in this metric means the model does a poor job of distinguishing toxic and non-toxic comments within the group.     
|BPSN AUC         |Here, we restrict the test set to only the non-toxic examples within the identity subgroup and the toxic examples outside the group. A low value in this metric means that the model confuses non-toxic examples in the identity subgroup with toxic examples from other groups, likely meaning that the model predicts higher toxicity scores for non-toxic examples in the identity group than it should.  
|BNSP AUC         |Here, we restrict the test set to only the toxic examples within the identity subgroup and the non-toxic examples outside the group. A low value here means that the model confuses toxic examples in the identity subgroup with non-toxic examples from other groups, likely meaning that the model predicts lower toxicity scores for toxic examples in the identity group than it should.|
