{% if build == "slides" %}

## Installation & Usage

{% else %}

## Installation Instructions and Usage Examples

{% endif %}

Clear, reproducible installation steps are the most critical part of your documentation.

{% if slide %}

### The Golden Rule

**Stick to standard tools**

- Use language-standard packaging systems
- Minimize custom installation steps
- Document environment setup explicitly

{% endif %}

{% if page %}

### The Golden Rule: Use Standard Tools

The more non-standard your installation process, the harder it is for others to use your work. Each custom step you add is another potential failure point and another barrier to adoption.

For Python projects, this means adhering to official packaging standards. The `pyproject.toml` file is the [modern standard for Python project configuration](https://peps.python.org/pep-0621/). Combined with Python's built-in `pip` and `venv` tools, installation should reduce to two universal steps.

{% endif %}

{% if build == "slides" %}

### Python Standard Installation

```bash
# 1. Create and activate environment
python -m venv .venv
source .venv/bin/activate

# 2. Install project
pip install -e .
```

**Key points:**
- `.` tells pip to use `pyproject.toml` in current directory
- `-e` (editable) allows live code changes without reinstall

{% endif %}

{% if page %}

### Standard Python Installation Pattern

For Python projects following modern packaging standards:

1. **Create and activate an isolated environment:**
   ```bash
   python -m venv .venv
   source .venv/bin/activate
   ```

2. **Install the project and its dependencies:**
   ```bash
   pip install -e .
   ```

The `.` tells pip to look for the `pyproject.toml` in the current directory. The `-e` (editable) flag is highly recommended for research and development. It installs the package in "symlink mode," meaning changes you make to files in `src/` are immediately reflected without needing to reinstall.

:::{admonition} Reproducibility Benefit
:class: tip
This pattern works identically on Windows, macOS, and Linux. Users don't need to understand your project's internals, they just follow the same two steps regardless of complexity.
:::

### Usage Examples

After installation instructions, provide concrete usage examples. Start with the simplest case:

```python
from myproject import analyze_data

results = analyze_data("input.csv")
print(results.summary())
```

Then show more advanced scenarios. Each example should be runnable, meaning that users should be able to copy-paste and execute them successfully.

{% endif %}
