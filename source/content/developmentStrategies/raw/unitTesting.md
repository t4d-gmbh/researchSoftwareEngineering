# Unit Testing

Unit testing is a fundamental practice in software engineering that involves verifying that individual components—such as functions or classes—work exactly as intended.

In the context of refactoring, unit testing acts as your safety net.
When you dismantle a script to extract functions, or when you optimize those functions later, you run the risk of breaking existing logic.
A robust suite of unit tests ensures that if you accidentally break something, you will know immediately. This allows you to refactor with confidence, knowing that regressions will be caught instantly.

## The importance of unit testing

* **Ensures code quality**: Tests verify that a function behaves correctly across a range of inputs, including edge cases.
* **Facilitates refactoring**: You cannot safely refactor code without tests. If a test fails after you clean up a function, it flags that the behavior has changed, prompting you to fix it before it becomes a bug in production.
* **Acts as live documentation**: Tests provide unambiguous examples of how a function is supposed to be used and what it returns, often serving as better documentation than the docstrings themselves.

## In practice: setting up unit testing with `pytest`

To implement unit testing, we recommend the [pytest](https://docs.pytest.org/en/stable/) framework. It is the industry standard for Python due to its simplicity and powerful features.

Follow these steps to integrate testing into your project:

1. **Create a directory for tests:**
Create a folder named `tests/` in your project root. Keeping tests separate from source code (`src/`) is a best practice for project organization.
2. **Install `pytest`:**
Ensure `pytest` is installed in your environment.
```bash
pip install pytest

```


It is also best practice to track testing dependencies separately. Add `pytest` to a dedicated `tests/requirements.txt` file:
```bash
pip freeze | grep pytest >> tests/requirements.txt

```


3. **Write unit tests:**
Create a new Python file in the `tests/` folder (e.g., `test_calculate.py`).
`pytest` automatically detects files starting with `test_` and functions starting with `test_`.
*Example:*
*In your source code (`src/hoselupf/calculate.py`):*
```python
def calculate_area(length, width):
    """Calculate the area of a rectangle."""
    return length * width

```


*In your test file (`tests/test_calculate.py`):*
```python
from hoselupf.calculate import calculate_area

def test_calculate_area():
    # Test standard case
    assert calculate_area(2, 3) == 6
    # Test edge cases
    assert calculate_area(0, 5) == 0
    assert calculate_area(-1, 5) == -5

```


4. **Run your tests:**
Navigate to your project root in the terminal.
* Activate your virtual environment.
* Install testing dependencies (e.g., `pip install -r tests/requirements.txt`).
* Run the tests:
```bash
python -m pytest

```




You will see a report indicating which tests passed (green dots) and which failed (red Fs), along with detailed tracebacks for failures.
5. **Refactor with confidence:**
Once your tests are passing, you can optimize or clean up `calculate_area`.
After every change, simply rerun `pytest`. If the tests pass, your refactoring was successful and safe.

By incorporating unit testing into your workflow, you transform your code from a fragile script into a robust, maintainable software package.

---

Source:\

* [https://docs.pytest.org/en/stable/](https://docs.pytest.org/en/stable/)\
