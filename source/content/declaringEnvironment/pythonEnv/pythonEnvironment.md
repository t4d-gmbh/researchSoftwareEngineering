### Python Environment Tooling

{% if slide %}

**Runtime Isolation Tooling**

* System-wide installations result in dependency conflicts.
* **Approach**: Project-specific, isolated virtual environments.

::::{grid}
:gutter: 2

:::{grid-item-card} Standard Tooling
**`venv` & `pip` & `dotenv**`

* `venv`: Generates the isolated `.venv` directory.
* `pip`: Installs packages into the localized directory.
* Requires manual environment activation.
* `dotenv`: CLI tool to inject `.env` variables into the runtime (`dotenv run -- python ...`).
:::

:::{grid-item-card} Modern Tooling
**`uv`**

* Consolidates environment creation, package installation, and execution.
* `uv sync`: Synchronizes dependencies (Relies on native shell variables; does NOT support `.env` files).
* `uv run`: Executes scripts within the isolated context.
* **Strict Isolation**: `uv run` ignores `.env` files by default, but can be included (`UV_ENV_FILE=.env` or `uv run --env-file .env ...`).
:::

::::

{% else %}

System-wide Python package installations lead to dependency version conflicts across concurrent projects. This is mitigated by establishing isolated, project-specific virtual environments, ensuring that dependencies, interpreters, and execution contexts remain fully self-contained.

#### Standard Tooling: `venv`, `pip`, and `dotenv`

The standard methodology relies on tools integrated directly into the core Python distribution, supplemented by external CLI utilities for environment management.

* **`venv`**: A standard library module utilized to generate an isolated environment structure (typically named `.venv`). This directory contains a localized Python interpreter and standard library clone.
* **`pip`**: The standard package installer. Upon manual environment activation (e.g., `source .venv/bin/activate`), `pip` routes all installed packages into the localized `.venv` directory rather than global system paths.
* **`dotenv`**: To adhere to the Separation of Concerns principle, environment variables should not be loaded within the Python code itself. Instead, the `dotenv` CLI tool (provided by the `python-dotenv` package) is utilized to wrap the execution, injecting the variables from the `.env` file directly into the script's environment:

```bash
dotenv run -- python scripts/data_processing.py

```

This baseline approach requires the target Python version to be manually pre-installed on the host system prior to environment creation.

#### Modern Tooling: `uv`

Modern workflows frequently utilize [uv](https://docs.astral.sh/uv/), a comprehensive package and project manager. It replaces individual standard tools by consolidating interpreter management, environment creation, and dependency resolution into a single utility.

**Standard Compatibility**
Despite operating as an independent manager, `uv` is strictly compatible with standard Python conventions. It generates a standard `.venv` directory. Users retain the ability to manually activate the environment (`source .venv/bin/activate`) and interact with it using standard commands.

**Automated Synchronization (`uv sync`)**
The `uv sync` command parses the project's configuration file to automatically download the specified Python interpreter, instantiate the `.venv`, and install all declared dependencies.

**Isolated Execution (`uv run`)**
To execute code, `uv run` is utilized.
This command automatically identifies the project's virtual environment and executes the specified script strictly within that isolated context, bypassing the requirement for manual environment activation.

To prevent implicit state and unexpected behaviors, `uv run` intentionally ignores `.env` files by default.
However, `uv` allows to pragmatically include environmental variables by setting the `UV_ENV_FILE` variable:

```bash
export UV_ENV_FILE=.env
uv run scripts/data_processing.py
```

To load local environment variables during execution, the target file can also be explicitly declared via the CLI flag:

```bash
uv run --env-file .env scripts/data_processing.py
```

{% endif %}
