## Accessing Object Storage

{% if slide %}

**Cloud-native data management**
- **Object Storage (S3/Swift)**: Stores data as flat objects in "buckets" rather than nested folders.
- **DVC natively uses S3**: It pushes your heavy data directly to object storage.
- **Git LFS**: Uses GitHub/GitLab storage by default, but *can* be configured to use S3.

{% else %}

In modern research environments, massive datasets are rarely stored on traditional network drives.
Instead, they are hosted on **Object Storage** systems like AWS S3, Google Cloud Storage, or institutional OpenStack Swift clusters. 


Unlike traditional file systems, object storage does not have a real directory hierarchy.
Data is stored as discrete "objects" inside a flat "bucket" and accessed via HTTP APIs. 

#### Integration with Git LFS and DVC
You do not have to abandon version control just because your data is on S3:
* **DVC (Data Version Control)**:  
  DVC natively uses object storage.
  When you run `dvc push`, it uploads your datasets directly to your configured S3 or Swift bucket.
* **Git LFS**:  
  By default, Git LFS uploads your large files to the internal servers of your Git provider (like GitHub or GitLab).
  However, if you are running out of GitHub quota, Git LFS *can* be configured to use S3 as its backend by using custom transfer agents (like `lfs-s3`).

{% endif %}

### Documenting Access & Security

{% if slide %}

**Security Rule #1: Never commit credentials!**
- Document *what* environment variables are needed.
- Provide a `.env.example` file.
- Specify the **Endpoint URL** and **Bucket Name** in the `data/README.md`.

{% else %}

When your code pulls data directly from S3 or Swift, it requires authentication.
**Never hardcode your Access Keys or Secret Keys into your scripts.**
Instead, document the required connection parameters in your `data/README.md` and provide a `.env.example` file in the root of your repository so users know what credentials they need to supply.

**Example `.env.example`:**
```bash
# Object Storage Configuration
OS_ENDPOINT_URL=https://s3.your-institution.edu)
OS_BUCKET_NAME=my-research-data-bucket
OS_ACCESS_KEY_ID=your_access_key_here
OS_SECRET_ACCESS_KEY=your_secret_key_here

```

In your documentation, clearly state how a user can obtain these credentials (e.g., *"To run this pipeline, request an S3 access token from the institutional IT helpdesk and place it in your local `.env` file"*).

{% endif %}

### Access Patterns & Tooling

{% if slide %}

**How to fetch the data:**

* **CLI Tools**: Use e.g.the MinIO Client (`mc`) to quickly mirror S3 buckets to local scratch space.
* **Python Native**: Use `pandas` with `s3fs` / `fsspec` to stream directly into memory.
* **Consider your cluster limits**: Streaming saves disk space; downloading speeds up repeated reads.

{% else %}

Explicitly document *how* the data should be brought into the compute environment.
There are two primary access patterns for object storage, and the choice greatly affects performance on a cluster:

#### Bulk Downloading to Local Scratch

For deep learning or processes that read the same files multiple times, it is usually best to download the data to the compute node's `$SCRATCH` or `$TMPDIR` space before the Python script runs.

A commonly used tool for interacting with S3-compatible storage is the **MinIO Client (`mc`)**.
Document the exact commands users need to run to sync the data:

```bash
# ./data/README.md

# 1. Configure the connection (using your environment variables)
mc alias set my-s3 $OS_ENDPOINT_URL $OS_ACCESS_KEY_ID $OS_SECRET_ACCESS_KEY

# 2. Mirror the remote bucket to the compute node's fast local scratch space
mc mirror my-s3/my-research-data-bucket/raw_images/ /tmp/scratch/raw_images/

```

#### Streaming Directly into Memory

For processing large tabular datasets (like Parquet or CSV files) that only need to be read once, you can stream the data directly from object storage into Python using libraries like `pandas` with `s3fs` (or `fsspec`).
This bypasses the local hard drive entirely.

Provide a minimal code snippet in your documentation, e.g.:

```python
import pandas as pd
import os

# Pandas uses fsspec under the hood to stream directly from S3
storage_options = {
    "key": os.getenv("OS_ACCESS_KEY_ID"),
    "secret": os.getenv("OS_SECRET_ACCESS_KEY"),
    "client_kwargs": {"endpoint_url": os.getenv("OS_ENDPOINT_URL")}
}

# No local file is ever created; data goes straight to RAM
df = pd.read_parquet(
    "s3://my-research-data-bucket/interim/processed_records.parquet", 
    storage_options=storage_options
)
```

:::{admonition} Performance Tip
:class: important
When streaming thousands of tiny files directly from object storage during a training loop, the network overhead will bottleneck a GPU.
Therefore it is important to clarify if a pipeline expects the data to be pre-downloaded or if it streams on-the-fly.
:::

{% endif %}
