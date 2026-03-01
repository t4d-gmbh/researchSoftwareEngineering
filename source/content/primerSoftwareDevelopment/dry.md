---
sd_hide_title: true
---
## The DRY Principle

{% if slide %}

```{compound}
{.centered}
{.bigger}
**Don't Repeat Yourself**

{.centered}
"Every piece of knowledge must have a single, unambiguous, authoritative representation within a system."
```


:::::{grid} 2
::::{grid-item-card} Why DRY
- Fix a bug in one place, not five
- Changes propagate automatically
- Reusable components get better testing
- Encourages modular architecture
::::
::::{grid-item-card} When DRY hurts
- Over-abstraction obscures intent
- Forcing two different use cases into one function creates "parameter soup"
- Accidental duplication ≠ logical duplication
::::
:::::

:::{admonition} Keep in mind
:class: warning margin
*"Duplication is far cheaper than the wrong abstraction."*
:::

---

### Example: Magic Strings

::::{grid} 2
:::{grid-item-card} WET ❌
```python
print(df['Name'])
print(df['Age'])
# "Name" repeated everywhere
```
If the column is renamed, you hunt down every occurrence.
:::
:::{grid-item-card} DRY ✔
```python
cn = SimpleNamespace()
cn.name = 'Name'
cn.age = 'Age'

print(df[cn.name])
print(df[cn.age])
```
Rename once, everything follows. IDE autocomplete works. Typos crash immediately.
:::
::::

{% else %}

### The Idea

DRY stands for *Don't Repeat Yourself*. The principle states that every piece of knowledge should have a single, unambiguous representation in a system. If you perform the same logical operation in multiple places, define it once and reuse it.

### Benefits

- **Fewer bugs:** Duplicated logic means a fix in one place might be missed in another.
- **Easier maintenance:** Centralized logic means updates happen in one location and propagate everywhere.
- **Better quality:** Components that get reused also get tested more thoroughly.
- **Cleaner architecture:** DRY naturally pushes you toward modular, decoupled design.

### When DRY Backfires

DRY is not a dogma. Pushed too far, it creates problems of its own:

- **Over-abstraction:** Code so generic it loses clarity. Functions that handle every edge case become convoluted.
- **Coupling:** Forcing two slightly different use cases into one function produces "parameter soup": functions with complex configuration to cover both cases.
- **Fragility:** If two unrelated parts of an application share code by accident (not because the logic is the same), changing the shared code for one part can break the other.

The goal is balance. As a practical rule: *duplication is far cheaper than the wrong abstraction.* How DRY to be is a judgment call that comes with experience.

### Single Source of Truth

Closely related to DRY is the concept of **Single Source of Truth (SSOT)**. While DRY usually refers to logic, SSOT refers to data: every data element should be defined in exactly one place.

In scientific computing, the boundary between data and code often blurs. Column names in a DataFrame are a good example: are they data (strings in a CSV) or code (identifiers in your script)? Either way, defining them once is always better.

### Example

A common source of duplication in data analysis is "magic strings". These are column names repeated as string literals throughout a script.

**The WET version** (Write Everything Twice):

```python
print(fighter_df['Name'])
print(fighter_df['Age'])
# 'Name' and 'Age' appear as strings in many places
```

If the CSV column is renamed from `"Name"` to `"Vorname"`, you have to find and replace every occurrence. Miss one, and the script fails silently or crashes far from where the actual problem is.

**The DRY version:**

```python
from types import SimpleNamespace

fighter_cn = SimpleNamespace()
fighter_cn.name = 'Name'
fighter_cn.age = 'Age'
fighter_cn.city = 'City'

print(fighter_df[fighter_cn.name])
print(fighter_df[fighter_cn.age])
```

This seems like overhead for a short script, but in a real project it gives you:

1. **Trivial refactoring**: change the column name in one place.
2. **IDE autocompletion**: `fighter_cn.` triggers suggestions; `"Na..."` does not.
3. **Immediate error detection**: `fighter_cn.naame` raises `AttributeError` right away. `fighter_df["Naame"]` might silently create an empty column.

{% endif %}
