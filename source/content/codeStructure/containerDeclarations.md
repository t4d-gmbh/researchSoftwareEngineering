## Container Blueprints

{% if slide %}

We consider container blueprints to be **environment definitions** which should remain strictly separated from operational logic.

::::{grid} 2
:gutter: 2

:::{grid-item-card} 📁 `containers/`
Houses declarative blueprints and manifests with payload (`Dockerfile`, `.def`), physically separating environment declaration from `src/` and `scripts/`.
:::

:::{grid-item-card} 🔒 `.env` & `.dockerignore`
Keeps local secrets out of version control and out of the compiled container image.
:::
::::

{% else %}

To maintain a clean repository root and strictly adhere to the Separation of Concerns, environment definitions (container blueprints) should be physically separated from operational logic (scripts) and core analytical code (the `src/` directory). 

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
{% endif %}
