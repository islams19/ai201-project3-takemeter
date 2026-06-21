# TakeMeter Planning

## Community

I will classify comments from NBA online communities, including Reddit, forums, and social media discussions.

## Task

TakeMeter will classify the quality of NBA discussion comments based on how much meaningful basketball discussion they provide.

## Label Taxonomy

### 1. Analysis

A comment that provides reasoning, evidence, basketball knowledge, statistics, comparisons, or a clear explanation to support its point.

**Examples:**

* "Jokic helps his teammates get easy shots because of his passing."
* "The Celtics have one of the best defenses in the league because they can switch every position."

### 2. Hot Take

A comment that expresses a strong opinion with little or no supporting evidence.

**Examples:**

* "Giannis is the best player ever."
* "Embiid will never win a championship."

### 3. Low-Effort / Noise

A comment that does not add meaningful discussion. These comments are usually very short, emotional reactions, insults, jokes, or one-line responses.

**Examples:**

* "Bad take."
* "Trash team."
* "Not true."

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

## Dataset Plan

I will collect and manually label at least 200 NBA comments.

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

## Evaluation Plan

I will evaluate both models using:

* Accuracy
* Precision
* Recall
* F1 Score
* Confusion Matrix

I will also include:

* At least three incorrectly classified examples
* An analysis of model errors
* A reflection on what the model learned versus what I intended it to learn
