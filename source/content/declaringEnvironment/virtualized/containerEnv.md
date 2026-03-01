### Containerized Environments

{% if slide %}

**System-Level Reproducibility**

{% else %}
Computational reproducibility frequently requires environmental control that extends beyond language-specific package managers. When software dependencies include complex system-level binaries, specific compiler toolchains, or specific versions of core system libraries (e.g., `glibc`), language-bound environments (such as Python virtual environments) are structurally insufficient.

To achieve system-level reproducibility, containerization is utilized. Containers provide a mechanism to package an application alongside its entire required user-space operating system.

#### Principles of OS-Level Virtualization

{% endif %}

{% if slide %}

::::{grid}
:gutter: 2

:::{grid-item-card} User Space Isolation 
Segregates applications, libraries, and binaries from the host.
:::
:::{grid-item-card} Shared Kernel
Executes directly on the host Operating System kernel.
:::
:::{grid-item-card} Performance
Provides near-native execution speed.
:::
:::{grid-item-card} Limitation
Execution is strictly dependent on the host kernel possessing all required modules and features.
:::
::::

{% else %}

Containers operate via OS-level virtualization. This paradigm isolates the user space—the segment of system memory where applications, libraries, and binaries execute—while sharing a single Operating System kernel with the host machine.

Because containers execute directly on the host kernel, this architecture eliminates overhead, resulting in execution speeds nearly identical to native host processes.

While OS-level virtualization provides near-instant instantiation and minimal overhead, the shared kernel architecture implies a structural limitation. If a containerized application requires specific kernel modules or features (e.g., specific networking subsystems or eBPF capabilities[^1]) that are absent in the host's kernel, the execution will fail.

[^1]: eBPF (extended Berkeley Packet Filter) is a technology that allows programs to run sandboxed within the Linux kernel without changing kernel source code or loading kernel modules. It is widely used for networking, security, and observability tasks.


#### Extending Beyond Language Environments
{% endif %}

{% if slide %}

A container manifest strictly versions and isolates the Python interpreter alongside:

::::{grid}
:gutter: 2

:::{grid-item}
* Base **operating system** (e.g., Ubuntu, Alpine Linux)
* Core **system libraries**
:::
:::{grid-item}
* **Compiler toolchains**
* other **software tools needed**
:::
::::

*The execution context is entirely separated from the host's global variables, configuration files, and installed binaries.*

{% else %}
As previously established, a Python `.venv` isolates only Python-domain packages. It inherently relies on the host operating system to provide underlying C libraries, network protocols, and hardware drivers.

Containers encompass the entire system user space. A container manifest declares the base operating system (e.g., Ubuntu 22.04, Alpine Linux) and all subsequent system-level modifications. This ensures that non-Python dependencies—such as core system libraries, compiler toolchains, or standalone software tools—are strictly versioned and isolated alongside the Python interpreter. The container isolates the execution context from the host's global variables, configuration files, and installed binaries.
{% endif %}

#### Declarative Manifests and Runtime Execution

{% if slide %}

::::::{grid} 2
:gutter: 2

:::::{grid-item-card} 📜 The Blueprint
:columns: 4

A container is instantiated from an image, compiled from a declarative manifest (e.g., `Dockerfile` or `Apptainer.def`). This dictates the exact system state.
:::::

:::::{grid-item-card} ⚡ Active Execution
Manifests actively instruct the runtime on **how to execute the payload** using directives like `ENTRYPOINT` or `%runscript`.

::::{grid} 1 1 1 2
:gutter: 2

:::{grid-item-card} 🦭 Podman (Dockerfile)
Execution is bound using the `ENTRYPOINT` directive:

```dockerfile
ENTRYPOINT ["python", "/opt/pipeline/main.py"]

```

:::

:::{grid-item-card} 👽 Apptainer
Execution is bound using the `%runscript` block:

```apptainer
%runscript
    exec python /opt/pipeline/main.py "$@"

```

:::
::::

:::::
::::::


{% else %}
A container is instantiated from an image, which is compiled from a declarative manifest (e.g., a `Dockerfile` for Podman/Docker, or an `Apptainer.def` file). This manifest serves as the exact blueprint of the system state.

Beyond merely packaging software, container manifests define default execution behaviors. A manifest is not strictly a passive storage mechanism; it actively instructs the container runtime on how to execute the payload.

For example, execution commands can be structurally bound to the container so that it functions identically to an executable binary. This is achieved differently depending on the runtime utilized:

**Podman (via Dockerfile)**
The `ENTRYPOINT` directive is utilized to define the default executable:

```dockerfile
ENTRYPOINT ["python", "/opt/pipeline/main.py"]

```

**Apptainer**
The `%runscript` block is utilized to pass arguments directly to the internal pipeline:

```apptainer
%runscript
    exec python /opt/pipeline/main.py "$@"

```

By executing these containers directly, arguments are passed to the internal logic, abstracting the internal Python environment entirely from the end-user.
{% endif %}
