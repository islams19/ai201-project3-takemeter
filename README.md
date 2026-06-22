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

## Final Reflection

The model struggled to distinguish between Analysis, Hot Take, and Low-Effort / Noise comments. Most predictions were assigned to the Low-Effort / Noise category.

One major reason for this result is the small dataset size. The project recommends at least 200 labeled examples, while this experiment used approximately 50 examples. With more labeled data, the model would likely learn stronger patterns and better distinguish between the three classes.

The error analysis suggests that short comments were especially difficult for the model. Even comments containing basketball reasoning were sometimes classified as Low-Effort / Noise because they lacked detailed explanations.

Future improvements would include collecting more examples, balancing the label distribution, and expanding the number of Analysis and Hot Take examples before retraining the model.
