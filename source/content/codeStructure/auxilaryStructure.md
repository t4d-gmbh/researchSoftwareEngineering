## Testing and Documentation

{% if slide %}

**Independent Validation and Communication**
Auxiliary tasks should be structurally isolated into independent locations.

### Testing Isolation and Scope

::::{grid} 2
:gutter: 2

:::{grid-item-card} ✅ Validation Target (`src/`)
- The `tests/` directory is dedicated **exclusively** to verifying reusable logic.
- Tests import pure functions from `src/` to assert expected outputs based on controlled inputs.
:::

:::{grid-item-card} 🚫 Strict Ignorance
- Tests **must ignore** `scripts/` and `notebooks/`.
- Execution endpoints are inherently stateful and lack modularity.
- Complex logic must be extracted to `src/` before it can be reliably tested.
:::
::::

{% else %}
Beyond the core analytical logic and execution scripts, a robust codebase requires dedicated infrastructure for functional validation and communication.
According to the principle of Separation of Concerns, these auxiliary tasks must be structurally isolated into their own independent locations.

### Testing Isolation and Scope


The `tests/` directory is dedicated exclusively to verifying the reusable logic contained within the `src/` package.
A testing framework (such as `pytest`) operates by importing the pure functions and classes from `src/` and asserting that they produce the expected outputs given controlled inputs.

Crucially, **the testing framework must strictly ignore the `scripts/` and `notebooks/` directories**.
Operational scripts and interactive notebooks are execution endpoints.
They are inherently stateful, dependent on specific environment variables, and heavily coupled to external data files or network connections.
Because they lack modularity, they are practically impossible to unit test reliably. 

This structural rule enforces codebase hygiene: if a procedural script or a Jupyter notebook contains complex data-processing logic that requires validation, that logic is in the wrong place.
It must be extracted, generalized, and moved into the `src/` directory.
Once in `src/`, it can be safely imported by the test suite for validation, and subsequently imported back into the script for execution.
{% endif %}

## Dependency Separation via `pyproject.toml`

{% if slide %}

**Consolidated Dependency Management**
Modern Python projects utilize the central `pyproject.toml` to declare isolated dependencies for auxiliary tasks via **optional dependencies** or **dependency groups**, enforcing Separation of Concerns without scattering configuration files.



::::{grid} 2
:gutter: 2

:::{grid-item-card} 📄 `pyproject.toml`
```toml
[project]
dependencies = ["pandas", "numpy"]

[project.optional-dependencies]
test = ["pytest", "pytest-cov"]
docs = ["sphinx", "mkdocs"]

```

:::

:::{grid-item-card} ⚙️ Isolated Installation
Auxiliary dependencies are strictly isolated and installed only when explicitly requested:

```bash
# Modern uv tooling
uv sync --extra test

# Standard pip
pip install -e .[test]

```

:::
::::

{% else %}

Because testing and documentation are independent concerns, their software dependencies must remain isolated from the primary analysis environment.

Historically, this isolation was achieved by placing distinct `requirements.txt` files inside the `tests/` and `docs/` directories. However, modern Python packaging consolidates these declarations within the central `pyproject.toml` file utilizing **optional dependencies** (or modern dependency groups).

This approach maintains strict environment isolation while centralizing dependency management. It delineates the operating environments into distinct categories:

* **Core Dependencies**: Required to execute the operational data pipeline (e.g., `pandas`, `scikit-learn`).
* **Test Dependencies**: Required exclusively for functional validation (e.g., `pytest`, `pytest-cov`).
* **Documentation Dependencies**: Required exclusively for generating static sites (e.g., `sphinx`, `mkdocs`).

### Example `pyproject.toml` Configuration

By defining auxiliary domains as optional extras, the primary execution environment remains lightweight and free of unnecessary bloat. Only the core dependencies are installed by default:

```toml
[project]
name = "mypkgs"
version = "0.1.0"
# Core dependencies installed by default
dependencies = [
    "pandas>=2.0.0",
    "numpy>=1.24.0"
]

[project.optional-dependencies]
# Auxiliary dependencies installed only upon request
test = [
    "pytest>=7.0", 
    "pytest-cov"
]
docs = [
    "sphinx", 
    "mkdocs"
]

```

### Explicit Installation

When provisioning the environment for a specific task (e.g., running the CI/CD testing pipeline), the auxiliary dependencies are explicitly invoked. The core analysis environment remains unaffected unless these flags are passed.

Utilizing modern `uv` synchronization:

```bash
# Installs core dependencies + testing tools
uv sync --extra test

```

Utilizing the standard `pip` installer:

```bash
# Installs the local package in editable mode + testing tools
pip install -e .[test]

```

### Note on Notebooks and Documentation
While tools like Quarto or Jupyter Book allow documents to be authored directly using `.ipynb` notebooks, these source notebooks should generally remain within the `notebooks/` directory.

The `docs/` folder is strictly reserved for the structural configuration, styling templates, and static assets required to compile those source notebooks and the `src/` package docstrings into a final, deployable website or book.
{% endif %}
