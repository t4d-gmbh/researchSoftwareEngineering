## Installation & Usage

{% if page %}
Clear, reproducible installation steps are the most critical part of your documentation.
{% endif %}

{.centered}
The Golden Rule:

{.centered}
{.bigger}
**Use Standard Tools**

{% if slide %}
**Stick to standard, modern tools**

- Use language-standard packaging systems (`pyproject.toml`)
- Minimize custom installation steps
- Document environment setup explicitly

{% else %}

The more non-standard your installation process, the harder it is for others to use your work.
Each custom step you add is another potential failure point and another barrier to adoption.

For Python projects, this means adhering to official packaging standards.
The `pyproject.toml` file is the [modern standard for Python project configuration](https://peps.python.org/pep-0621/).
Combined with a project manager like `uv`, installation reduces to a single, universal command.

{% endif %}

### Installation

{% if slide %}
**Example**: Python-based project using `uv`.

::::{grid}
:gutter: 2

:::{grid-item}
:class: sd-m-auto

1. Clone the repository:
   ```
   git clone https://github.com/<owner>/<repo-name>.git
   cd repo-name
   ```
2. Install python version, create environment and install project:
   ```bash
   uv sync
   ```
:::
:::{grid-item-card} Key points:
:class: sd-m-auto

* `uv sync` directly uses the Python version declared in the `pyproject.toml`
* `uv sync` automatically creates an isolated `.venv`
* It reads `pyproject.toml` to install all dependencies
* The project is installed in editable mode by default
:::
::::

{% else %}

For Python projects following modern packaging standards, we recommend using [`uv`](https://docs.astral.sh/uv/), a fast Python package and project manager written in Rust.

**A. Develop locally (Clone and Sync):**

1. Clone the repository:
   ```
   git clone https://github.com/<owner>/<repo-name>.git
   cd repo-name
   ```
2. Install python version, create environment and install project:
   ```bash
   uv sync
   ```

Running `uv sync` handles everything for you: it installs the required Python version, creates an isolated virtual environment (`.venv`), resolves your dependencies from the `pyproject.toml`, and installs them.

By default, it installs your package in "editable" (symlink) mode, meaning changes you make to the source code are immediately reflected without needing to reinstall.

**B. Install the package directly from GitHub:**
If you only want to use the package and its dependencies without modifying the source code, you can install it directly into your active environment from the repository:

1. Setup or activeate your virtual environment using python 3.13:
   ```
   uv venv --python 3.13
   ```
2. Install the package directly from GitHub:
   ```
   uv pip install git+https://github.com/<owner>/<repo-name>.git
   ```

:::{admonition} Reproducibility Benefit
:class: tip
This pattern works identically on Windows, macOS, and Linux.
Users don't need to understand your project's internals, manually create virtual environments, or worry about pip versions — they just use standard `uv` commands regardless of complexity.
:::

{% endif %}

### Usage

{% if slide %}
**Example**: Python-based project using `uv`.

Provide a minimal, copy-pasteable example:

```bash
uv run python scripts/drafts/hello.py

```

{% else %}

Provide a copy-pasteable use case with expected output:

```bash
uv run python scripts/drafts/hello.py

```

**Expected Output:**

```text
Job completed. Results safely written to /app/results/output_hello.txt

```

`uv run` automatically detects the `.venv` and safely executes your code without requiring you to manually activate the environment.

*(Alternatively, you can manually activate the environment using `source .venv/bin/activate`, and simply run `python scripts/drafts/hello.py`)*.

:::{admonition} Extended Documentation
To keep the `README.md` concise, advanced scenarios should not be detailed directly here.
Instead, refer to the extended documentation (e.g., under the `docs/` folder) or provide direct links to advanced scripts.
:::

{% endif %}
