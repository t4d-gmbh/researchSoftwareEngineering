## Unit Testing

{% if slide %}

:::{admonition} Why test?
:class: tip
- **Quality**: verify correct behavior across inputs and edge cases
- **Safe refactoring**: catch regressions immediately
- **Documentation**: tests show exactly how a function is supposed to behave
:::

{% else %}

Unit testing verifies that individual components (functions, classes) behave exactly as intended.
In the context of refactoring, tests act as your safety net: when you restructure or optimize a function, a test suite catches regressions immediately.

Three reasons to write tests:

- **Quality**: tests verify correct behavior across a range of inputs, including edge cases.
- **Safe refactoring**: if a test fails after cleanup, you know the behavior changed before that change reaches production.
- **Living documentation**: tests show unambiguously how a function should be called and what it returns.

{% endif %}

{% if slide %}

### Getting started with `pytest`

```bash
pip install pytest
```

```python
# src/hoselupf/calculate.py
def calculate_area(length, width):
    """Calculate the area of a rectangle."""
    return length * width
```

```python
# tests/test_calculate.py
from hoselupf.calculate import calculate_area

def test_calculate_area():
    assert calculate_area(2, 3) == 6
    assert calculate_area(0, 5) == 0
    assert calculate_area(-1, 5) == -5
```

```bash
python -m pytest
```

{% else %}

### Setting up `pytest`

[`pytest`](https://docs.pytest.org/en/stable/) is the standard testing framework for Python. To integrate it into your project:

1. **Create a `tests/` directory** in your project root, separate from your source code.
2. **Install pytest**: `pip install pytest`
3. **Write tests** in files named `test_*.py`. pytest discovers these automatically.

Here is a minimal example. Given a function in your source code:

```python
# src/hoselupf/calculate.py
def calculate_area(length, width):
    """Calculate the area of a rectangle."""
    return length * width
```

Write a corresponding test:

```python
# tests/test_calculate.py
from hoselupf.calculate import calculate_area

def test_calculate_area():
    assert calculate_area(2, 3) == 6
    assert calculate_area(0, 5) == 0
    assert calculate_area(-1, 5) == -5
```

4. **Run tests** from your project root:

```bash
python -m pytest
```

`pytest` reports which tests passed and which failed, with tracebacks for failures.
Once your tests pass, you can refactor freely. Just rerun `pytest` after every change.

{% endif %}
