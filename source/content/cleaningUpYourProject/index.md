---
sd_hide_title: true
---
# ✏️ Cleaning Up Your Project

```{compound}
{.centered}
{.bigger}
**Exercise**: Separate the Concerns

{.centered}
Open the [PSCProject](https://github.com/j-i-l/PSCProject) repository and read through `scripts/explore/first_round.py`.
```

---

## 🔍 Identify

Read the script and classify every element into one of these categories:

::::{grid} 2 2 4 4
:gutter: 2

:::{grid-item-card} ⚙️ Configuration
Model ID, LoRA hyperparameters, training arguments, paths, ...
:::
:::{grid-item-card} 💾 Data
What is raw, what is interim, what is a result?
:::
:::{grid-item-card} 🌍 Environment
Machine-specific settings (`HF_HOME`, device map, CUDA cache, ...)
:::
:::{grid-item-card} 🧠 Code
The actual logic: loading, tokenizing, training, saving.
:::
::::

---

## 🛠️ Task: Restructure the Project

Move each element to its proper place:

::::{grid} 2
:gutter: 2

:::{grid-item-card} Create & populate
```text
.env                  # environment variables
config/               # hyperparams, model config
src/                  # reusable functions/modules
scripts/drafts/       # move the .py here
data/README.md        # document data stages
```
:::

:::{grid-item-card} Guiding questions
- Where does `MODEL_ID` belong — code, config, or environment?
- Which paths are machine-specific vs. project-specific?
- What should `src/` expose so that `scripts/` stays short?
:::
::::

:::{admonition} Up next
:class: important
We will formalize these observations using three principles: **Orthogonality**, **DRY**, and **Single Source of Truth**.
:::
