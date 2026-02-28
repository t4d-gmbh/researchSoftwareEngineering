{% if page %}
### Hardware Limitations and Operational Pitfalls

Researchers frequently encounter specific architectural limitations and operational pitfalls when adopting containers, especially when migrating from standard VM environments.

#### Hardware and State Limitations

**1. Hardware Architecture Binding**  
Like virtual environments, containers are bound to the CPU architecture upon which they are built.
A container image built on an ARM64 processor (e.g., Apple Silicon) will not natively execute on an x86_64 HPC cluster.
Cross-architecture execution requires instruction-set emulation (e.g., via QEMU), which incurs severe performance degradation.
Images must be explicitly cross-compiled or built natively on the target architecture.



**2. Hardware Pass-through (GPUs)**  
By default, containers cannot access physical hardware accelerators on the host system.
To utilize GPUs for machine learning, the container runtime must be explicitly instructed to map host-level driver interfaces into the container namespace.
This necessitates specific runtime flags (e.g., `docker run --gpus all` or `apptainer run --nv`) and requires the host system to possess specialized toolkit integrations (e.g., the NVIDIA Container Toolkit).

**3. State Persistence and Immutability**  
Container filesystems are ephemeral.
Any data written to the container's internal filesystem during execution is destroyed when the container terminates.
Persistent data generation (e.g., saving model weights or processed datasets) requires the explicit configuration of bind mounts (or volumes), which map a directory on the host filesystem directly into the container's isolated namespace.

#### Operational Pitfalls

##### Discrepancies in Filesystem Layers

**1. Persistent Image Bloat (The Deletion Fallacy)**  
Because intermediate container layers are strictly immutable, deleting a file in a subsequent layer does not reclaim disk space.
Instead, the union filesystem creates a "whiteout" marker in the upper layer, which hides the file from the unified view.
The actual file payload remains permanently archived in the lower read-only layer, increasing the total image transfer size.

*Mitigation*: Temporary files generated during installation (e.g., `apt-get` caches or source code tarballs) must be downloaded, utilized, and deleted within a single `RUN` directive (a single layer) to prevent storage bloat.

**2. Cryptographic and Credential Leaks**  
The deletion fallacy extends to security.
If SSH keys, API tokens, or proprietary datasets are copied into a container during a build step and subsequently removed in a later step, those secrets remain fully extractable.
Any user with access to the container registry can download the image, inspect the intermediate layer history, and extract the deleted credentials.

**3. Architectural Discrepancy in Apptainer**  
While Docker and Podman maintain this layered architecture at rest and during runtime, Apptainer treats layers differently.
Apptainer utilizes the layered OCI cache during the build phase but ultimately "squashes" the final image into a flat, monolithic Singularity Image Format (`.sif`) file.

This design choice explicitly abandons host-level deduplication to optimize for High-Performance Computing (HPC) environments.
Parallel filesystems (e.g., Lustre, GPFS) exhibit severe performance degradation when managing thousands of small overlay files.
By squashing the layers into a single `.sif` binary, Apptainer reduces I/O metadata operations, ensuring the container loads efficiently across thousands of distributed compute nodes.

##### Discrepancies in Isolation Policies

A major operational pitfall arises from the discrepancy in default isolation policies between Docker/Podman and Apptainer.

By default, Docker fully isolates the container filesystem from the host.
Conversely, to prioritize scientific workflows, **Apptainer implicitly mounts the user's home directory (`$HOME`), the current working directory (`$PWD`), and `/tmp` into the container at runtime.**
While this facilitates immediate access to research data, it breaches environmental isolation.
If a user has a localized Python package installed in `~/.local/lib/python` on the host, the Apptainer container will mount the host's home directory, detect those host packages, and potentially override the container's internal dependencies.
To enforce strict isolation identical to Docker, Apptainer must be explicitly invoked with the `--containall` flag.

{% endif %}
