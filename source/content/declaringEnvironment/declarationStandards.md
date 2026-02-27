# Standardized Configuration

{% if slide %}

**The `pyproject.toml` Standard**
- **Build System**: Defines how the package is constructed (PEP 518).
- **Metadata**: Centralizes versioning, authorship, and licensing (PEP 621).
- **Dependencies**: Explicitly declares runtime packages and Python versions.
- **Optional Dependencies**: Isolates execution contexts (e.g., packages needed exclusively for testing).
- **Tool Configuration**: Centralizes settings for formatters, linters, and testing frameworks.

**Handling System Binaries:**
- **Conda**: System-level isolation for complex binaries (e.g., CUDA).
- **Pixi**: Integrates Conda-ecosystem resolution directly into `pyproject.toml`.

{% else %}

While tools execute the installation, the environment and project specifications must be declaratively defined. The modern Python packaging standard dictates the use of a `pyproject.toml` file. This file serves as the centralized configuration matrix for the project, replacing legacy files such as `requirements.txt`, `setup.py`, and `setup.cfg`.

### Comprehensive Project Configuration

The `pyproject.toml` structure is divided into specific tables that govern distinct aspects of the software project.

**1. Build System Instructions (`[build-system]`)**
This table defines the backend required to package the codebase into installable distributions (wheels and source distributions). Standard backends include `hatchling`, `flit-core`, or `setuptools`.

**2. Project Metadata and Versioning (`[project]`)**
Core project metadata is strictly formalized under PEP 621. This table standardizes the declaration of the project's name, versioning scheme (which can be static or dynamically derived from Git tags), description, designated entry points, license types, and authorship information. It acts as the primary source of truth for repository information.

**3. Dependency Declarations**
Within the `[project]` table, the runtime execution context is defined:
* `requires-python`: Dictates the compatible Python interpreter versions.
* `dependencies`: An array of the core external packages strictly required for the software to function.

**4. Optional Dependencies (`[project.optional-dependencies]`)**
Optional dependencies are utilized to define distinct, compartmentalized execution contexts without polluting the core runtime environment. They permit the specification of additional packages required exclusively for specific workflows, such as executing test suites (e.g., including `pytest` and code coverage modules), generating documentation (e.g., `sphinx`), or configuring developer environments.

**5. Tool Configuration (`[tool.*]`)**
The configuration of external developer tools is consolidated within the `pyproject.toml`. Tables such as `[tool.pytest.ini_options]` or `[tool.ruff]` dictate the behavior of test runners, static type checkers, linters, and code formatters, ensuring uniform configurations across all execution environments.

```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[project]
name = "research-software-project"
version = "0.1.0"
description = "Computational project for data analysis."
readme = "README.md"
license = {text = "MIT"}
authors = [{name = "Research Lab", email = "lab@institution.edu"}]
requires-python = ">=3.11"
dependencies = [
    "numpy>=1.24.0",
    "pandas>=2.0.0",
]

[project.optional-dependencies]
testing = ["pytest", "pytest-cov"]

[tool.ruff]
line-length = 88

```

### Alternative Ecosystems: `conda` and `pixi`

Standard Python tooling occasionally fails when projects require complex non-Python dependencies, such as specific C++ compilers, system-level libraries, or GPU drivers. In these instances, alternative ecosystems are utilized.

**Conda**
The `conda` package manager isolates environments at the system level rather than strictly at the Python package level. It installs Python itself alongside necessary system binaries. Conda typically relies on an independent configuration format (`environment.yml`).

**Pixi**
`pixi` is a modern package manager that leverages the Conda ecosystem for binary resolution but integrates directly into the standard Python configuration workflow. It bridges the gap between Python standards and Conda binaries by extending the `pyproject.toml`.

To utilize `pixi`, a dedicated `[tool.pixi]` table is appended to the `pyproject.toml`. This defines Conda-specific channels, dependencies, and system requirements without violating standard Python packaging rules:

```toml
[tool.pixi.project]
channels = ["conda-forge"]
platforms = ["linux-64", "osx-arm64"]

[tool.pixi.dependencies]
python = "3.11.*"
cuda-toolkit = "11.8.*"

```

{% endif %}
