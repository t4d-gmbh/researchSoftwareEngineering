(pillarsSoC)=
# 4 Pillars of SoC

:::{admonition} The Four Pillars of SoC
:class: tip, margin
{% if slide %}
Environment. Configuration. Code. Data.
{% else %}
True computational reproducibility mandates the rigid Separation of Concerns (SoC) across four distinct, isolated pillars. Failure to isolate these concerns leads to security vulnerabilities (credentials in Git), rigid codebases, non-reproducible environments, and data integrity failures.
{% endif %}
:::
{% if slide %}

```{compound}
{.centered}
An optimized strategy for managing the interaction of Environment, Configuration, Code, and Data.

```

{% else %}

Effective data handling is critical for computational efficiency, reproducibility, and scientific integrity. Within a modern computational project, data must not be treated as an ephemeral byproduct but as a first-class citizen governed by a deliberate strategy.

This strategy hinges on the strict application of the **Separation of Concerns (SoC)** principle. Concerns are separated into four distinct pillars, which only intersect at the moment of execution within a controlled script:

1. **Environment** (Software stack and runtime context)
2. **Configuration** (Static algorithmic parameters)
3. **Code** (Reusable logic vs. execution coordination)
4. **Data** (Actual data vs. state declarations)

#### The Four Pillars of SoC

{% endif %}

::::{grid} 1 1 2 2
:gutter: 2

:::{grid-item-card} Pillar 1: Environment
:class: sd-m-auto

{% if page %}
Defines the software stack, underlying OS context, and dynamic runtime information.
{% endif %}

* **Build-time Context:** Defines the static software image.
{% if page %}
  * *Declarations:* `pyproject.toml`, `Conda.yml`.
  * *Definition Artifacts:* `containers/` folder holding `.def` or `Dockerfiles`.
{% endif %}


* **Runtime Context:** Defines the dynamic execution state and secrets.
{% if page %}
  * *Mechanisms:* Utilizes local `.env` files (git-ignored).
  * *Content:* Passed via system environment variables; contains credentials, dynamic API keys, and compute resource definitions.
{% endif %}

:::
:::{grid-item-card} Pillar 2: Configuration
:class: sd-m-auto

{.smaller}
The `config/` folder

Defines the static parameters required by the algorithmic logic.

{% if page %}
* **Declarations:** Structured YAML/TOML files (e.g., Hydra configs).
* **Content:** Model hyperparameters (learning rates, layer counts), data processing options, and application-specific settings.
* **Constraint:** **Never** contains credentials or secrets (passed via runtime environment).
{% endif %}

:::
:::{grid-item-card} Pillar 3: Code
:class: sd-m-auto

{% if page %}
The algorithmic logic, rigidly separated into reusable building blocks and execution coordination.
{% endif %}

* **Reusable Logic (`/src`)**: Clean, library-like algorithmic code.
{% if page %}
  * **Independent on** Pillar 1 (Environment variables) or Pillar 2 (Configuration loading logic).
{% endif %}
* **Execution Scripts (`/scripts`)**: The "conductor."
{% if page %}
  These scripts are the *only* intersection point where all pillars combine: they read dynamic context (Pillar 1), load static parameters (Pillar 2), import reusable logic from `/src` (Pillar 3), and act upon data declared in `/data` (Pillar 4).
{% endif %}

:::
:::{grid-item-card} Pillar 4: Data
:class: sd-m-auto

{.smaller}
The `data/` folder

{% if page %}
Manages the project state (inputs, intermediates, outputs). A strict distinction is made between attached data and data definitions ("metadata").
{% endif %}

* **Attached (Actual) Data**{% if page %}:  
  Should only contain small, immutable datasets localized to the repository (e.g., tiny test cases).
  {% endif %}
* **Data "Metadata" & Declarations**{% if page %}:  
  Defines WHERE data is and how to access it, rather than hosting it.
  * *Declarations:* Contains DVC (Data Version Control) files, Git LFS pointer files, or Git Submodules.
  * *Access Info:* Object Storage URLs, bucket names, and endpoint paths.
{% endif %}

:::
::::
