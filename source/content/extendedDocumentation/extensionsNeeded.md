---
sd_hide_title: true
---
## Extended Documentation Requirements

{% if slide %}

{.centered}
{.bigger}
**A single `README.md` is insufficient for:**

::::{grid}
:gutter: 2

:::{grid-item-card} Project Complexity:
- **Software packages** engineered for broad usability
- **Large repositories** containing a multitude of scripts
- **Complex environments** with specific dependency requirements
:::

:::{grid-item-card} Documentation Depth:
- **API documentation** extracted directly from code
- **Extensive tutorials** and step-by-step guides
- **Searchable** and version-specific documentation
- **Detailed methodology** and mathematical derivations
:::

::::

{% else %}

While a well-crafted `README.md` is sufficient for many isolated research scripts, more comprehensive documentation infrastructure is required as a codebase expands or is distributed for broader usage.

A single `README.md` file becomes insufficient under the following conditions:

* **Usability of Software Packages**: When a project is distributed as a reusable software package, users require extensive API references, usage examples, and troubleshooting guides that exceed the capacity of a single page.
* **Large Multi-Script Projects**: Repositories containing a multitude of interdependent scripts require orientation guides, architecture diagrams, and module-specific documentation to facilitate navigation.
* **Complex Environment Setup**: When dependency resolution requires specific hardware configurations, system-level libraries, or multi-container orchestrations, dedicated installation manuals are necessitated.
* **Version-Specific Documentation**: As software evolves, documentation must reflect specific releases (e.g., v1.0 vs. v2.0) to prevent configuration mismatches.
* **Searchability**: Extensive documentation requires indexing and full-text search capabilities to remain functional.
* **Methodological Depth**: Full mathematical derivations, theoretical backgrounds, and literature reviews must be isolated from the primary codebase entry point.

{% endif %}
