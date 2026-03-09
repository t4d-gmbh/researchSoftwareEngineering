### Apptainer Runtime Guide: `run`, `exec`, and `shell`

In Apptainer, the interaction between the host and the container filesystem depends on the command used. While all commands inherit the `%environment` block, their treatment of the `%runscript` and the working directory differs.

---

#### Command Overview

| Command | Primary Purpose | Executes `%runscript`? | Default Working Directory |
| --- | --- | --- | --- |
| **`run`** | Execute default app logic | **Yes** | Host `$PWD` (unless `cd` is in script) |
| **`exec`** | Run specific host tools | **No** | Host `$PWD` |
| **`shell`** | Interactive debugging | **No** | Host `$PWD` |

---

#### Behavior and `%runscript`

* **`run`**: Triggers the code defined in the `%runscript` section of the `.def` file. If the script contains `cd /app`, the application will execute from that directory.
* **`exec`**: Bypasses the `%runscript` entirely. It runs the command provided in the arguments (e.g., `apptainer exec image.sif python script.py`). It ignores any `cd` commands or logic defined in the image's entry point.
* **`shell`**: Opens a terminal (usually `bash`). Like `exec`, it ignores the `%runscript`.

---

#### Bind Mounts and Isolation

By default, Apptainer facilitates a "transparent" bridge. This means the container behaves as if it is a part of the host system.

##### Default Bindings

For all three commands (`run`, `exec`, `shell`), Apptainer automatically binds:

* **`$HOME`**: Your host home directory.
* **`$PWD`**: Your current host directory.
* **`/tmp`**: The host temporary directory.

##### Forcing Internal Paths

Because `$PWD` is bound by default, `apptainer exec` will always start in your host path. To override this and use an internal directory like `/app`, you must use the `--pwd` flag:

```bash
apptainer exec --pwd /app image.sif pwd

```

##### Total Isolation (`--contain`)

To prevent the host's `$HOME` and `$PWD` from being visible inside the container, use the `--contain` (or `-c`) flag. This ensures the environment is reproducible and unaffected by host files.

```bash
apptainer run --contain image.sif

```

---

#### Summary of Usage

* Use **`run`** when you want the container to act as a pre-configured executable (utilizing the internal `cd /app` logic).
* Use **`exec`** when you need to run a specific command or script that is not the container's primary purpose.
* Use **`shell`** to enter the container and manually inspect files in `/app` or `/opt/venv`.
