{% if page %}
### Image Layering and Union Filesystems

Container images are not monolithic data blobs; they are structurally organized via layered filesystems, typically utilizing a Union Filesystem implementation (e.g., OverlayFS). This architecture dictates how images are constructed, stored, and executed.



#### Principles of Layered Construction

When a container runtime processes a declarative manifest (e.g., a `Dockerfile`), each sequential directive (such as `RUN`, `COPY`, or `ADD`) generates a discrete filesystem diff.
This diff is committed as an immutable, read-only layer.

At runtime, the storage driver stacks these independent read-only layers into a single unified view.
To permit application execution, a thin, ephemeral read-write layer is superimposed on top of the stack.
Any modifications made by the application during runtime (e.g., writing log files) occur exclusively within this top ephemeral layer.

#### System-Level Resource Optimization

This architecture provides two structural optimizations:

1. **Deduplication**: If multiple distinct container images rely on the same base image (e.g., `ubuntu:22.04`), the host system stores the base read-only layers exactly once.
   Multiple running containers concurrently reference the same underlying files on disk, drastically reducing storage consumption.
2. **Build Caching**: During the image build process, if a specific layer's directive and inputs remain unchanged, the runtime reuses the cached layer rather than recompiling it.
{% endif %}
