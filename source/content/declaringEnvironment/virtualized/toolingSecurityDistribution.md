### Container Runtimes

{% if slide %}

**Implementation Variances**  
While based on the same underlying principles (Linux namespaces and cgroups), runtimes differ significantly in **security models** and **isolation policies**.

{% else %}
While the underlying principle (Linux namespaces and cgroups) remains consistent, the implementations of container runtimes vary significantly, primarily regarding security and isolation policies.

#### Docker and Podman

{% endif %}

{% if slide %}

::::{grid} 2
:gutter: 2

:::{grid-item-card} 🐳 Docker

* Historical standard for containerization.
* Relies on a high-privilege **root daemon**.
* Widely banned on HPC clusters due to the inherent security risks of root-level access.
:::

:::{grid-item-card} 🦭 Podman

* Open-source, **daemonless** alternative.
* Implements **rootless** containers via user namespaces (no root access required).
* Drop-in replacement utilizing identical command-line syntax.
:::

::::

{% else %}

**Docker** is the historical standard for containerization. It relies on a background daemon running with high privileges (`root`). While standard in web microservices, Docker is widely banned on High-Performance Computing (HPC) clusters due to the inherent security risks of granting users access to a root-level daemon.

**Podman** functions as an open-source, daemonless alternative to Docker. It implements rootless containers by utilizing user namespaces, allowing unprivileged users to build and execute containers without root access. Podman is a drop-in replacement for Docker, parsing the same `Dockerfile` manifests and utilizing identical command-line syntax.

#### Apptainer (formerly Singularity)

{% endif %}

{% if slide %}

::::::{grid}
:::::{grid-item-card} Apptainer
Industry Standard for HPC **diverging from Docker and Podman**:

::::{grid} 2
:gutter: 2

:::{grid-item-card} 📦 Image Format
Compiles the container into a **single, immutable flat file** (`.sif`). This allows it to be transferred and executed identically to a standard binary.
:::

:::{grid-item-card} 👤 Execution Privilege
Natively executes the payload as the **invoking user**. No privilege escalation occurs; processes inside the container are owned by the host user.
:::
::::

:::::
::::::

{% else %}

**Apptainer** is the industry standard container runtime for HPC and scientific computing environments. It diverges from Docker and Podman in several critical architectural aspects:

1. **Image Format**: Instead of managing a layered filesystem cache via a daemon, Apptainer compiles the entire container into a single, immutable flat file (Singularity Image Format, `.sif`). This allows containers to be transferred, archived, and executed identically to standard binary files.
2. **Execution Privilege**: Apptainer natively executes the container payload as the invoking user. No privilege escalation occurs. If `user_A` runs the container, the processes inside the container are owned by `user_A` on the host system.

#### Distribution via Container Registries

{% endif %}

{% if slide %}

**OCI-Compliant Registries**
Eliminates the need to distribute source code or installation instructions by providing a pre-compiled, verifiable system state.

:::{admonition} CI/CD Integration & Audit Trails
:class: note
Modern version control platforms (GitHub/GitLab) automatically build images upon repository commits. Tagging these images with the exact **Git SHA** provides a rigorous audit trail, linking the compiled environment directly to the source code that defined it.
:::

{% else %}

Container images are distributed via OCI-compliant (Open Container Initiative) registries. This infrastructure eliminates the need to distribute source code and installation instructions, replacing them with a pre-compiled, verifiable system state.

Standard public registries (e.g., Docker Hub) are utilized for base OS images. For research software, modern version control platforms (GitHub and GitLab) provide integrated Container Registries natively attached to repositories. This allows Continuous Integration (CI) pipelines to automatically build a new container image upon every repository commit, tagged with the exact Git SHA. This provides a rigorous audit trail, linking a specific compiled execution environment directly to the version-controlled source code that defined it.
{% endif %}
