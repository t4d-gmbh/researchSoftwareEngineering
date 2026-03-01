---
sd_hide_title: true
---
# ✏️ Restructure Your Code Base

```{compound}
{.centered}
{.bigger}
**Exercise**: Apply the Three Principles

{.centered}
Open `scripts/explore/first_round.py` — mark every violation you find.
```

::::{grid} 3
:gutter: 2

:::{grid-item-card} 🔀 Orthogonality
Independent concerns tangled together?

*Could you swap the dataset without touching the training loop?*
:::
:::{grid-item-card} 🔁 DRY
Values or logic repeated across files?

*What breaks if you change `MODEL_ID` in one file but not the other?*
:::
:::{grid-item-card} 📌 SST
Parameters without a single home?

*Where is the canonical definition of `max_length`?*
:::
::::

:::{admonition} ~10 min annotation → plenum discussion
:class: tip
:::

---

## 💬 Discussion

- Which blocks become their own **function** or **module**?
- Where should shared parameters live?
- What is the right granularity?
