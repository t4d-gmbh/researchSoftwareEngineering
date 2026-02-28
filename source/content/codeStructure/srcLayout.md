## The `src/` Layout

{% if slide %}

**The "src-layout"**
- Instructs the Python interpreter where to find importable code.
- Physically isolates core analysis logic from runtime execution and configuration.
- A directory with an `__init__.py` is treated natively as a **package**.



{% else %}

The `src` directory is central to a well-engineered Python project. Standard tools like `pip`, `uv`, and `setuptools` are designed to natively recognize this structural pattern (often referred to as the "src-layout").

In Python, "installing" a package essentially means directing the interpreter to the code's location so it can be globally imported, regardless of the active working directory. By placing the codebase inside a dedicated folder like `src/mypkgs`, the core analysis logic is physically isolated from runtime scripts and configuration files.

When a subdirectory (e.g., `mypkgs`) containing an `__init__.py` file is instantiated, Python treats it as a **package** (see the [official modules tutorial](https://docs.python.org/3.13/tutorial/modules.html)). Any `.py` file inside becomes a submodule that can be imported, identically to third-party libraries such as `pandas` or `numpy`.

### Example Implementation
{% endif %}

{% if slide %}

::::{grid} 2
:gutter: 2

:::{grid-item-card} 📁 Directory Structure
```plaintext
.
├── scripts/
│   └── run_hello.py
├── src/
│   └── mypkgs/
│       ├── __init__.py
│       └── hello.py
├── pyproject.toml
.

```

:::

:::{grid-item-card} 🧩 Core Logic (`src/`)

```python
# src/mypkgs/hello.py
def say_hello(name: str) -> None:
    """Greets a name"""
    print(f"Hello {name}")

```

:::
::::

{% else %}

Consider the following file structure, which strictly separates the reusable package (`mypkgs`) from the operational execution environment (`scripts`):

```plaintext
.
├── scripts/
│   └── run_hello.py
├── src/
│   └── mypkgs/
│       ├── __init__.py
│       └── hello.py
├── pyproject.toml
.

```

If `hello.py` contains a simple function:

```python
# src/mypkgs/hello.py
def say_hello(name: str) -> None:
    """Greets a name"""
    print(f"Hello {name}")

```

### Editable Installations

{% endif %}

{% if slide %}

**Editable (Development) Installs**
Creates a system symlink to the `src/` directory. Modifications to the underlying Python files are immediately reflected without requiring reinstallation.

::::{grid} 2
:gutter: 2

:::{grid-item-card} ⚙️ Installation

```bash
# Using modern uv tooling
uv sync

# Using standard pip
pip install -e .

```

:::

:::{grid-item-card} 🚀 Execution (`scripts/`)

```python
# scripts/run_hello.py
from mypkgs.hello import say_hello

if __name__ == "__main__":
    say_hello(name="Bob")

```

:::
::::

{% else %}

Assuming a valid `pyproject.toml` configuration is present at the repository root, this local package can be integrated into the active virtual environment in "editable" (or development) mode. An editable install creates a symlink to the `src/` directory, meaning any modifications to the underlying Python files are immediately reflected across the system without requiring reinstallation.

**1. Install the project**
Utilizing modern tooling like `uv`, synchronization automatically installs the local package defined in `pyproject.toml` in editable mode:

```bash
uv sync

```

Alternatively, utilizing the standard `pip` installer:

```bash
pip install -e .

```

**2. Import and execute**
Once installed, the functions can be imported into any operational script, notebook, or shell operating within that virtual environment. The script acts purely as the execution trigger, importing the logic from the isolated package:

```python
# scripts/run_hello.py
from mypkgs.hello import say_hello

if __name__ == "__main__":
    # Executes the logic defined in src/mypkgs/hello.py
    say_hello(name="Bob")

```

{% endif %}
