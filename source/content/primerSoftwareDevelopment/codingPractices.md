{% if build == "slides" %}
## Good Coding Practices
{% else %}
## Good Coding Practices
{% endif %}

{% if slide %}

### Language-Specific Conventions

- Every language has its own idioms — learn them
- Python: docstrings, PEP 8, `snake_case` for functions, `CamelCase` for classes
- Following conventions makes your code readable to others (and to tools)

---

### Descriptive Names

Bad naming forces the reader to memorize arbitrary labels.

::::{grid} 2
:::{grid-item-card} Don't
```python
def proc(d, t):
    return d / t
```
:::
:::{grid-item-card} Do
```python
def compute_speed(distance, time):
    return distance / time
```
:::
::::

:::{admonition} Rule of thumb
:class: tip margin
If you need a comment to explain what a variable *is*, rename it instead.
:::

---

### Comments: When and Why

| Use comments to... | Avoid comments that... |
|---|---|
| Explain *why* a decision was made | Repeat what the code already says |
| Summarize complex logic at a high level | Substitute for clear naming |
| Provide usage examples | Excuse unreadable code |

---

### Consistency Over Cleverness

- Stick to one style: indentation, naming, file structure
- Consistency reduces cognitive load
- Readability always beats brevity

:::{admonition} Remember
:class: important margin
Code is read far more often than it is written.
:::

{% else %}

### Stick to Language-Specific Standards

Every programming language has its own idioms and best practices. Beyond the general principles below, familiarize yourself with the specific conventions of your language.

In Python, **docstrings** are standard. They are string literals (typically `"""..."""`) placed as the first statement in a module, function, class, or method. Unlike comments, they are accessible at runtime and can be used to generate documentation automatically. See [PEP 257](https://peps.python.org/pep-0257/) for the official convention.

Python also uses strict **naming conventions**: `CamelCase` for classes, `snake_case` for functions and variables, `ALL_CAPS` for constants. These are not enforced by the interpreter, but following them makes your code immediately recognizable to any Python developer.

Try running this in a Python shell:

```python
import this
```

The ["Zen of Python"](https://peps.python.org/pep-0020/) captures the core philosophy behind idiomatic Python. Some of it is tongue-in-cheek, but the principles are sound.

### Make Code Readable

#### Use Descriptive Names

Names are the primary way we understand code. A function called `proc` tells you nothing; `compute_speed` tells you everything. If a variable name requires a comment to explain what it holds, the name is wrong.

Nondescriptive names force the reader to memorize arbitrary mappings. Comments are a poor patch for bad naming. Fix the name instead.

#### Use Comments Appropriately

Comments serve three purposes:

- **why:** Justify a non-obvious design choice or workaround.
- **what:** Provide a high-level overview of a complex block.
- **how:** Show usage examples, especially for public APIs.

Play-by-play comments that repeat what the code does line-by-line are clutter. If a line needs a comment to explain *what* it does, it is probably too complex or too cleverly written ;-).

Comments that explain *why* a specific approach was taken are always valuable, that context cannot be recovered from the code alone.

#### Don't Fixate on Line Count

Equating code quality with brevity is a common trap. Condensing logic into cryptic one-liners makes debugging painful. A slightly longer function with clear, step-by-step logic is always preferable.

Readability trumps brevity. Code is read far more often than it is written.

#### Embrace Consistency

A consistent style (same indentation, same naming logic, same file structure) reduces cognitive load. When style varies across a codebase, the reader constantly has to adjust. Follow the established style guide (e.g., PEP 8 for Python) and stick to it.

{% endif %}
