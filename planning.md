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
## Community Research

### Chosen Community

r/nba

This community contains active basketball discussions, game reactions, player debates, trade discussions, and analysis from NBA fans. The quality of discussion varies significantly, making it a good community for a discourse classification task.

### What Makes a High-Quality Comment?

After reviewing NBA discussions, high-quality comments usually:

* Explain a basketball idea or strategy
* Provide evidence, statistics, or comparisons
* Discuss players, teams, or games in detail

Low-quality comments are often:

* Very short reactions
* Insults or personal attacks
* Strong opinions without reasoning

## Label Definitions

### Analysis

Definition:
A comment that supports its claim with basketball reasoning, evidence, statistics, comparisons, or detailed explanation.

Examples:

1. "Jokic makes Denver's offense better because his passing creates open shots for everyone on the floor."

2. "The Celtics are difficult to defend because they have multiple players who can score and shoot from outside."

Uncertain Example:

"Luka is the best offensive player in the league because he controls every possession."

Decision:
Analysis, because the comment provides a basketball reason for the claim.

---

### Hot Take

Definition:
A strong opinion that provides little or no supporting evidence.

Examples:

1. "Giannis is the greatest player of all time."

2. "Embiid will never win a championship."

Uncertain Example:

"LeBron is overrated because his playoff record against elite teams is not impressive."

Decision:
Hot Take, because the statistic is used mainly to support a strong opinion rather than provide detailed analysis.

---

### Low-Effort / Noise

Definition:
A comment that contributes little meaningful discussion and is mainly a reaction, insult, or very short response.

Examples:

1. "Bad take."

2. "Trash team."

Uncertain Example:

"I don't agree with that."

Decision:
Low-Effort / Noise, because it expresses disagreement without providing reasoning.

## Mutual Exclusivity Check

Every comment should belong to exactly one label.

Decision Rules:

* If the comment provides basketball reasoning or evidence → Analysis
* If the comment expresses a strong opinion without meaningful support → Hot Take
* If the comment is mainly a short reaction or adds little discussion → Low-Effort / Noise

These rules are designed to make the labels mutually exclusive and reduce ambiguity during annotation.

