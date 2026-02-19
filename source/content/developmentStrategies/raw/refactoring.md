# Refactoring

Attempting to write code that is perfectly DRY (Don't Repeat Yourself) and orthogonal on your first try is a recipe for paralysis—especially if you are solving a complex problem or are new to programming.
When drafting a script, your primary focus should always be on **solving the problem**.
Strategies like "rubber ducking" help you break these complex tasks down into manageable steps.

But if you write "messy" code to solve the problem, how do you end up with high-quality, reusable code?

The answer is: **Refactoring**.

Refactoring is the disciplined practice of restructuring existing code to improve its design, readability, and maintainability—*without* altering its external behavior.
As Martin Fowler defines it in his seminal book *Refactoring: Improving the Design of Existing Code*, the goal is simple: make the code easier for humans to understand and modify.

Refactoring generally targets four key dimensions:

* **Performance**: Optimizing code to run faster or consume fewer resources. This is critical in data-intensive applications where efficiency dictates user experience.
* **Usability**: Making code easier to read. This involves renaming variables for clarity, adding comments, and organizing logic so your future self can understand it.
* **Reusability**: Structuring logic so it can be applied in different contexts without modification, reducing redundancy and errors.
* **Compatibility**: Ensuring the code adheres to standards, integrates well with libraries, and manages dependencies correctly.

In Data Science, the priority usually flows in this order: **Performance > Reusability > Compatibility > Usability**.
We will explore performance in Section 11. For now, we focus on **reusability**.

# Functions

Reusability allows you to write logic once and deploy it across multiple parts of your project.
The primary mechanism for achieving this is the **function**.

A function is a self-contained block of code designed to perform a specific task.
It accepts inputs (arguments), processes them, and returns outputs. By encapsulating logic in functions, you avoid duplication and create a toolbox of reliable operations.

*Note on Classes:* In Python, you will inevitably interact with classes (e.g., creating a `pandas.DataFrame`). Unlike functions, which perform an action and return, classes create objects that persist with their own internal state. While most principles below apply to classes, we will focus on functions to keep this section manageable.

### Benefits of using functions

1. **Modularity**: Functions break complex problems into small, isolated pieces.
2. **Abstraction**: They hide the "how" and expose the "what." You can use a function without knowing the gritty details of its implementation.
3. **Testing and Debugging**: You can test a function in isolation. If it breaks, you know exactly where to look.
4. **Collaboration**: Different team members can build different functions simultaneously.
5. **Documentation**: A well-named function with a clear docstring serves as its own documentation.

### The function docstring

An essential component of any function is the **docstring**.
This is a special comment block placed at the very top of a function definition.
A "good" docstring meets two criteria:

* **Clarity**: It provides immediate context. A user should understand *how* to use the function without reading the code body.
* **Standardization**: While you *can* write docstrings however you like, following a standard allows IDEs and documentation tools (like Sphinx) to parse them automatically.

In this course, we adhere to the **NumPy/SciPy formatting style**.
You can read the full specification <span style="color: #06402B;">[in the official documentation](https://numpydoc.readthedocs.io/en/latest/format.html)</span>, or simply ask an LLM to "generate a NumPy-style docstring" for your code.

A complete docstring includes:

* **Summary**: A one-line description (max 79 characters).
* **Extended Description**: Details on behavior, edge cases, or algorithmic complexity.
* **Parameters**: A list of arguments, their types, and descriptions.
* **Returns**: Description of the output and its type.
* **Exceptions**: Errors the function might raise.
* **Examples**: Code snippets demonstrating usage.

**Example:**

```python
def add_numbers(a: int, b: int) -> int:
    """Add two numbers together.

    Here would be the place to write the extended description, but this
    function does not really need one...

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

*Tip: LLMs are excellent at drafting docstrings. Paste your function definition and ask for a NumPy-formatted docstring to get a quick head start.*

# Practical guide for refactoring scripts with functions

If you used "rubber ducking," you likely already know which parts of your script are repetitive or messy. To refactor systematically, follow these steps:

**1. Identify repetitive code**

* **Observation**: Look for copy-pasted blocks or logic that appears multiple times with minor variations.
* **Action**: Extract this logic into a single function. This centralizes the logic (SSOT) and adheres to the DRY principle.

**2. Create clear definitions**

* **Observation**: A function is only useful if its purpose is obvious.
* **Action**:
* **Descriptive Name**: The name should be a verb-noun pair that explains the action (e.g., `calculate_mean` vs `do_math`).
* **Single Responsibility**: A function should do *one* thing. If it does three things, break it into three functions. This ensures orthogonality.



**3. Implement with rubber ducking**

* **Observation**: Functions must be self-contained. They cannot rely on variables defined outside of them (global variables).
* **Action**: When writing the function body, explain to your "duck" exactly what data the function needs. These become your **arguments**. If the function needs a dataframe `df`, pass `df` as an argument; do not assume `df` exists globally.

**4. Aggregate into modules**

* **Observation**: As functions multiply, a single file becomes cluttered.
* **Action**: Group related functions into **modules** (Python files) and **packages** (folders with an `__init__.py`).
* **Define Modules**: Group by theme. In a data project, you might have `cleaning.py` and `visualization.py`.
* **Create Structure**:


*A complex project structure:*
```plaintext
my_project/
├── src/
│   ├── data_preprocessing/
│   │   ├── __init__.py
│   │   ├── cleaning.py
│   │   ├── transformation.py
│   │   └── feature_engineering.py
│   ├── data_visualization/
│   │   ├── __init__.py
│   │   ├── plots.py
│   │   └── charts.py
│   └── statistical_analysis/
│       ├── __init__.py
│       ├── regression.py
│       └── hypothesis_testing.py
└── pyproject.toml

```


*A simpler project structure:*
```plaintext
my_project/
├── src/
│   └── my_analysis/
│       ├── __init__.py
│       ├── cleaning.py
│       ├── regression.py
│       └── hypothesis_testing.py
└── pyproject.toml

```



**5. Importing functions**
Once organized, you can import your logic cleanly in your analysis scripts or notebooks:

```python
from src.my_analysis.cleaning import remove_nulls
from src.my_analysis.regression import create_histogram

```

---

Source:\

* Hunt, A., & Thomas, D. (2019). The Pragmatic Programmer: Your journey to mastery. Addison-Wesley. ISBN 9780135957059. (Original publication)\
* Fowler, M. (2018). Refactoring: Improving the design of existing code (2nd ed.). Addison-Wesley Professional. ISBN 013475770X, 9780134757704.\
* [https://numpydoc.readthedocs.io/en/latest/format.html](https://numpydoc.readthedocs.io/en/latest/format.html)\

---

**Would you like me to provide a concrete example of taking a "messy" script and refactoring it into the modular structure described above?**
