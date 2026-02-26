### Separation of Concerns (SoC)

{% if page %}
When organizing scientific projects (especially in data science) one principle stands above the rest:
{% endif %}

{.centered}
{.bigger}
**The separation of logic, parameters, environment, and data**

{% if page %}
This principle, known as Separation of Concerns (SoC), is fundamental for reproducibility, clarity, and maintainability. It dictates how the digital artifacts of a project should be physically organized on disk, ensuring that a change in one domain (e.g., running the code on a different computer) does not require a change in another (e.g., modifying the core logic).
{% endif %}

{% if slide %}

::::::{tab-set}
:::::{tab-item} Basic

::::{grid} 1 1 2 2
:gutter: 3

:::{grid-item}
```bash
my_data_science_project/
│
├── config/            # Centralized parameterizations
├── data/              # Input data
└── code/              # Code and scripts
.  
.

```

:::

:::{grid-item}
**Key Takeaways:**

* **Foundational separation:** Code is physically isolated from configuration parameters and datasets.
* **Portability:** Hardcoded paths and parameters are explicitly eliminated from the source code.
* **Clarity:** The core domains of the project are immediately identifiable to collaborators.
:::

::::
:::::

:::::{tab-item} Best Practice
::::{grid} 1 1 2 2
:gutter: 3

:::{grid-item}

```bash
my_data_science_project/
│
├── config/            # Parameters (YAML/TOML)
├── .env               # Environment/State (paths, secrets)
│
├── scripts/           # Logic (execution)
│
├── data/              # Data (inputs)
└── results/           # Data (outputs/deliverables)
.
.

```

:::

:::{grid-item}
**Key Takeaways:**

* **Environment isolation:** Local paths and secrets are extracted to `.env` files.
* **Security:** The `.env` file must never be committed to version control.
* **Dynamic loading:** Paths are fetched programmatically at runtime rather than hardcoded:

```python
import os
from dotenv import load_dotenv
# Load local .env variables
load_dotenv()
# Fetch environment-specific paths
output_dir = os.getenv("OUTPUT_DIR")
```

:::
::::
:::::

:::::{tab-item} Advanced
::::{grid} 1 1 2 2
:gutter: 3

:::{grid-item}

```bash
my_data_science_project/
│
├── data/
│   ├── raw/           # Immutable data dumps
│   ├── interim/       # Intermediary data
│   └── final/         # Cleaned, tidy data
│
├── src/               # Reusable logic (Python package)
├── scripts/           # Executable logic (batch scripts)
│
├── config/            # Parameters
├── .env               # Environment state
└── results/           # Outputs
.
.

```

:::

:::{grid-item}
**Key Takeaways:**

* **Logic division:** Reusable modules (`src/`) are strictly separated from executable routines (`scripts/`).
* **Data lineage:** Data is divided into discrete stages to document processing steps and transformations.
* **Immutability:** Raw data is strictly preserved and never overwritten by analytical scripts.
:::
::::
:::::

:::::{tab-item} + Metadata
::::{grid} 1 1 2 2
:gutter: 3

:::{grid-item}

```bash
my_data_science_project/
│
├── data/              # (raw, interim, final)
├── src/               # (reusable logic)
├── scripts/           # (executable logic)
├── results/           # (outputs)
├── config/            # (parameters)
│
├── docs/              # Documentation source files
├── pyproject.toml     # Project metadata and dependencies
├── README.md          # Project overview
├── LICENSE            # Usage rights
├── .env.example       # Environment template
└── .gitignore         # Version control exclusions

```

:::

:::{grid-item}
**Key Takeaways:**

* **Self-description:** Essential context and usage instructions are provided at the root level.
* **Dependency management:** Required packages and metadata are defined centrally (e.g., `pyproject.toml`).
* **Safe onboarding:** Templates (`.env.example`) are provided so collaborators can safely configure their local environments without sharing secrets.
:::
::::
:::::
::::::

{% else %}

At the most basic level, Separation of Concerns implies creating distinct subdirectories to separate the code from its configuration and the data it operates on:

```bash
my_data_science_project/
│
├── config/            # Directory for configuration files
├── data/              # Directory for input data
└── code/              # Directory for programming logic
.  
.


```

However, a robust project structure goes deeper. Best practice requires explicitly separating logic, parameters, environment/state, and the data inputs/outputs. Hardcoding data paths or attempting to store massive datasets within a repository is highly discouraged. By introducing an `.env` file and distinct input/output directories, the project becomes modular and environment-agnostic:

```bash
my_data_science_project/
│
├── config/            # Parameters: Centralized parameterizations (YAML/TOML)
├── .env               # Environment: Local paths and secrets (DO NOT COMMIT)
│
├── scripts/           # Logic: Python scripts for exploration and analysis
│
├── data/              # Data (Input): Kept small or used for symlinks
└── results/           # Data (Output): Plots, figures, tables
.
.


```

**Using Environment Variables**
The `.env` file defines local variables, such as absolute paths to external storage drives where the actual training data or output directories reside. These paths can be loaded dynamically using the `python-dotenv` package:

```python
import os
from dotenv import load_dotenv

# Load variables from the local .env file
load_dotenv()

# Safely fetch environment-specific paths
output_dir = os.getenv("OUTPUT_DIR")

```

:::{admonition} Best Practice: Securing .env files
:class: tip
The `.env` file must **never** be committed to version control, as it may contain sensitive paths or API keys. It should be explicitly added to the `.gitignore` file. Instead, an `.env.example` file should be committed, providing a blank template so collaborators know which variables must be defined on their respective systems.
:::

As complexity grows, the advanced case requires splitting these concerns even further. Logic is divided into executable routines (`scripts/`) and reusable modules (`src/`). Data is divided into discrete stages (`raw/`, `interim/`, `final/`) to trace lineage and document processing steps:

```bash
my_data_science_project/
│
├── data/              # Data stages
│   ├── raw/           # Original, immutable data dumps
│   ├── interim/       # Intermediary data from filtering/cleaning
│   └── final/         # Cleaned, tidy data used for analysis
│
├── src/               # Reusable logic: The core Python package
├── scripts/           # Executable logic: Batch execution scripts
│
├── config/            # Parameters
├── .env               # Environment state
└── results/           # Output deliverables
.
.


```

Finally, to make the project entirely self-describing, essential metadata and documentation are added to the root structure:

```bash
my_data_science_project/
│
├── data/              # Data stages
├── src/               # Reusable logic
├── scripts/           # Executable logic
├── results/           # Outputs
├── config/            # Parameters
│
├── docs/              # Documentation source files (e.g., Sphinx, MkDocs)
├── pyproject.toml     # Project metadata and dependencies (SSOT)
├── README.md          # Project overview and instructions
├── LICENSE            # License governing usage
├── .env.example       # Template for the .env file (committed to version control)
└── .gitignore         # Files and directories to ignore in Git


```

{% endif %}

### Quality and Control

{% if page %}
Once the core concerns are separated, an extensive structure integrates dedicated components for quality assurance and automation. Testing and benchmarking are critical for ensuring that the logic performs accurately and efficiently over time.



Furthermore, modern scientific computing relies heavily on Continuous Integration and Continuous Deployment (CI/CD). By including configuration files for platforms like GitHub or GitLab, the execution of tests, benchmarks, and documentation builds can be fully automated whenever changes are made to the repository.

```bash
my_data_science_project/
│
├── tests/                    # Quality Control: Automated unit and integration tests
│   ├── requirements.txt      # Dependencies specifically for testing (e.g., pytest)
│   └── test_cleaning.py      # Test suites corresponding to src modules
│
├── benchmark/                # Quality Control: Performance and scaling tests
│   └── run_benchmarks.py     # Scripts to track execution time and resource usage
│
├── .github/                  # Automation: GitHub-specific configurations
│   └── workflows/            # GitHub Actions CI/CD pipelines (YAML)
│
├── .gitlab-ci.yml            # Automation: GitLab CI/CD pipeline configuration
.
.

```

* **Note on CI/CD:** A project typically utilizes either `.github/workflows/` (if hosted on GitHub) or `.gitlab-ci.yml` (if hosted on GitLab), but rarely both simultaneously. They are included together here simply for illustrative purposes.

{% endif %}

{% if slide %}

::::{grid} 1 1 2 2
:gutter: 3

:::{grid-item}

```bash
my_data_science_project/
│
├── tests/             # Automated unit tests
├── benchmark/         # Performance tracking
│
├── .github/
│   └── workflows/     # GitHub CI/CD pipelines
│
├── .gitlab-ci.yml     # GitLab CI/CD pipeline
.
.

```

:::

:::{grid-item}
**Key Takeaways:**

* **Automated Assurance:** Code correctness and computational efficiency are systematically verified through dedicated `tests/` and `benchmark/` suites.
* **Continuous Integration (CI):** Automated pipelines (`.github/workflows/` or `.gitlab-ci.yml`) execute tests immediately whenever the codebase is modified.
* **Reliability:** Bugs and performance regressions are caught prior to publication, ensuring that analytical results remain stable and reproducible.
:::
::::

{% endif %}

