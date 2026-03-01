---
sd_hide_title: true
---
# ✏️ Restructure Your Code Base

```{compound}
{.centered}
{.bigger}
**Exercise**: Split the Script

{.centered}
Break `first_round.py` into focused scripts and extract reusable logic into `src/`.
```

---

## 🔪 Step 1 — Split into three scripts

::::{grid} 3
:gutter: 2

:::{grid-item-card} 📥 Data retrieval
Download / fetch the raw corpus.
:::
:::{grid-item-card} 🧹 Preprocessing
Turn raw data into clean text files (`data/interim/`).
:::
:::{grid-item-card} 🏋️ Training
Load model, tokenize, train, save adapter.
:::
::::

---

## 🧠 Step 2 — Extract reusable functions into `src/`

Identify logic inside each script that is **general-purpose** and move it to a module:

::::{grid} 2
:gutter: 2

:::{grid-item-card} 🚀 `scripts/`
Orchestration only — parse config, call functions, save outputs.
:::
:::{grid-item-card} 🧠 `src/apertusor/`
Reusable building blocks: model loading, tokenization helpers, data utilities.
:::
::::

:::{admonition} Keep in mind
:class: warning margin
Maintain the separation of concerns from the previous exercise — config, environment, data, and code each stay in their own place.
:::

---

## 💬 Discussion

- Which pieces of the script are reusable across data retrieval, preprocessing, and training?
- What stays in `scripts/` vs. what moves to `src/`?
- Does splitting change how you handle configuration?
