---
sd_hide_title: true
---
# ✏️ Refactor Your Project

```{compound}
{.centered}
{.bigger}
**Exercise**: Rewrite the Fine-Tuning Pipeline

{.centered}
Restructure `first_round.py` so you can change the model, dataset, or a hyperparameter **without editing unrelated code**.
```

---

## A Possible Target Structure

::::{grid} 2
:gutter: 2

:::{grid-item-card} 🧠 `src/custom/`
```text
__init__.py
model.py      # load, quantize, apply LoRA
data.py       # load, clean, tokenize
config.py     # MODEL_ID, paths, hyperparams
```
:::

:::{grid-item-card} 🚀 `scripts/`
```text
train.py      # orchestrate: load → prepare → train → save
inference.py  # load base + adapter → generate
```
:::
::::

---

## Steps

:::::{grid} 2 2 4 4
:gutter: 2

::::{grid-item-card} 1 — Config
Extract `MODEL_ID`, paths, LoRA & training hyperparameters into one place.
::::
::::{grid-item-card} 2 — Data
Isolate loading, cleaning, tokenizing. No model knowledge.
::::
::::{grid-item-card} 3 — Model
Functions for quantized loading, LoRA injection, tokenizer. No data knowledge.
::::
::::{grid-item-card} 4 — Script
`train.py` wires it all together — short, readable, mostly function calls.
::::
:::::

---

## 📝 Homework

:::{admonition} Due next session
:class: important
Complete the refactoring and push to your fork.
:::

- No duplicated `MODEL_ID`
- `src/custom/` importable via `pip install -e .`
- `train.py` and `inference.py` read like a high-level recipe
- Commented-out code removed — that's what version control is for
