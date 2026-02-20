### 2026 Update

{% if page %}
Almost 10 years after Wilson et al. (2017) an appendix is expedient:
{% endif %}

::::{grid} 1 1 2 2
:gutter: 2

:::{grid-item-card} 🤖 AI Usage
:class: sd-shadow-s

* **Disclosure:** State where AI (e.g., LLMs) was used for artifact (code, logic, text) *generation* and *modification*.
* **Verification:** Audit all AI-generated artifacts for errors.
* **Prompts:** Archive prompts used to generate critical artifacts, like code or analysis workflows.
:::

:::{grid-item-card} 📦 Software Environment
:class: sd-shadow-s

* **Isolation:** Work with dedicated virtual environments to enforce dependency control.
* **Pinned Dependencies:** Use lockfiles to ensure exact version parity.
* **Virtualization:** Containerize workflows to encapsulate the software environment.
:::

:::{grid-item-card} 🔌 Hardware Context
:class: sd-shadow-s

* **Specs:** Document GPU model, VRAM, and driver versions (e.g., CUDA).
* **Virtualization:** Use VMs to get a full documentation of the hardware stack used.
:::

:::{grid-item-card} 🧪 Verification & Consistency
:class: sd-shadow-s

* **Unit Tests:** Write tests for functions to ensure logic stays consistent.
* **Fixed Seeds:** Set and record seeds for all random number generators.
:::
::::
