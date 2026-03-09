## Functions & Classes

{% if slide %}

The primary tool for reusable code: the **function**.

:::::{grid} 2
:gutter: 2

::::{grid-item-card} Benefits
- **Modularity**: break problems into small pieces
- **Abstraction**: hide the "how," expose the "what"
- **Testability**: verify functions in isolation
- **Collaboration**: team members build different functions
::::
::::{grid-item-card} Good design
- Descriptive **verb-noun name** (`calculate_mean`, not `do_math`)
- **Single responsibility**: one function, one job
- **No global variables**: pass everything as arguments
::::
:::::

More advanced codebases can benefit greatly from a more versatile structural coding pattern: the **class**.

:::::{grid} 2
:gutter: 2

::::{grid-item-card} Benefits
- **Encapsulation**: bundle data and behavior
- **State management**: retain data across operations
- **Inheritance**: extend and reuse existing structures
::::
::::{grid-item-card} Good design
- Descriptive **noun name** (PascalCase, e.g., `DataProcessor`)
- **High cohesion**: methods tightly related to class data
- **Low coupling**: minimized dependencies on external components
::::
:::::

{% else %}

### Functions

The primary mechanism for achieving reusable code is the function: a self-contained block of code that accepts inputs, processes them, and returns outputs.

Functions give you modularity (small isolated pieces), abstraction (you can use a function without knowing its internals), testability (verify each one in isolation), and make collaboration straightforward (different people build different functions).

A well-designed function follows a few rules:

- **Descriptive name**: use a verb-noun pair that explains the action, e.g. `calculate_mean` rather than `do_math`.
- **Single responsibility**: one function should do one thing. If it does three things, split it into three functions.
- **No hidden dependencies**: pass all required data as arguments instead of relying on global variables.

#### Docstrings

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

### Classes

For more advanced architectural requirements, the class serves as a versatile structural pattern. A class acts as a blueprint for creating objects (instances), allowing data (attributes) and behavior (methods) to be bundled together into a single logical entity.

Classes provide encapsulation (keeping data and its manipulating functions together), state management (maintaining internal data across multiple method calls), and inheritance (allowing new structures to be derived from existing ones).

A well-designed class adheres to specific principles:

* **Noun-based naming**: Class names should be descriptive nouns utilizing PascalCase (e.g., `DataProcessor`).
* **High cohesion**: A class should represent a single concept, with all its methods closely related to its internal state.
* **Low coupling**: Dependencies on external classes or global states should be minimized to ensure the class can be tested and reused independently.

#### Object-Oriented (OO) Coding Pattern

Object-Oriented Programming (OOP) is a paradigm organized around objects rather than discrete actions, and data rather than pure logic. Implementing OO patterns facilitates the management of complex state and behavior in large, reproducible codebases.

Core OO principles include:

* **Encapsulation**: Internal states are hidden from the outside, preventing unintended interference. Interaction occurs only through well-defined public methods.
* **Inheritance**: Code duplication is reduced by allowing new, specialized classes to inherit properties and methods from generalized parent classes.
* **Polymorphism**: Different classes can be treated uniformly if they share a common interface, enhancing flexibility in code design.

Similar to functions, classes and their methods require comprehensive docstrings to guarantee readability and collaborative potential.

```python
class DataProcessor:
    """A class used to process and scale numerical data.

    Parameters
    ----------
    scaling_factor : float
        The multiplier applied to the data during processing.

    Attributes
    ----------
    scaling_factor : float
        The stored scaling factor.
    """

    def __init__(self, scaling_factor: float):
        self.scaling_factor = scaling_factor

    def scale_value(self, value: float) -> float:
        """Scale a single numerical value.

        Parameters
        ----------
        value : float
            The input value to be scaled.

        Returns
        -------
        float
            The scaled value.
        """
        return value * self.scaling_factor

```

{% endif %}
