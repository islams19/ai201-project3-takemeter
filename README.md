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

## Difficult Examples

Examples that may be difficult to classify:

* Comments containing both analysis and strong opinions.
* Sarcastic comments.
* Comments that are short but still contain basketball reasoning.

## Reflection

This project explores the difference between meaningful basketball analysis, opinion-based takes, and low-effort comments.
