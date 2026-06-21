# TakeMeter Planning

## Community

I will classify comments from NBA online communities, including Reddit, forums, and social media discussions.

### Chosen Community

r/nba

This community contains active basketball discussions, game reactions, player debates, trade discussions, and analysis from NBA fans. The quality of discussion varies significantly, making it a good community for a discourse classification task.

### Why I Chose This Community

I chose r/nba because it is one of the largest and most active sports discussion communities online. The community contains a wide variety of comments, including detailed basketball analysis, strong opinions about players and teams, and short reaction comments. This variety makes it a good fit for a classification task because the differences between comment types are meaningful and occur frequently.

## Task

TakeMeter will classify the quality of NBA discussion comments based on how much meaningful basketball discussion they provide.

### What Makes a High-Quality Comment?

High-quality comments usually:

* Explain a basketball idea or strategy.
* Provide evidence, statistics, or comparisons.
* Discuss players, teams, or games in detail.

Low-quality comments are often:

* Very short reactions.
* Insults or personal attacks.
* Strong opinions without reasoning.

## Label Taxonomy

### 1. Analysis

A comment that provides reasoning, evidence, basketball knowledge, statistics, comparisons, or a clear explanation to support its point.

**Examples:**

* "Jokic helps his teammates get easy shots because of his passing."
* "The Celtics have one of the best defenses in the league because they can switch every position."

**Uncertain Example:**

* "Luka is the best offensive player in the league because he controls every possession."

**Decision:**

Analysis, because the comment provides a basketball reason for the claim.

### 2. Hot Take

A comment that expresses a strong opinion with little or no supporting evidence.

**Examples:**

* "Giannis is the best player ever."
* "Embiid will never win a championship."

**Uncertain Example:**

* "LeBron is overrated because his playoff record against elite teams is not impressive."

**Decision:**

Hot Take, because the statistic is mainly used to support a strong opinion rather than provide detailed analysis.

### 3. Low-Effort / Noise

A comment that does not add meaningful discussion. These comments are usually very short, emotional reactions, insults, jokes, or one-line responses.

**Examples:**

* "Bad take."
* "Trash team."
* "Not true."

**Uncertain Example:**

* "I don't agree with that."

**Decision:**

Low-Effort / Noise, because it expresses disagreement without providing reasoning.

## Ambiguous Example

**Comment:**

"LeBron is overrated because he struggles against elite defenses in the playoffs."

**Possible Labels:**

* Analysis
* Hot Take

**Decision Rule:**

If a comment provides a specific basketball reason, statistic, comparison, or explanation that supports the claim, it will be labeled as Analysis.

If a comment mainly expresses a strong opinion without meaningful support, it will be labeled as Hot Take.

**Final Label:**

Analysis

## Edge Cases

* If a comment contains both emotion and basketball reasoning, label it as Analysis.
* If a comment makes a strong claim but provides little evidence, label it as Hot Take.
* If a comment is very short and adds little discussion, label it as Low-Effort / Noise.
* Every comment must belong to exactly one label.

## Mutual Exclusivity Check

Every comment should belong to exactly one label.

### Decision Rules

* If the comment provides basketball reasoning or evidence → Analysis
* If the comment expresses a strong opinion without meaningful support → Hot Take
* If the comment is mainly a short reaction or adds little discussion → Low-Effort / Noise

These rules help ensure that the labels do not overlap and can be applied consistently.

## Data Collection Plan

I will collect comments from r/nba discussion threads, game threads, player discussions, and trade discussions.

I will manually label at least 200 comments.

Target distribution:

* Analysis: 70 comments
* Hot Take: 70 comments
* Low-Effort / Noise: 60 comments

If one label is underrepresented after collecting 200 comments, I will continue collecting examples until all labels have enough examples for training and evaluation.

Each row will contain:

* text
* label
* split

The dataset will be divided into:

* Train Set (70%)
* Validation Set (15%)
* Test Set (15%)

## Model Plan

I will fine-tune DistilBERT (`distilbert-base-uncased`) on the labeled NBA comment dataset.

I will compare the fine-tuned model against Groq's `llama-3.3-70b-versatile` using zero-shot classification on the same test set.

## Evaluation Metrics

I will use multiple evaluation metrics because accuracy alone does not show how well the model performs on each label.

### Accuracy

Accuracy measures the percentage of comments classified correctly overall.

### Precision

Precision measures how often a predicted label is correct.

### Recall

Recall measures how many comments from a label are successfully identified by the model.

### F1 Score

F1 Score balances precision and recall and provides a better measure of classification quality.

### Confusion Matrix

The confusion matrix helps identify which labels are most frequently confused with one another.

## Evaluation Plan

I will evaluate both models using:

* Accuracy
* Precision
* Recall
* F1 Score
* Confusion Matrix

I will also include:

* At least three incorrectly classified examples.
* An analysis of model errors.
* A reflection on what the model learned versus what I intended it to learn.

## Definition of Success

I will consider the project successful if:

* The fine-tuned model achieves at least 70% accuracy on the test set.
* The F1 score for each label (Analysis, Hot Take, and Low-Effort / Noise) is at least 0.70.
* The fine-tuned model performs better than the Groq zero-shot baseline on overall accuracy.
* The confusion matrix shows that most predictions fall into the correct category rather than being confused with another label.
* The model correctly classifies at least 2 out of the 3 difficult edge-case examples selected for error analysis.

If these criteria are met, I would consider the classifier useful for identifying different types of NBA discussion comments in a real online community.
## AI Tool Plan

### Label Stress-Testing

Before collecting and labeling all 200 comments, I will use ChatGPT to generate 5–10 NBA comments that sit near the boundary between Analysis, Hot Take, and Low-Effort / Noise.

The goal is to test whether my label definitions are clear and mutually exclusive.

Examples of boundary cases I will test:

* A strong opinion supported by one statistic
* A short comment that contains basketball reasoning
* A reaction comment that includes a small amount of analysis

If I cannot consistently assign a single label to these examples, I will revise my label definitions and decision rules before beginning large-scale annotation.

### Annotation Assistance

I may use ChatGPT to suggest labels for a small batch of NBA comments before reviewing them manually.

However, all final labels will be reviewed and approved by me before being added to the dataset.

To maintain transparency, I will keep track of which comments were initially pre-labeled by AI and document this process in the AI Usage section of the final report.

### Failure Analysis

After evaluating the model, I will examine incorrectly classified examples and use ChatGPT to help identify common error patterns.

I will specifically look for:

* Confusion between Analysis and Hot Take comments
* Difficulty classifying short comments
* Comments that contain both reasoning and opinion
* Comments that provide weak evidence for a strong claim

Any patterns suggested by AI will be manually verified by reviewing the misclassified examples before being included in the final evaluation report.

### AI Usage Disclosure

AI tools will be used for:

* Label stress-testing
* Annotation assistance
* Failure analysis

AI tools will not make final labeling decisions. All final dataset labels, evaluation results, and conclusions will be reviewed and approved by me.
