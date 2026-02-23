## Refactoring

{% if slide %}

:::{admonition} Definition
:class: note
Refactoring restructures existing code to improve its design, readability, and maintainability *without* changing its external behavior.
:::

{% else %}

Trying to write perfectly DRY, well-structured code on your first attempt is a recipe for paralysis.
When drafting a script, your primary focus should be on solving the problem.
The path from messy working code to clean reusable code is called **refactoring**.

Refactoring is the disciplined practice of restructuring existing code to improve its design, readability, and maintainability without altering its external behavior.

It generally targets four dimensions:

- **Performance**: making code faster or less resource-hungry.
- **Usability**: making code easier to read and understand.
- **Reusability**: structuring logic so it can be applied in different contexts.
- **Compatibility**: ensuring the code integrates well with libraries and standards.

{% endif %}

## Functions

{% if slide %}

The primary tool for reusable code: the **function**.

:::::{grid} 2
::::{grid-item-card} Benefits
- **Modularity**: break problems into small pieces
- **Abstraction**: hide the "how," expose the "what"
- **Testability**: verify functions in isolation
- **Collaboration**: team members build different functions
::::
::::{grid-item-card} Good function design
- Descriptive **verb-noun name** (`calculate_mean`, not `do_math`)
- **Single responsibility**: one function, one job
- **No global variables**: pass everything as arguments
::::
:::::

{% else %}

The primary mechanism for achieving reusable code is the function: a self-contained block of code that accepts inputs, processes them, and returns outputs.

Functions give you modularity (small isolated pieces), abstraction (you can use a function without knowing its internals), testability (verify each one in isolation), and make collaboration straightforward (different people build different functions).

A well-designed function follows a few rules:

- **Descriptive name**: use a verb-noun pair that explains the action, e.g. `calculate_mean` rather than `do_math`.
- **Single responsibility**: one function should do one thing. If it does three things, split it into three functions.
- **No hidden dependencies**: pass all required data as arguments instead of relying on global variables.

{% endif %}

{% if page %}

### Docstrings

Every function should have a docstring. That's a comment block placed at the top of its definition.
A good docstring lets a user understand how to call the function without reading the implementation.

This course follows the **NumPy/SciPy docstring style**. A complete docstring includes a summary, parameter descriptions, return types, and usage examples:

```python
def add_numbers(a: int, b: int) -> int:
    """Add two numbers together.

    Parameters
    ----------
    a
        The first number to add.
    b
        The second number to add.

    Returns
    -------
    int
        The sum of `a` and `b`.

    Examples
    -------
    >>> add_numbers(2, 3)
    5
    """
    return a + b
```

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
