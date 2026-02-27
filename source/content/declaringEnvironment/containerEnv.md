# Containerized Environments and OS-Level Virtualization

Computational reproducibility frequently requires environmental control that extends beyond language-specific package managers. When software dependencies include complex system-level binaries, specific compiler toolchains, or specific versions of core system libraries (e.g., `glibc`), language-bound environments (such as Python virtual environments) are structurally insufficient.

To achieve system-level reproducibility, containerization is utilized. Containers provide a mechanism to package an application alongside its entire required user-space operating system.

## Principles of OS-Level Virtualization

Containers operate via OS-level virtualization. This paradigm isolates the user space—the segment of system memory where applications, libraries, and binaries execute—while sharing a single Operating System kernel with the host machine.

This differs fundamentally from Hardware Virtualization (Virtual Machines or VMs). A VM virtualizes the physical hardware, requiring a complete guest OS and a dedicated guest kernel to be booted, which introduces significant computational overhead. Conversely, containers execute directly on the host kernel. This architecture eliminates the overhead of hardware emulation and guest kernel management, resulting in execution speeds nearly identical to native host processes.

While OS-level virtualization provides near-instant instantiation and minimal overhead, the shared kernel architecture implies that complete reproducibility is not achieved. If a containerized application requires specific kernel modules or features (e.g., specific networking subsystems or eBPF capabilities) that are absent in the host's kernel, the execution will fail. For absolute hardware and kernel-level determinism, full Virtual Machines remain the necessary architecture.

## Extending Beyond Language Environments

As previously established, a Python `.venv` isolates only Python-domain packages. It inherently relies on the host operating system to provide underlying C libraries, network protocols, and GPU drivers.

Containers encompass the entire system user space. A container manifest declares the base operating system (e.g., Ubuntu 22.04, Alpine Linux) and all subsequent system-level modifications. This ensures that non-Python dependencies—such as `ffmpeg` for video processing, geospatial libraries like `GDAL`, or specific C++ compilers—are strictly versioned and isolated alongside the Python interpreter. The container isolates the execution context from the host's global variables, configuration files, and installed binaries.

## Declarative Manifests and Runtime Execution

A container is instantiated from an image, which is compiled from a declarative manifest (e.g., a `Dockerfile` or `Apptainer.def`). This manifest serves as the exact blueprint of the system state.

Beyond merely packaging software, container manifests define default execution behaviors. A manifest is not strictly a passive storage mechanism; it actively instructs the container runtime on how to execute the payload.

For example, utilizing the `ENTRYPOINT` directive in Docker or the `%runscript` block in Apptainer binds a specific command to the container's execution. If a container is built to run a specific data pipeline, the container itself functions as the executable binary:

```apptainer
%runscript
    exec python /opt/pipeline/main.py "$@"

```

## Image Layering and Union Filesystems

Container images are not monolithic data blobs; they are structurally organized via layered filesystems, typically utilizing a Union Filesystem implementation (e.g., OverlayFS). This architecture dictates how images are constructed, stored, and executed.

### Principles of Layered Construction

When a container runtime processes a declarative manifest (e.g., a `Dockerfile`), each sequential directive (such as `RUN`, `COPY`, or `ADD`) generates a discrete filesystem diff. This diff is committed as an immutable, read-only layer.

At runtime, the storage driver stacks these independent read-only layers into a single unified view. To permit application execution, a thin, ephemeral read-write layer is superimposed on top of the stack. Any modifications made by the application during runtime (e.g., writing log files) occur exclusively within this top ephemeral layer.

### System-Level Resource Optimization

This architecture provides two structural optimizations:

1. **Deduplication**: If multiple distinct container images rely on the same base image (e.g., `ubuntu:22.04`), the host system stores the base read-only layers exactly once. Multiple running containers concurrently reference the same underlying files on disk, drastically reducing storage consumption.
2. **Build Caching**: During the image build process, if a specific layer's directive and inputs remain unchanged, the runtime reuses the cached layer rather than recompiling it.

### Discrepancies and Operational Pitfalls

While layered filesystems optimize network transfer and local storage, they introduce critical operational constraints that frequently trap developers migrating from standard VM environments.

**1. Persistent Image Bloat (The Deletion Fallacy)**
Because intermediate layers are strictly immutable, deleting a file in a subsequent layer does not reclaim disk space. Instead, the union filesystem creates a "whiteout" marker in the upper layer, which hides the file from the unified view. The actual file payload remains permanently archived in the lower read-only layer, increasing the total image transfer size.

*Mitigation*: Temporary files generated during installation (e.g., `apt-get` caches or source code tarballs) must be downloaded, utilized, and deleted within a single `RUN` directive (a single layer) to prevent storage bloat.

**2. Cryptographic and Credential Leaks**
The deletion fallacy extends to security. If SSH keys, API tokens, or proprietary datasets are copied into a container during a build step and subsequently removed in a later step, those secrets remain fully extractable. Any user with access to the container registry can download the image, inspect the intermediate layer history, and extract the deleted credentials.

**3. Architectural Discrepancy in Apptainer**
While Docker and Podman maintain this layered architecture at rest and during runtime, Apptainer treats layers differently. Apptainer utilizes the layered OCI cache during the build phase but ultimately "squashes" the final image into a flat, monolithic Singularity Image Format (`.sif`) file.

This design choice explicitly abandons host-level deduplication to optimize for High-Performance Computing (HPC) environments. Parallel filesystems (e.g., Lustre, GPFS) exhibit severe performance degradation when managing thousands of small overlay files. By squashing the layers into a single `.sif` binary, Apptainer reduces I/O metadata operations, ensuring the container loads efficiently across thousands of distributed compute nodes.
Executing this container directly passes arguments to the internal pipeline, abstracting the internal Python environment entirely from the end-user.

## Tooling Implementations and Security Models

While the underlying principle (Linux namespaces and cgroups) remains consistent, the implementations of container runtimes vary significantly, primarily regarding security and isolation policies.

### Docker and Podman

**Docker** is the historical standard for containerization. It relies on a background daemon running with high privileges (`root`). While standard in web microservices, Docker is widely banned on High-Performance Computing (HPC) clusters due to the inherent security risks of granting users access to a root-level daemon.

**Podman** functions as an open-source, daemonless alternative to Docker. It implements rootless containers by utilizing user namespaces, allowing unprivileged users to build and execute containers without root access. Podman is a drop-in replacement for Docker, parsing the same `Dockerfile` manifests and utilizing identical command-line syntax.

### Apptainer (formerly Singularity)

**Apptainer** is the industry standard container runtime for HPC and scientific computing environments. It diverges from Docker and Podman in several critical architectural aspects:

1. **Image Format**: Instead of managing a layered filesystem cache via a daemon, Apptainer compiles the entire container into a single, immutable flat file (Singularity Image Format, `.sif`). This allows containers to be transferred, archived, and executed identically to standard binary files.
2. **Execution Privilege**: Apptainer natively executes the container payload as the invoking user. No privilege escalation occurs. If `user_A` runs the container, the processes inside the container are owned by `user_A` on the host system.

### Discrepancies in Isolation Policies (Operational Pitfalls)

A major operational pitfall arises from the discrepancy in default isolation policies between Docker/Podman and Apptainer.

By default, Docker fully isolates the container filesystem from the host. Conversely, to prioritize scientific workflows, **Apptainer implicitly mounts the user's home directory (`$HOME`), the current working directory (`$PWD`), and `/tmp` into the container at runtime.** While this facilitates immediate access to research data, it breaches environmental isolation. If a user has a localized Python package installed in `~/.local/lib/python` on the host, the Apptainer container will mount the host's home directory, detect those host packages, and potentially override the container's internal dependencies. To enforce strict isolation identical to Docker, Apptainer must be explicitly invoked with the `--containall` flag.

## Hardware and State Limitations

Researchers frequently encounter three specific architectural limitations when adopting containers:

**1. Hardware Architecture Binding**
Like virtual environments, containers are bound to the CPU architecture upon which they are built. A container image built on an ARM64 processor (e.g., Apple Silicon) will not natively execute on an x86_64 HPC cluster. Cross-architecture execution requires instruction-set emulation (e.g., via QEMU), which incurs severe performance degradation. Images must be explicitly cross-compiled or built natively on the target architecture.

**2. Hardware Pass-through (GPUs)**
By default, containers cannot access physical hardware accelerators on the host system. To utilize GPUs for machine learning, the container runtime must be explicitly instructed to map host-level driver interfaces into the container namespace. This necessitates specific runtime flags (e.g., `docker run --gpus all` or `apptainer run --nv`) and requires the host system to possess specialized toolkit integrations (e.g., the NVIDIA Container Toolkit).

**3. State Persistence and Immutability**
Container filesystems are ephemeral. Any data written to the container's internal filesystem during execution is destroyed when the container terminates. Persistent data generation (e.g., saving model weights or processed datasets) requires the explicit configuration of bind mounts (or volumes), which map a directory on the host filesystem directly into the container's isolated namespace.

## Distribution via Container Registries

Container images are distributed via OCI-compliant (Open Container Initiative) registries. This infrastructure eliminates the need to distribute source code and installation instructions, replacing them with a pre-compiled, verifiable system state.

Standard public registries (e.g., Docker Hub) are utilized for base OS images. For research software, modern version control platforms (GitHub and GitLab) provide integrated Container Registries natively attached to repositories. This allows Continuous Integration (CI) pipelines to automatically build a new container image upon every repository commit, tagged with the exact Git SHA. This provides a rigorous audit trail, linking a specific compiled execution environment directly to the version-controlled source code that defined it.

