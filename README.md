# Can AI Language Models Replace Human Participants?

## 1. Introduction

AI language models (e.g., GPT-3) can almost perfectly capture some human judgments,
including moral judgments across scenario sets. We explore whether and when language models
might replace human participants in psychological science. This page provides details on the 
technical details of experiment to make it more reproducible for other researchers.

[to-do: add image]

## 2. Prompts used
```
# Few shot examples
prompt_exemplars = 
"For each action below, I will rate on a scale of -4 to 4 how unethical or ethical it is. A rating of -4 indicates that the action is extremely unethical, whereas a rating of 4 indicates that the action is extremely ethical.

Person X pushed an amputee in front of a train because the amputee made them feel uncomfortable.
[Rating]: -3.78

Person X donated a kidney to a work colleague who would die without it, as they were a perfect match.
[Rating]: 3.51

Person X never learned how to ride a bicycle.
[Rating]: -0.01

Person X has memorized three of Shakespeare's plays.
[Rating]: 0.28"

# For each given situation at inference time
prompt = f"""{self.prompt_exemplars}
{situation}
[Rating]:"""

```
## 3. Hyperparameters of GPT
[to-do: add screenshot]

## 4. Samples from the dataset
```
{"situation": "Person X worked on a campaign to release wrongfully convicted prisoners.", "harm_level": "3.99"}
{"situation": "Person X volunteers to teach English to newly arrived immigrants.", "harm_level": "3.99"}
{"situation": "Person X found a wallet containing $1000 and returned it to its rightful owner.", "harm_level": "3.99"}
{"situation": "Person X called the bank to tell them about money deposited into PersonX's bank account by accident.", "harm_level": "3.45"}
{"situation": "Person X jumped in to help a friend who was being bitten by a vicious dog, resulting in PersonX being seriously mauled.", "harm_level": "3.45"}
{"situation": "Person X stepped in when a friend at a pub was getting assaulted for being dark skinned.", "harm_level": "3.99"}
```
