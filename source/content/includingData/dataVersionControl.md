---
sd_hide_title: true
---
## Versioning Data 2.0

{.centered}
{.bigger}
**Data Version Control (DVC)**

{% if slide %}

**Data tracking for machine learning pipelines**
- Designed specifically for dataset and model versioning.
- Git tracks `.dvc` metadata files.
- DVC manages data transfer to remote storage (e.g., AWS S3, GCS, SSH).
- Features a storage-agnostic architecture.

{% else %}

For projects involving complex data pipelines, large-scale datasets, or reliance on cloud storage infrastructure (e.g., AWS S3, Google Cloud Storage, or institutional SSH servers), **[Data Version Control](https://dvc.org/) (DVC)** is frequently implemented.

DVC functions similarly to Git but is optimized for large data artifacts and machine learning models.
Data is tracked using lightweight `.dvc` metadata files committed to the Git repository, while the actual data payloads are pushed to a specified remote storage backend.

{% endif %}

### Implementation: DVC & Git

{% if slide %}

::::{grid} 1 2 2 2
:gutter: 2

:::{grid-item-card} 1. Initialization & Remote Configuration:
```bash
dvc init
dvc remote add -d myremote s3://my-lab-bucket/data

```
:::

:::{grid-item-card} 2. Tracking & Committing Data:

```bash
dvc add data/raw/
git add data/raw.dvc data/.gitignore
git commit -m "Track raw data with DVC"

```
:::

{% else %}

The following steps outline the initialization and versioning process when utilizing DVC alongside Git.

#### Initialization and Configuration

```bash
# Execute within an initialized Git repository
dvc init

# Configure a remote storage backend (e.g., an AWS S3 bucket)
dvc remote add -d myremote s3://my-lab-bucket/project-data

```

#### Adding Data to DVC

Large files or directories are tracked using `dvc add` rather than `git add`.

```bash
# Track the raw data directory with DVC
dvc add data/raw/

# DVC generates a 'data/raw.dvc' metadata tracking file. 
# This metadata file is then committed to Git.
git add data/raw.dvc data/.gitignore
git commit -m "Track raw data with DVC"

```

{% endif %}
{% if slide %}

:::{grid-item-card} 3. Push Code & Data:

```bash
git push origin main
dvc push

```
:::
:::{grid-item-card} 4. Retrieve Data:

```bash
git clone [https://github.com/](https://github.com/)<owner>/<repo-name>.git
dvc pull  # Retrieves exact data versions linked to this commit

```

:::
::::

{% else %}

#### Pushing Data and Code

Code is pushed to the Git remote, while data is pushed to the DVC remote.

```bash
git push origin main
dvc push

```

#### Retrieving Data

When the Git repository is cloned, only the codebase and the `.dvc` tracking files are initially retrieved. To download the actual datasets linked to a specific Git commit, `dvc pull` must be executed:

```bash
git clone [https://github.com/](https://github.com/)<owner>/<repo-name>.git
cd repo-name

# Retrieves the exact data versions specified by the current Git commit
dvc pull

```

:::{admonition} Storage Agnosticism and Pipeline Tracking
:class: note

* **Storage Agnosticism**: DVC permits the use of various storage backends (e.g., institutional SSH servers, AWS S3) rather than relying exclusively on Git hosting platforms for large file storage.
* **Pipeline Tracking**: DVC possesses capabilities to track the computational steps that generate data, facilitating the reproduction of transformations from `data/raw/` to `data/final/`.
:::

{% endif %}
