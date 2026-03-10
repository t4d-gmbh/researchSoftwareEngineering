---
sd_hide_title: true
---
## Single Source of Truth (SSOT)

{% if slide %}

```{compound}
{.centered}
{.bigger}
**Single Source of Truth**

{.centered}
"Information must be defined in exactly one location. All subsequent usages must reference or derive from this primary definition."

```

:::::{grid} 2
::::{grid-item-card} Scope of Application

* **Data:** Raw inputs remain immutable; outputs are derived programmatically.
* **Metadata:** Versions and licenses reside in a single configuration.
* **Parameters:** Algorithmic settings are defined centrally.
::::
::::{grid-item-card} Integration with DRY
* **DRY** targets procedural **logic and behavior**.
* **SSOT** targets **data and state**.
* Eliminates conflicting project states.
* Guarantees computational reproducibility.
::::
:::::

:::{admonition} Core Rule
:class: warning margin
*"State must be referenced or derived, never duplicated."*
:::

---

### Example: Project Metadata

::::{grid} 2
:::{grid-item-card} Duplicated State ❌

```python
# pyproject.toml
version = "1.2.0"

# src/mypkgs/__init__.py
__version__ = "1.2.0"

# docs/conf.py
release = "1.2.0"

```

Version bumps require modifying three separate files. Desynchronization is highly probable.
:::
:::{grid-item-card} SSOT ✔

```toml
# pyproject.toml
[project]
version = "1.2.0"

```

```python
# src/mupkgs/__init__.py
from importlib.metadata import version
__version__ = version("my_package")

```

Defined once. Parsed dynamically. Impossible to desynchronize.
:::
::::

{% else %}

### The Idea

The Single Source of Truth (SSOT) principle dictates that every distinct piece of information within a system must be defined in exactly one location. Once defined, this information is only referred to or derived from that primary definition. While the DRY principle typically governs procedural logic and behavior, SSOT governs state, data, and metadata.

### Project-Wide Application

The necessity of a single source of truth extends across the entirety of a computational project:

* **Data Entities:** Raw data must be treated as immutable and stored in a definitive location. Intermediate or cleaned datasets must be derived programmatically from this source via reproducible scripts, rather than being manually copied or modified.
* **Metadata:** Project-level information, such as version numbers, author details, and license declarations, must be centralized. Defining a version number in a single standard configuration file (e.g., `pyproject.toml`) prevents conflicting version reports across environments and documentation.
* **Configuration Parameters:** Algorithmic thresholds, hyperparameters, and file paths must be defined in a dedicated configuration file and passed into the execution environment. Hardcoding these parameters throughout the source code creates hidden, fragmented states.

### Benefits and Integration with DRY

* **Elimination of Conflicting States:** When information is duplicated, synchronization is continuously required. SSOT eliminates the possibility of components operating on conflicting definitions.
* **Guaranteed Reproducibility:** A project's execution can only be reliably reproduced if its parameters and inputs are definitively known and uniquely identifiable.
* **Synergy with DRY:** SSOT and DRY are complementary architectural patterns. DRY ensures that the *method* for processing data is written once, while SSOT ensures that the *data* or *state* being processed is defined once.

### Example: Project Versioning

A pervasive violation of SSOT in software projects is the manual duplication of project metadata.

**The Duplicated State approach:**

```python
# pyproject.toml
version = "1.2.0"

# src/mypkgs/__init__.py
__version__ = "1.2.0"

# docs/conf.py
release = "1.2.0"

```

If a release is prepared, the version string must be manually updated in three discrete locations. If one update is overlooked, the project enters an inconsistent state, potentially causing deployment failures or documentation mismatches.

**The SSOT approach:**

The version is defined exclusively in the standardized project configuration file.

```toml
# pyproject.toml
[project]
name = "my_package"
version = "1.2.0"

```

All other components derive this information dynamically at runtime using standard library utilities.

```python
# src/mypkgs/__init__.py
from importlib.metadata import version

# The version is derived dynamically from the installed package metadata
__version__ = version("my_package")

```

This architectural pattern guarantees that a version bump requires only a single modification. The change propagates automatically, ensuring the entire project remains strictly synchronized and unambiguous.

{% endif %}
