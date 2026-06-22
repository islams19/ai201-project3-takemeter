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
