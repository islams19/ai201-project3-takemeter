# TakeMeter Planning

## Community
I will classify comments from the NBA online community.

## Task
TakeMeter will classify the quality of NBA discussion comments.

## Labels

### 1. Insightful Take
A comment that gives a clear basketball reason, evidence, comparison, or useful analysis.

### 2. Hot Take
A comment that gives a strong opinion but has little evidence, exaggeration, or emotional language.


### 3. Low-Effort / Noise
A comment that is mostly a joke, insult, meme, one-word reaction, or does not add real discussion.


## Edge Cases
If a comment has analysis and emotion, label it Insightful Take if it gives a real basketball reason.
If a comment is strong but gives no clear reason, label it Hot Take.
If a comment is too short or just a joke, label it Low-Effort / Noise.

## Dataset Plan
I will collect at least 200 NBA comments.
Each row will include:
- text
- label
- split

The split will be:
- train
- validation
- test

## Model Plan
I will fine-tune distilbert-base-uncased.
I will compare it against Groq llama-3.3-70b-versatile as a zero-shot baseline.

## Evaluation Plan
I will report:
- accuracy
- per-class precision, recall, or F1
- confusion matrix
- at least 3 wrong predictions
- reflection on what the model learned
