## Codebase Architecture

{% if slide %}

**Separation of Concerns (SoC)**
A structural foundation that physically isolates distinct operational domains: code, configuration, environment, infrastructure, and data.



{% else %}
A reproducible and scalable computational project requires a structural foundation that enforces the Separation of Concerns (SoC).
The codebase must be organized so that distinct operational domains, like code, configuration parameters, environment variables, infrastructure definitions, and data, are as isolated from one another as possible. 

By designing the directory structure to reflect these boundaries, the codebase naturally prevents the entanglement of logic and configuration.
Furthermore, the structural separation guarantees that core analytical logic can be reused across multiple execution contexts without duplicating code.



### Directory Roles
{% endif %}

{% if slide %}

::::{grid} 2
:gutter: 2

:::{grid-item-card} 🧠 `src/` (Core Logic)
Contains the generalized, reusable Python code.
Functions are agnostic to state and wait to be imported.
:::

:::{grid-item-card} 🚀 `scripts/` (Operational Execution)
Procedural entry points (`train.py`).
They rely on environmental variables, parse configs, and apply them to `src/` logic.
:::

:::{grid-item-card} 📓 `notebooks/` (Exploration)
Reserved exclusively for EDA and prototyping.
Imports from `src/`, but is never imported itself.
:::

:::{grid-item-card} 📦 `containers/` (Infrastructure)
Houses declarative blueprints (`Dockerfile`, `Apptainer.def`), keeping the repository root clean.
:::

:::{grid-item-card} 💾 `data/`
Strictly version-controlled directory containing raw and processed datasets, isolated from execution logic.
:::

::::

*This structure allows the exact same `src/` logic to be executed interactively in `notebooks/` or automatically via `scripts/`, within a reproducible environment defined in `containers/`.*

{% else %}
To achieve this separation, a standard repository utilizes distinct top-level directories, each serving a singular purpose:

* **`src/` (Core Logic)**:  
  Contains the generalized, reusable Python package.
  Functions and classes defined here do not execute independently; they wait to be imported.
  They remain agnostic to external configurations and environment states.
* **`scripts/` (Operational Execution)**:  
  Contains the procedural entry points (e.g., `train_model.py`, `download_data.py`).
  These scripts act as the orchestrators: they load the environment variables (`.env`), parse the configuration parameters, and apply them to the reusable logic imported from the `src/` directory.
* **`notebooks/` (Exploration and Prototyping)**:  
  Reserved exclusively for Jupyter notebooks utilized for Exploratory Data Analysis (EDA), prototyping, and interactive visualization.
  Notebooks import the core logic from `src/` but are never imported themselves.
* **`containers/` (Infrastructure Manifests)**:  
  Houses the declarative environment blueprints (e.g., `Dockerfile`, `Apptainer.def`). 
  Isolating these manifests ensures the repository root remains clean and strictly uncouples system-level dependencies from the Python application logic.
* **`data/`**:  
  The strictly version-controlled directory containing raw and processed datasets, isolated from the execution logic.

By structuring the project in this manner, an analysis pipeline can be run identically via an automated script in the `scripts/` folder or interactively within the `notebooks/` folder, simply by importing the same underlying function from `src/`, all while executing within a reproducible system environment defined in `containers/`.
{% endif %}
