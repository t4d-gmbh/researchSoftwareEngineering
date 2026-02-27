# Python Environment Tooling

{% if slide %}

**Runtime Isolation Tooling**
- System-wide installations result in dependency conflicts.
- **Approach**: Project-specific, isolated virtual environments.

::::{grid}
:gutter: 2

:::{grid-item-card} Standard Tooling
**`venv` & `pip`**
- `venv`: Standard library module; generates the isolated `.venv` directory.
- `pip`: Installs packages into the localized directory.
- Requires manual environment activation.
:::

:::{grid-item-card} Modern Tooling
**`uv`**
- Consolidates environment creation, package installation, and execution.
- Manages Python interpreter downloads automatically.
- `uv sync`: Synchronizes dependencies and automatically loads environment variables (`.env`).
- `uv run`: Executes scripts within the isolated context without manual activation.
:::

::::

{% else %}

System-wide Python package installations lead to dependency version conflicts across concurrent projects. This is mitigated by establishing isolated, project-specific virtual environments, ensuring that dependencies, interpreters, and execution contexts remain fully self-contained.

### Standard Tooling: `venv` and `pip`

The standard methodology relies on tools integrated directly into the core Python distribution.

* **`venv`**: A standard library module utilized to generate an isolated environment structure (typically named `.venv`). This directory contains a localized Python interpreter and standard library clone.
* **`pip`**: The standard package installer. Upon manual environment activation (e.g., `source .venv/bin/activate`), `pip` routes all installed packages into the localized `.venv` directory rather than global system paths.

This baseline approach requires the target Python version to be manually pre-installed on the host system prior to environment creation.

### Modern Environment Management: `uv`

Modern workflows frequently utilize [uv](https://docs.astral.sh/uv/), a comprehensive package and project manager. It replaces individual standard tools by consolidating interpreter management, environment creation, and dependency resolution into a single utility. 

**Standard Compatibility**
Despite operating as an independent manager, `uv` is strictly compatible with standard Python conventions. It generates a standard `.venv` directory. Users retain the ability to manually activate the environment (`source .venv/bin/activate`) and interact with it using standard commands.

**Automated Synchronization (`uv sync`)**
The `uv sync` command parses the project's configuration file to automatically download the specified Python interpreter, instantiate the `.venv`, and install all declared dependencies. It natively handles the loading of environment variables from `.env` files.

**Isolated Execution (`uv run`)**
To execute code, `uv run` is utilized. This command automatically identifies the project's virtual environment and executes the specified script strictly within that isolated context, bypassing the requirement for manual environment activation:

```bash
uv run python scripts/data_processing.py

```

{% endif %}
