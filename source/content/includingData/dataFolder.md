---
sd_hide_title: true
---
## Linking Data to a Project

{% if slide %}

{.centered}
{.bigger}
**Linking data is a mandatory condition for a projects reproducibility.**

::::{grid}
:gutter: 6

:::{grid-item}
:columns: 6

{% else %}

While code defines the execution of a computational process, data constitutes the actual entity being processed.
Data must be linked directly to the project repository to allow for reproducibility and to facilitate the environment setup process.

{% endif %}

### The Data Directory

{% if slide %}

**Single entry point with strict structural separation:**
- **`data/raw/`**: Immutable, original data. (Read-only)
- **`data/interim/`**: Cleaned or transformed intermediate data.
- **`data/final/`**: Synthesized output data and canonical datasets ready for modeling.

:::
:::{grid-item}
:columns: 6

{% else %}

A single entry point for all datasets facilitates orientation and streamlines a project setup.
This entry point is typically the `data/` directory at the root of a repository.
To maintain pipeline integrity and prevent data corruption, this directory is subdivided into three distinct stages:

* **`data/raw/`**:  
  The original, immutable data.
  Files in this directory must not be edited and are to be treated as strictly read-only.
  Data cleaning or correction is performed via scripts that read from `raw/` and output to intermediate directories.
* **`data/interim/`**:  
  Intermediate data that has been transformed or cleaned but is not yet formatted for the final modeling or analysis phase.
* **`data/final/`**:  
  The canonical datasets utilized directly for modeling, reporting, or publication.  
  This folder can be further divided including, e.g., `data/final/results` a directory that contains only synthesized results needed for visualization and reporting.

{% endif %}

### A Data README.md

{% if slide %}

**The data documentation location:**
- A projects `README.md` and `data/README.md` must provide all necessary information regarding used data.
- Data dictionaries (definitions of columns/variables).
- Provenance (exact URLs, SQL queries).
- Summary of transformations (`raw/` -> `interim/` -> `final/`).

:::
::::

{% else %}

The root `README.md` needs to remain short and concise and thus is restricted to stating data location and ownership.
All further explanations and metadata should be placed in `data/README.md`.

This file should contain:
* Data dictionaries (definitions for each column or variable).
* Detailed provenance (exact URLs or database queries utilized to fetch the raw data).
* A technical summary of the scripts and transformations applied to move data from `raw/` to `interim/` and ultimately to `final/`.

{% endif %}

{% if slide %}
:::{admonition} Infrastructure & Performance Considerations
:class: note

**Impact of data storage on performance**
- **I/O Latency**: Network drives exhibit high latency when accessing numerous small files.
- **Data Locality**: Data is typically transferred to local scratch space (`/tmp`, `$SCRATCH`) on compute nodes prior to execution.
- **Configurability**: Codebases must handle variable paths based on the execution environment.

{.centered}
{.bigger}
**Simply copying all data to `data/` wont cut it!**

:::

{% else %}

### Infrastructure & Performance Considerations


The storage location and access methodology of data significantly impact computational performance, particularly within cloud and cluster infrastructures.

* **I/O Latency**: Reading numerous small files directly from a network drive on a cluster introduces high latency and can degrade overall network performance. 
* **Data Locality**: Transferring data to the compute node's local scratch space (e.g., `/tmp` or `$SCRATCH`) prior to script execution is often required to achieve optimal I/O efficiency.

The `data/` directory structure and the associated codebase must account for these infrastructure variations.
Simply copying all data into the `data/` folder is not a viable option for project with non-trivial datasets (i.e. > 100MB).

Scripts must be configurable (e.g., via environment variables in `.env` or `JSON` files in `config/`) to read from different data paths depending on the execution environment, such as a local workstation versus a high-performance compute node.

{% endif %}
