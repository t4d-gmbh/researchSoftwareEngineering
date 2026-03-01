---
sd_hide_title: true
---
## Refactoring

{% if slide %}

```{compound}
{.centered}
{.bigger}
**Refactoring**:

{.centered}
Restructure existing code to increase usability, reusability, compatibility and performance *without* changing its external behavior.
```

:::::{grid} 1 2 2 2
:gutter: 2

::::{grid-item}

:::{important}
Nobody writes DRY, well-structured and well-documented orthogonal code on a first attempt!
:::
::::
::::{grid-item-card} Separate Problems:
1. Focus on implementing the routine
2. Refactor into functions/classes
3. Write tests
4. Refactor for performance
4. Refactor for usability
4. Refactor for ...

::::
:::::

{% else %}

Trying to write perfectly DRY, well-structured code on your first attempt is a recipe for paralysis.
When drafting a script, your primary focus should be on solving the problem.
The path from messy working code to clean reusable code is called **refactoring**.

Refactoring is the disciplined practice of restructuring existing code to improve its design, readability, and maintainability without altering its external behavior.

It generally targets four dimensions:

- **Usability**: making code easier to read and understand.
- **Reusability**: structuring logic so it can be applied in different contexts.
- **Compatibility**: ensuring the code integrates well with libraries and standards.
- **Performance**: making code faster or less resource-hungry.

### Refactoring in practice

A systematic approach to refactoring a script:

1. **Identify repetitive code**: look for copy-pasted blocks or logic that appears multiple times. Extract it into a function.
2. **Create clear definitions**: give each function a descriptive name and a single responsibility.
3. **Implement with rubber ducking**: explain to your duck what data the function needs. Those become your arguments.
4. **Aggregate into modules**: group related functions into Python files (modules) and folders (packages).

A simple project structure might look like this:

```plaintext
my_project/
├── src/
│   └── my_analysis/
│       ├── __init__.py
│       ├── cleaning.py
│       └── regression.py
└── pyproject.toml
```

You can then import your logic cleanly:

```python
from my_analysis.cleaning import remove_nulls
from my_analysis.regression import fit_model
```

{% endif %}
