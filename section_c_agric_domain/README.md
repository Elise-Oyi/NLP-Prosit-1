# ICS554 Prosit 1 — Section C: GPT-2 tuned to the agriculture domain

GPT-2 (small, 124M parameters) fine-tuned on Kenyan farmer questions and answers, so it
models agricultural English better than the general-purpose model.

## Results

Perplexity (lower is better).

| Model | Dev | Test |
|---|---|---|
| GPT-2 untuned | 15.45 | 15.61 |
| **GPT-2 tuned** | **5.09** | **5.07** |

> These numbers are from the first run, which measured only the first 200 dev/test
> texts. The notebook now measures every dev and test text, so update this table
> from `section_c_results.txt` after re-running it.

Training loss fell from 3.34 to about 1.55. Dev and test perplexity are almost the same,
so the model is not just memorising the training data.

## Data

[`DigiGreen/farmerchat-queries`](https://huggingface.co/datasets/DigiGreen/farmerchat-queries),
Kenya subset: 6,815 farmer questions with answers (about 2.3 million words). Each
question and its answer are joined into one text.

Split (shuffled with seed 42): 80% train (5,452), 10% dev (681), 10% test (682).

## Training

Full fine-tuning of GPT-2 small: 600 steps, batch size 4, max length 256 tokens,
AdamW, learning rate 5e-5, on a free Google Colab Tesla T4 GPU. Padding tokens are
excluded from the loss. Every 100 steps the model is checked on 50 dev texts it never
trains on, to confirm it is learning and not just memorising.

## Figures

The notebook saves these to `MyDrive/Ashesi/ICS554_Prosit1_TaskC/figures/`:

- `training_curves.png` — training loss per step, and dev perplexity every 100 steps
- `perplexity_before_after.png` — untuned vs tuned perplexity on dev and test

It also prints untuned and tuned GPT-2 completions of the same prompts (same random
seed) side by side, and saves them in `section_c_results.txt`.

## How to run

Open `NLP_Task2_domain_model.ipynb` in Google Colab with a GPU runtime and run all cells.
The dataset downloads from Hugging Face. Results and figures are saved to Google Drive under
`MyDrive/Ashesi/ICS554_Prosit1_TaskC/`.

Requirements: `torch`, `transformers`, `datasets` (all preinstalled on Colab).
