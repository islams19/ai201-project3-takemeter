# TakeMeter: NBA Discussion Quality Classifier

## Overview

TakeMeter is a text classification project that evaluates the quality of NBA discussion comments. The goal is to classify comments into categories that reflect how much value they add to a basketball discussion.

## Community

NBA online discussion communities such as Reddit, forums, and social media comment sections.

## Labels

### Insightful Take

Comments that provide reasoning, analysis, evidence, or useful basketball discussion.

Examples:

* "Jokic helps his teammates get easy shots."
* "The Celtics play good team defense."

### Hot Take

Strong opinions that have little evidence or are exaggerated.

Examples:

* "Giannis is the best player ever."
* "Embiid will never win a title."

### Low-Effort / Noise

Very short comments that do not add meaningful discussion.

Examples:

* "Bad take."
* "Trash team."

## Dataset

The dataset contains labeled NBA discussion comments.

Columns:

* text
* label
* split

Target size: 200+ labeled examples.

## Model

Base model:

* distilbert-base-uncased

Baseline model:

* Groq llama-3.3-70b-versatile

## Training Settings

I fine-tuned the model using the default training settings provided in the notebook.

Model:

* distilbert-base-uncased

Training Hyperparameters:

* Epochs: 3
* Learning Rate: 2e-5
* Training Batch Size: 16
* Evaluation Batch Size: 32
* Weight Decay: 0.01

I kept the default settings because they are recommended for datasets containing approximately 100–500 examples and provide a strong baseline for text classification.

## Evaluation

The project will compare:

* Accuracy
* Precision
* Recall
* F1 Score
* Confusion Matrix

The fine-tuned model will be evaluated against the Groq zero-shot baseline.

## Evaluation Interpretation

The model's overall accuracy shows how many test examples it classified correctly.

I also reviewed precision, recall, and F1 score for each label because accuracy alone does not show whether the model performs well on every class.

### Accuracy

Accuracy measures the percentage of comments classified correctly overall.

### Precision

Precision measures how often a predicted label is correct. High precision means the model is usually correct when it predicts a specific label.

### Recall

Recall measures how many comments from a label are successfully identified by the model. High recall means the model is finding most examples of that label.

### F1 Score

F1 Score combines precision and recall into a single metric and provides a balanced measure of performance.

### Confusion Matrix

The confusion matrix helps identify which labels are most commonly confused with one another. This is especially useful for understanding whether the model struggles to distinguish between Analysis and Hot Take comments.

### Success Criteria

A successful model should achieve:

* Overall accuracy above 70%
* Per-class F1 scores near or above 0.70
* Clear improvement over the Groq zero-shot baseline
* Most predictions appearing on the diagonal of the confusion matrix

## Difficult Examples

Examples that may be difficult to classify:

* Comments containing both analysis and strong opinions.
* Sarcastic comments.
* Comments that are short but still contain basketball reasoning.

## Reflection

This project explores the difference between meaningful basketball analysis, opinion-based takes, and low-effort comments.

## Results

### Fine-Tuned Model Performance

**Overall Accuracy:** 25%

#### Per-Class Metrics

| Label              | Precision | Recall | F1 Score |
| ------------------ | --------- | ------ | -------- |
| Analysis           | 0.00      | 0.00   | 0.00     |
| Hot Take           | 0.00      | 0.00   | 0.00     |
| Low-Effort / Noise | 0.25      | 1.00   | 0.40     |

### Confusion Matrix

The confusion matrix showed that the model predicted most examples as **Low-Effort / Noise**.

The model struggled to distinguish between Analysis and Hot Take comments and frequently classified them as Low-Effort / Noise.

The confusion matrix image is included as:

* confusion_matrix.png

## Error Analysis

### Example 1

**Comment:**
"Luka makes smart plays with the ball."

**True Label:** Analysis

**Predicted Label:** Low-Effort / Noise

**Analysis:**
The comment contains basketball reasoning but is very short. The model likely relied on comment length rather than recognizing the basketball analysis.

### Example 2

**Comment:**
"Tatum is not as good as everyone thinks."

**True Label:** Hot Take

**Predicted Label:** Low-Effort / Noise

**Analysis:**
This comment expresses a strong opinion and should be classified as a Hot Take. Because it is short and lacks supporting evidence, the model confused it with a low-effort reaction.

### Example 3

**Comment:**
"The Nuggets move the ball well."

**True Label:** Analysis

**Predicted Label:** Low-Effort / Noise

**Analysis:**
The comment provides a basketball observation, but the model incorrectly treated it as a short reaction comment.

## Evaluation Report

### Fine-Tuned Model Accuracy

* Fine-Tuned Model Accuracy: 25%
* Test Set Size: 8 Examples

### Baseline Model Accuracy

The Groq zero-shot baseline was used as a comparison model. The baseline and fine-tuned model were evaluated on the same test set.

### Per-Class Metrics (Fine-Tuned Model)

| Label              | Precision | Recall | F1 Score |
| ------------------ | --------- | ------ | -------- |
| Analysis           | 0.00      | 0.00   | 0.00     |
| Hot Take           | 0.00      | 0.00   | 0.00     |
| Low-Effort / Noise | 0.25      | 1.00   | 0.40     |

### Confusion Matrix (Fine-Tuned Model)

| True Label         | Analysis | Hot Take | Low-Effort / Noise |
| ------------------ | -------- | -------- | ------------------ |
| Analysis           | 0        | 0        | 3                  |
| Hot Take           | 0        | 0        | 3                  |
| Low-Effort / Noise | 0        | 0        | 2                  |

### Error Pattern Analysis

After reviewing the incorrect predictions, the most common pattern was confusion between Analysis and Low-Effort / Noise.

The model frequently predicted Low-Effort / Noise when a comment was short, even when it contained basketball reasoning. This suggests that the model learned to associate short comments with the Low-Effort / Noise label rather than focusing on the actual content.

The model also struggled to identify Hot Take comments. Many strong opinions were classified as Low-Effort / Noise because they were short and lacked detailed explanations.

This appears to be primarily a data limitation problem rather than a labeling problem. The labels were applied consistently, but the training dataset was small and did not contain enough examples showing the differences between short Analysis comments, short Hot Takes, and true Low-Effort comments.

To improve performance, I would collect more examples, especially short Analysis and Hot Take comments, and increase the overall dataset size beyond 200 examples.

### Wrong Prediction Analysis

#### Example 1

**Comment:** "Luka makes smart plays with the ball."

**True Label:** Analysis

**Predicted Label:** Low-Effort / Noise

**Why It Failed:**

The comment contains basketball reasoning, but it is very short. The model appears to rely heavily on comment length instead of identifying basketball analysis.

#### Example 2

**Comment:** "Tatum is not as good as everyone thinks."

**True Label:** Hot Take

**Predicted Label:** Low-Effort / Noise

**Why It Failed:**

The comment expresses a strong opinion without supporting evidence, which matches the Hot Take definition. The model incorrectly treated it as a simple reaction because of its short length.

#### Example 3

**Comment:** "The Nuggets move the ball well."

**True Label:** Analysis

**Predicted Label:** Low-Effort / Noise

**Why It Failed:**

The comment contains a basketball observation and should be classified as Analysis. The model again focused on the short structure of the comment rather than its basketball content.

### Sample Classifications

| Comment                                                                          | Predicted Label    | Confidence |
| -------------------------------------------------------------------------------- | ------------------ | ---------- |
| Luka makes smart plays with the ball.                                            | Low-Effort / Noise | 0.37       |
| Having burner accounts is the opposite of not caring.                            | Low-Effort / Noise | 0.37       |
| Champagnie played like a 2nd overall pick more than the actual 2nd overall pick. | Low-Effort / Noise | 0.38       |
| The Nuggets move the ball well.                                                  | Low-Effort / Noise | 0.38       |
| Best at the chase down block ever.                                               | Low-Effort / Noise | 0.39       |

### Reflection

My goal was for the model to distinguish between meaningful basketball analysis, opinion-based hot takes, and low-effort discussion.

Instead, the model primarily learned to distinguish comments based on length. Short comments were frequently classified as Low-Effort / Noise regardless of whether they contained basketball reasoning or strong opinions.

This suggests that the model did not fully learn the intended decision boundaries between Analysis, Hot Take, and Low-Effort / Noise. The small dataset size likely caused the model to overfit to superficial patterns such as comment length rather than deeper semantic meaning.

With a larger and more balanced dataset, the model would likely learn the intended distinctions more effectively.


## Final Reflection

The model struggled to distinguish between Analysis, Hot Take, and Low-Effort / Noise comments. Most predictions were assigned to the Low-Effort / Noise category.

One major reason for this result is the small dataset size. The project recommends at least 200 labeled examples, while this experiment used approximately 50 examples. With more labeled data, the model would likely learn stronger patterns and better distinguish between the three classes.

The error analysis suggests that short comments were especially difficult for the model. Even comments containing basketball reasoning were sometimes classified as Low-Effort / Noise because they lacked detailed explanations.

Future improvements would include collecting more examples, balancing the label distribution, and expanding the number of Analysis and Hot Take examples before retraining the model.
