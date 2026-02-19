# Coding practices

## Stick to Language-Specific Standards

Every programming language comes with its own set of idioms and best practices for writing high-quality code.
Beyond the general principles outlined below, you should always familiarize yourself with the specific conventions of your chosen language.

In Python, for instance, the use of *docstrings* is standard practice.
Docstrings are string literals—typically enclosed in triple double quotes (`"""..."""`)—that appear as the very first statement in a module, function, class, or method. Unlike comments, they are accessible at runtime and are used to automatically generate documentation.

To learn more, refer to the official [Python convention about docstrings](https://peps.python.org/pep-0257/) (PEP 257) or read the excellent *Real Python* guide on [Documenting Your Python Code Base Using Docstrings](https://realpython.com/documenting-python-code/#documenting-your-python-code-base-using-docstrings).
We will return to this topic in future sessions.

Furthermore, Python adheres to strict naming conventions to differentiate between types of objects.

Classes should be named using *CamelCase* (e.g., `MyClass`), while functions, variables, and instances should use *snake_case* (e.g., `my_variable`). Global constants should be written in *ALL_CAPS*.
While the code will run without following these rules, adhering to them significantly improves readability for both human reviewers and AI-assisted tools.

Python even embeds its own philosophy on code quality directly into the language.
You can view these guiding principles, known as the "Zen of Python," by opening an interactive shell and running:

```python
import this

```

The "Zen of Python" offers aphorisms that capture the essence of "Pythonic" code. While some points are abstract, they provide excellent guidance for decision-making in software design.
(As a side note, consider looking up why the `this` module is considered one of Python's oldest Easter eggs).

## Make Code Readable

In this section, we focus on techniques to ensure your code is accessible to others:

* Making code self-documenting.
* Prioritizing clarity over cleverness.
* Leveraging language features correctly.

### Use Descriptive Names

Names are the primary handles we use to grasp concepts in code.
Consider a household appliance: labeling a toaster "Object A" obscures its function, whereas labeling it "Toaster" immediately conveys its purpose.
If you had to read a manual referring only to "Object A," you would constantly have to look up what it does.

The same logic applies to programming. Names for classes, functions, and variables should be self-explanatory.

**Retain:**

* *Nondescriptive names force the reader to memorize arbitrary details.*
* *Comments are a poor patch for bad naming; fix the name instead.*

### Use Comments Appropriately

Comments are powerful, but they can be misused. They generally serve to:

* **Explain what:** Summarize a block of code.
* **Explain why:** Justify a non-obvious design choice or workaround.
* **Explain how:** Provide usage examples.

High-level comments that summarize a complex class or algorithm are valuable. However, "play-by-play" comments that merely repeat what the code is doing line-by-line are clutter. If your code requires a comment to explain *what* a simple line does, the code itself is likely too complex or poorly named.

Conversely, comments that explain *why* a specific approach was taken (e.g., "We use this algorithm because it handles edge case X better") are invaluable, as that context cannot be inferred from the code alone.

**Retain:**

* *Redundant comments create visual noise.*
* *Do not use comments to excuse unreadable code.*
* *Use comments to provide context and explain "Why".*
* *Use comments for high-level summaries/documentation.*

### Don’t Fixate on the Number of Lines of Code

It is a common pitfall to equate code quality with brevity.
While concise code is generally good, optimizing solely for the lowest "Lines of Code" (LOC) count often leads to cryptic, "clever" one-liners that are impossible to debug.
A slightly longer function that clearly lays out its logic step-by-step is always preferable to a condensed, obscure one.

**Retain:**

* *Readability trumps brevity.*
* *Code is read much more often than it is written.*

### Embrace Consistency

A consistent coding style is the bedrock of maintainability.
Whether you are working alone or in a team, sticking to a uniform style—same indentation, same naming logic, same file structure—reduces the cognitive load required to read the code.
When style varies, the reader has to constantly adjust their mental model.

**Retain:**

* *Consistency makes patterns easier to spot.*
* *Strictly follow the established style guide (e.g., PEP 8 for Python).*

By adhering to these practices, you ensure that your code is not just a set of instructions for a machine, but a clear communication tool for human developers.

## Reflection

Python is famous for its hidden jokes and features. Aside from the `this` module, try to find a few other Easter eggs hidden in the standard library...

---

Source:\

* Hunt, A., & Thomas, D. (2019). The Pragmatic Programmer: Your journey to mastery. Addison-Wesley. ISBN 9780135957059. (Original publication)
