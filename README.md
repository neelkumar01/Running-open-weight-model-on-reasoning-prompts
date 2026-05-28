## Running DeepSeek R1 Distill Qwen 1.5B Model on Reasoning Prompts

### Overview

The main motive of this project is to run an open weight reasoning model on a small set of reasoning based prompts and observe how it responds.

The project uses five different reasoning prompts. After running the prompts, the model’s answers are compared with the expected answers to check whether it gives correct and stable responses

Overall, this project gives a simple idea of how a small open weight model performs on common reasoning tasks 🧠

### Model Used

**Model:** DeepSeek-R1-Distill-Qwen-1.5B

It is designed to imitate the reasoning behavior of the larger DeepSeek-R1 model while being lightweight enough to run locally. Because it is a 1.5B parameter model, it is faster and easier to run than larger models

### Prompt Categories

Five reasoning prompts are used. Each prompt targets a known cognitive trap

| No. | Reasoning Type | Prompt |
|---|---|---|
| 1 | Normal intution check | A train takes 2 hours to go from City A to City B. The return journey takes 120 minutes. Which journey is faster? Show your full reasoning step by step | 
| 2 | Multi step arithmetic | Rohan had 60 marbles. He gave 20 to his friend, then doubled what he had left, then lost 15. How many marbles does he have now? | 
| 3 | Logical Deduction | There are three boxes: one has apples, one has oranges, and one has both. All labels are wrong. You can pick one fruit from one box only. Which box should you pick from to fix all labels? Explain your full chain of reasoning before giving a final answer. | 
| 4 | Multiplicative reasoning | Aman can clean a room in 3 hours. Bina can clean the same room in 6 hours. They work together for 1 hour, then Aman leaves. How long will Bina take to finish the rest? Show all steps. | 
| 5 | Casual reasoning | A woman looked at a photo and said, “I have no brothers or sisters, but this person’s father is my father’s son.” Who is in the photo? Show your reasoning. | 


### Results Summary

| Prompt | Correct Answer | Model Answer | Correct? | Analysis |
|---|---|---|---|---|
| 1 | Both trips last 2 hours (120 minutes), so neither is faster; they are equally fast. | It introduced an arbitrary distance D, calculated speeds for each leg, realised 2 hours = 120 minutes, and concluded both journeys are equally fast | Yes | The model reached the right conclusion but was verbose, briefly confused by the time units, and added unnecessary distance notation before recognising the times are identical. |
| 2 | Rohan has 65 marbles now. | It subtracted 20, doubled the remainder, subtracted 15, and concluded Rohan has 65 marbles | Yes | The reasoning is clear and correct, though the model repeated the final answer and extra wording could be trimmed. |
| 3 | Pick one fruit from the box labeled “both.” Its content must be a single fruit type (apples or oranges); that single sample lets you deduce and relabel all three boxes. | It reasoned that because every label is wrong, the “both” box must hold only one fruit type, so sampling that box reveals its true contents and allows the other two boxes to be relabeled. | Yes | The logic is essentially right—choose the “both” box—though the explanation is verbose and repeats points; a shorter chain of reasoning would suffice. |
| 4 | Bina needs 3 hours more to finish the room. | It computed the rates (Aman = ⅓ room/hr, Bina = ⅙ room/hr), found they cleaned ½ room together in 1 hour, and calculated that Bina needs 3 hours to finish the remaining ½ room. | Yes | Reasoning is accurate and clearly structured, though the explanation is long and repeats steps; it could be condensed without losing clarity. |
| 5 | The photo shows her son | It argued that “my father’s son” refers to the woman herself and concluded the photo is of the woman. | No | The model mis-parsed the relationship chain: “my father’s son” indeed refers to the speaker, which means she is the father of the person in the photo—hence the person must be her child, not herself; it also tangled gender terms and gave a contradictory explanation. |


