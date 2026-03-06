# AI Evaluation Metrics Spike

Status: Completed

## Need
As part of the Large Language Model (LLM) validation framework we need a process for comparing LLM responses to known ground truths, e.g. comparing the answers to questions with the known correct answer or comparing LLM generated summaries to the human-written equivalent.  For the initial LLM validation we used two methods for making this comparison - DeepEval (LLM-As-A-Judge) and Bert-Score (Semantic Similarity).  LLM-As-A-Judge requires asking an LLM to score one response in relation to a ground-truth (the assumed ideal response), using a detailed prompt.  Semantic similarity simply rates whether the words in the two response and groun-truth have similar meanings.  DeepEval seemed to provide the best peformance based on finding that newer and bigger models outperformed older and smaller ones.  However there are other methods to do this e.g. Ragas, Meteor and Pydantic and simply looking for the correct ordering of models is not a robust enough way to choose the best evaluation metric.


## Hypothesis
One of the evaluation metrics DeepEval, Pydantic, Ragas or Bert-Score provides a reliable method of comparing LLM responses to the ground-truth and we can determine which method peforms best.

## What we aim to discover
- Which of DeepEval, Pydantic, Ragas or Bert-Score provides the most reliable method of comparing an LLM response to the ground-truth.

## Assumptions
- The ground-truths are true.  In reality this may not always be the case.

## Methodology
- We investigated two functions of LLMs: the ability to answer questions and the ability to summarise documents.

- For Question-Answering we used a public dataset of questions with an array of correct answers, the best answer and an array of incorrect answers.  We exploded the correct and incorrect answer arrays into a column and added a field is_correct describing which of the two arrays they came from.  We fed all the answers into all of our evaluation methods and asked them to calculate a score reflecting correctness.  These were blinded so the model did not know whether they were correct or incorrect.  For each method we evaluated the difference between the mean score for correct answers and incorrect answers.  A large difference between these numbers meant the model was more clearly distinguishing the two.  We also chose a threshold above which answers were deemed 'correct', and calculated a confusion matrix and f1 score.  The f1 score is an average of precision and recall. The difference-between-means and f1 were then examined and compared across the five evaluation methods.  We then set the threshold equal to the mean of correct and incorrect scores and repeated.  This offered an improvement in f1.

- For Document summarising we used a public dataset of documents with a human written summary.  We added a field is_correct=True to this dataset.  We then duplicated the dataset, randomly shuffled the summaries, added a field is_correct=False and added this to the original dataset.  We fed all the answers into all of our evaluation methods and asked them to calculate a score reflecting the quality of the summary.  For each method we evaluated the difference between the mean score for the correct and incorrect summaries.  We also chose a threshold equal above which summaries were deemed correct, and calculated a confusion matrix and f1 score. The difference-between-means and f1 were then examined and compared across the five evaluation methods.  We then set the threshold equal to the mean of correct and incorrect scores and repeated.  This offered an improvement in f1.

We repeated the entire experiment with different back-end models and different values of model temperature where applicable.

## Outcomes
Pydantic generally offers the best performance but the choice of model depends on the type of response being compared.  GPT OSS 120b performs better when comparing question answers whereas Claude 3 Haiku is best at comparing document summaries.  Temperature makes little difference.  We will therefore proceed using Pydantic with Claude Haiku and GPT OSS 120b and a temperature of 0.  Due to the small number of prompts processed results should be treated with caution.


### Key Findings
When comparing the answers to questions
- Pydantic offers the biggest difference in correct and incorrect scores but Deepeval offers the best f1 score.
- GPT OSS 120b offers the best score-difference and f1
- Temperature makes no difference

When comparing the summaries of documents
- Pydantic offers the biggest difference in correct and incorrect scores and highest f1 score.
- Claude 3 Haiku offers the best score-difference and f1
- There is a slight improvement when using a temperature of 0.1 over 0 or 0.2

## Shortcomings
- Due to processing limitations in using a laptop we have based our conclusions on 30 prompts per evaluation method, model and temperature.  To draw a more reliable conclusion we need to re-run the process on a cluster using at least 100 prompts per method, model and temperature.