# ICS554 NLP — Prosit 1: Language Models

Code for the Prosit 1 technical report.

| Section | Folder | What it is |
|---|---|---|
| B | [`section_b_twi_ngram/`](section_b_twi_ngram/) | n-gram language model for Twi (low-resource African language), add-k vs Kneser-Ney smoothing |
| C | [`section_c_agric_domain/`](section_c_agric_domain/) | GPT-2 fine-tuned to the agriculture domain (Kenyan farmer Q&A) |

## Headline results

| Section | Model | Test perplexity |
|---|---|---|
| B | Add-k bigram (best add-k) | 175.27 |
| B | **Kneser-Ney 5-gram** | **80.14** |
| C | GPT-2 untuned | 15.66 |
| C | **GPT-2 tuned** | **5.11** |

Perplexities from different sections are not comparable: they use different languages,
data and tokenizers (words vs GPT-2 subword tokens).

See each folder's README for data, training details and how to run.
