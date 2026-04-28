# English → Vietnamese Machine Translation

Comparing two Transformer paradigms for English-to-Vietnamese translation on IWSLT'15 data:

| # | Experiment | Model | BLEU |
|---|-----------|-------|------|
| 1 | Encoder–Decoder | `Helsinki-NLP/opus-mt-en-vi` (fine-tuned) | **37.30** |
| 2 | Decoder-only LLM | `google/gemma-2-2b-it` + QLoRA | **32.79** |
| — | Baseline (no fine-tuning) | `Helsinki-NLP/opus-mt-en-vi` | 29.76 |

## 📁 Project Structure

```
en-vi-mt/
├── notebooks/
│   ├── 01_data.ipynb              # Data collection, cleaning & EDA (IWSLT15 En-Vi)
│   ├── 02_encoder_decoder.ipynb   # Fine-tune MarianMT (Encoder-Decoder)
│   └── 03_finetune_llm.ipynb      # Fine-tune Gemma-2-2B with QLoRA (Decoder-only)
├── results/                       # BLEU scores, training logs, translation examples
├── data/                          # Raw & processed data (git-ignored)
├── report/                        # Final report
├── src/                           # Helper scripts
├── requirements.txt
└── README.md
```

## 🚀 How to Run (Kaggle)

These notebooks are designed to run sequentially on **Kaggle** with a **GPU T4** accelerator:

1. **Notebook 01** — Upload to Kaggle → `Save & Run All (Commit)`. This generates the cleaned IWSLT15 dataset.
2. **Notebook 02** — Upload to Kaggle → **Add Data** → attach the output of Notebook 01 → enable GPU → `Save & Run All (Commit)`.
3. **Notebook 03** — Upload to Kaggle → **Add Data** → attach the output of Notebook 01 → add your `HF_TOKEN` in **Add-ons → Secrets** (required to download the gated Gemma model) → enable GPU → `Save & Run All (Commit)`.

> **Note:** Notebooks 02 and 03 automatically search for the dataset inside `/kaggle/input` regardless of the source notebook's name or owner, so no hardcoded paths need to be changed.

## 📦 Requirements

```bash
pip install -r requirements.txt
```

## 📊 Detailed Results

Full metrics are saved in `results/`:

| File | Description |
|------|-------------|
| `exp1_encoder_decoder.json` | Baseline & fine-tuned BLEU for MarianMT |
| `exp2_llm_lora.json` | BLEU score for Gemma-2-2B QLoRA |
| `training_log_exp1.json` | Training loss/BLEU per epoch (Exp 1) |
| `training_log_exp2.json` | Training loss per step (Exp 2) |
| `translation_examples.json` | 20 side-by-side translations (Exp 1) |
| `llm_translation_examples.json` | 20 side-by-side translations (Exp 2) |
| `baseline_predictions.json` | Top 50 raw predictions from MarianMT baseline |
| `llm_predictions_checkpoint.json` | Top 50 raw predictions from Gemma-2-2B |