## Container Blueprints

{% if slide %}

Environment definitions should be physically isolated from operational logic.

::::{grid} 2
:gutter: 2

:::{grid-item-card} 📁 `containers/`
Houses declarative blueprints and manifests with payload (`Dockerfile`, `.def`), physically separating environment declaration from `src/` and `scripts/`.
:::

:::{grid-item-card} 🔒 `.env` & `.dockerignore`
Keeps local secrets out of version control and out of the compiled container image.
:::
::::

::::::{grid}
:gutter: 2

:::::{grid-item-card} Docker
{% else %}

To maintain a clean repository root and strictly adhere to the Separation of Concerns, infrastructure definitions (container blueprints) should be physically separated from operational logic (scripts) and core analytical code (the `src/` directory). 

Furthermore, local environment variables (such as those stored in a `.env` file) must remain strictly decoupled from the immutable container image. They must be excluded during the build phase and injected dynamically at runtime.

### Directory Structure



By utilizing a `containers/` directory, the codebase clearly delineates infrastructure from analytical logic:

```plaintext
.
├── containers/
│   ├── pipeline.Dockerfile
│   └── pipeline.def
├── scripts/
│   └── drafts/
│       └── hello.py
├── src/
│   └── mypackage/
├── .dockerignore      # Prevents secrets from being copied into the image
├── .env               # Local secrets (ignored by version control)
├── pyproject.toml
└── README.md

```

### Docker Implementation
{% endif %}

{% if slide %}

A **`.dockerignore` is mandatory** to prevent importing `.env` files (secret leakage).

1. 🛡️ **Secure Build Context**

   ```plaintext
   # .dockerignore
   .env
   .git/
   .venv/
   __pycache__/
   
   ```
2. ⚙️ **Build**
   
   Execute from the repository root, passing the manifest path:
   
   ```bash
   docker build -t my-img -f containers/pipeline.Dockerfile .
   ```

3. 🚀 **Execute**
   
   Execute from the repository root, injecting the `.env` file dynamically:
   
   ```bash
   docker run --rm --env-file .env my-img
   ```

:::
::::

:::::
:::::{grid-item-card} Apptainer

{% else %}

#### 1. Securing the Build (`.dockerignore`)

Because the `Dockerfile` utilizes the `COPY . /app` directive to bring the repository context into the image, a `.dockerignore` file must be present at the repository root to prevent the `.env` file from being permanently baked into the container.

```plaintext
# .dockerignore
.env
.git/
.venv/
__pycache__/

```

#### 2. `containers/pipeline.Dockerfile`

```dockerfile
# 1. Use an official, lightweight Python runtime
FROM python:3.13-slim

# 2. Install git so the build backend can determine the package version
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

# 3. Copy the pre-compiled uv binary from the official image
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# 4. Set the working directory inside the container
WORKDIR /app

# 5. Copy the project files into the container (respecting .dockerignore)
COPY . /app

# 6. Install the package and dependencies using uv
RUN uv pip install --system --no-cache --compile-bytecode .

# 7. Create a non-root user for security
RUN useradd -m appuser && chown -R appuser /app
USER appuser

# 8. Run the script when the container launches
CMD ["python", "scripts/drafts/hello.py"]

```

#### 3. Building and Executing via Docker

Execute the following commands from the **repository root**. The `--env-file` flag is utilized during the `run` command to inject the local variables directly into the container's isolated runtime.

```bash
# Build the image. 
docker build -t my-pipeline-image -f containers/pipeline.Dockerfile .

# Execute the containerized script, dynamically injecting the .env file
docker run --rm --env-file .env my-pipeline-image

```

### Apptainer Implementation
{% endif %}

{% if slide %}

**Explicit Copying over Ignore Files**
Apptainer lacks a native `.dockerignore` equivalent.
To prevent `.env` files from entering the image, directories must be copied explicitly.

1. 🛡️ **Secure Build Context**  

   ```apptainer
   %files
       # Explicitly avoid local .env files
       pyproject.toml /app/
       src /app/src
       scripts /app/scripts
   ```
2. ⚙️ **Build**  
   
   Execute from the repository root, passing the manifest path:
   
   ```bash
   apptainer build img.sif containers/pipeline.def
   
   ```
3. 🚀 **Execute**  
   Apptainer supports the `--env-file` flag (v1.1.0+) for symmetric runtime injection:
   ```bash
   apptainer run --env-file .env img.sif
   ```
:::::
::::::

{% else %}

Apptainer requires a structurally different blueprint (`.def` file). Because Apptainer does not natively utilize an ignore file (like `.dockerignore`) during the `%files` block, it is best practice to explicitly copy only the necessary directories rather than the entire repository root `.` to ensure the `.env` file is not accidentally archived into the image.

#### 1. `containers/pipeline.def`

```apptainer
Bootstrap: docker
From: python:3.13-slim

%files
    # Explicitly copy required directories to avoid capturing local .env files
    pyproject.toml /app/
    LICENSE /app/
    README.md /app/
    src /app/src
    scripts/ /app/scripts/

%post
    # 1. Install necessary system dependencies
    apt-get update && apt-get install -y git curl
    rm -rf /var/lib/apt/lists/*

    # 2. Install uv package manager
    curl -LsSf [https://astral.sh/uv/install.sh](https://astral.sh/uv/install.sh) | env UV_INSTALL_DIR="/bin" sh

    # 3. Install the project in the system environment utilizing uv
    cd /app
    uv pip install --system --no-cache --compile-bytecode .

%runscript
    # 4. Define the execution behavior
    cd /app
    exec python scripts/drafts/hello.py "$@"

```

#### 2. Building and Executing via Apptainer

Unlike Docker, Apptainer compiles the blueprint directly into a flat binary file (`.sif`). During execution, Apptainer also supports the `--env-file` flag (in versions 1.1.0+), allowing for symmetric runtime injection.

Execute the following commands from the **repository root**:

```bash
# Build the .sif binary image.
apptainer build containers/pipeline.sif containers/pipeline.def

# Execute the containerized script, explicitly passing the environment file.
apptainer run --env-file .env containers/pipeline.sif

```

{% endif %}
