### Standardized Configuration

::::{grid}
:gutter: 2

:::{grid-item}
:class: sd-m-auto

{% if slide %}


**The `pyproject.toml` Standard**
- **Build System**: Defines how the package is constructed.
- **Metadata**: Centralizes versioning, authorship, and licensing.
- **Dependencies**: Explicitly declares runtime packages and Python versions.
- **Optional Dependencies**: Isolates execution contexts (e.g., testing).
- **Tool Configuration**: Centralizes settings for optional toosl (e.g. linters, testing).

{% else %}

While tools execute the installation, the environment and project specifications must be declaratively defined.
The modern Python packaging standard dictates the use of a `pyproject.toml` file.
This file serves as the centralized configuration matrix for the project, replacing legacy files such as `requirements.txt`, `setup.py`, and `setup.cfg`.

{% endif %}
:::
:::{grid-item}
:class: sd-m-auto

```TOML
# ./pyproject.toml
[project]
name = "your_project_name"
authors = [
  { name="Your Name", email="your.email@example.com" },
]
description = "Brief description of your project"
readme = "README.md"
requires-python = "~=3.13.0"
license.file = "LICENSE"
dependencies = [ "numpy==2.3.5", ]
[project.urls]
Homepage = "https://github.com/j-i-l/pythonProject"

[dependency-groups]
test = [ "pytest~=7.4.3", ]
docs = [ "Sphinx==8.1.3", ]
dev = [{include-group = "test"},
       {include-group = "docs"},
       "black>=23.0", ]

[tool.hatch.version]
source = "vcs"

[build-system]
requires = ["hatchling", "hatch-vcs"]
build-backend = "hatchling.build"
```
:::

{% if slide %}

**Handling System Binaries:**
- **Conda**: System-level isolation for complex binaries (e.g., CUDA).
- **Pixi**: Integrates Conda-ecosystem resolution directly into `pyproject.toml`.

{% else %}

#### Comprehensive Project Configuration

The `pyproject.toml` structure is divided into specific tables that govern distinct aspects of the software project.

**1. Build System Instructions (`[build-system]`)**
This table defines the backend required to package the codebase into installable distributions (wheels and source distributions). Standard backends include `hatchling`, `flit-core`, or `setuptools`.

**2. Project Metadata and Versioning (`[project]`)**
Core project metadata is strictly formalized under [PEP 621](https://peps.python.org/pep-0621/). This table standardizes the declaration of the project's name, versioning scheme (which can be static or dynamically derived from [Git tags](https://t4d-gmbh.github.io/using-git-in-academia/content/working-with-git/source/content/elements/index.html#:~:text=the%20main%20codebase.-,Tags,-A%20%20tag%20is)), description, designated entry points, license types, and authorship information. It acts as the primary source of truth for repository information.

**3. Dependency Declarations**
Within the `[project]` table, the runtime execution context is defined:
* `requires-python`: Dictates the compatible Python interpreter versions.
* `dependencies`: An array of the core external packages strictly required for the software to function.

**4. Optional Dependencies (`[project.optional-dependencies]`)**
Optional dependencies are utilized to define distinct, compartmentalized execution contexts without polluting the core runtime environment. They permit the specification of additional packages required exclusively for specific workflows, such as executing test suites (e.g., including `pytest` and code coverage modules), generating documentation (e.g., `sphinx`), or configuring developer environments.

**5. Tool Configuration (`[tool.*]`)**
The configuration of external developer tools is consolidated within the `pyproject.toml`. Tables such as `[tool.pytest.ini_options]` or `[tool.ruff]` dictate the behavior of test runners, static type checkers, linters, and code formatters, ensuring uniform configurations across all execution environments.

:::{admonition} Interpreter vs. Compilers
:class: tip
An *interpreter* is a program that directly executes instructions written in a programming language, line by line, without requiring prior compilation into machine code. In Python's case, the interpreter (e.g., `python3`) reads and runs `.py` files at runtime.
*Compilers* translate the entire program at once, creating an executable file that runs quickly, whereas interpreters translate and execute code line-by-line, making them slower but easier for debugging.
:::

#### Alternative Ecosystems

Standard Python tooling occasionally fails when projects require complex non-Python dependencies, such as specific C++ compilers, system-level libraries, or GPU drivers.
In these instances, alternative ecosystems are utilized.

**[Conda](https://docs.conda.io/en/latest/)**
The `conda` package manager isolates environments at the system level rather than strictly at the Python package level. It installs Python itself alongside necessary system binaries. Conda typically relies on an independent configuration format (`environment.yml`).

**[Pixi](https://pixi.prefix.dev/latest/)**
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

**Additional resources**:  
* Structure and format of TOML files [en.wikipedia.org/wiki/TOML](https://en.wikipedia.org/wiki/TOML), [toml.io/en/latest](https://toml.io/en/latest)

{% endif %}
