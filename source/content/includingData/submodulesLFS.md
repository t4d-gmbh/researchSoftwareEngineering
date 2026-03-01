---
sd_hide_title: true
---
## Versioning Data 1.0

{.centered}
{.bigger}
**Git LFS & Submodules**

{% if slide %}

**Limitations of standard Git for data tracking**
- Committing large files increases repository size and encounters hosting limits.
- **Approach**: Combine Git LFS (for the data repository) with Git Submodules (to link data to the code repository).

::::{grid}
:gutter: 6

:::{grid-item}

{% else %}

Git is not designed to handle large datasets and binary files.
Committing large files, such as multi-gigabyte CSVs, increases repository size, slows down operations, and frequently results in errors due to file size limits imposed by hosting providers. 

**[Git Large File Storage](https://git-lfs.com/) (LFS)** in combination with **[Git Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)** are one way to mitigate this problem.
When combined, they allow to link versioned data into the primary codebase repository without increasing its footprint.


{% endif %}

### Git LFS (Large File Storage)

{% if slide %}

Git LFS replaces large files with text pointers.
```bash
# Initialize LFS in a dedicated data repository
git lfs install
git lfs track "*.csv"
git add .gitattributes ./dataset.csv
git commit -m "Add raw dataset"

```

:::
:::{grid-item}

{% else %}

Git LFS operates by replacing large files in the repository with small text pointer files, while the actual file contents are stored on a remote server.

**Workflow for creating a standalone data repository:**

```bash
# Initialize LFS in a dedicated data repository (e.g., project-data-repo)
git lfs install

# Configure LFS to track specific file extensions
git lfs track "*.csv"
git lfs track "*.h5"

# Commit and push changes (large files are routed to LFS storage, not Git history)
git add .gitattributes ./dataset.csv
git commit -m "Add raw dataset"
git push origin main

```

{% endif %}

### Git Submodules & "Lazy Loading"

{% if slide %}

Linking data repositories via Submodules

```bash
git submodule add https://github.com/<owner>/<data-repo>.git data/raw/
```

Lazy Loading Initialization:

```bash
# Data is pulled to the compute node only upon explicit initialization
git submodule update --init --recursive

```
:::
::::
{% else %}

Rather than storing LFS data directly within the primary code repository, the recommended approach is to isolate the data in an independent repository and link it to the code repository using a **Git Submodule**.

A submodule functions as a strict reference to a specific commit of an external repository.

**Linking the data to the project:**

```bash
# Execute within the primary code repository
git submodule add https://github.com/<owner>/<data-repo>.git data/raw/
git commit -m "Link raw data repository as a submodule"

```

:::{admonition} Lazy Loading Mechanism
:class: tip
When a repository is cloned that contains a submodule, the submodule directory (e.g., `data/raw/`) is uninitialized and empty by default.
Large datasets are not downloaded automatically.

This mechanism allows local development to proceed using minimal or synthetic data, bypassing unnecessary data transfers.
When the codebase is deployed to a compute node on a cluster, the required data is explicitly pulled:

```bash
# Execute on the compute node where the data is required
git submodule update --init --recursive

```

This strategy conserves network bandwidth and local disk space while ensuring that the compute environment retrieves the exact required version of the data.
:::

{% endif %}
