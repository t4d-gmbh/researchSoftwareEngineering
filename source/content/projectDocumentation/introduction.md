{% if build == "slides" %}

## Why Document?

{% else %}

## Minimal Documentation Requirements

{% endif %}

Good documentation doesn't require extensive effort. A well-structured minimal documentation already makes your project:

- **Usable** by others (and yourself in six months)
- **Citable** with clear authorship and licensing
- **Reproducible** with explicit installation steps

{% if slide %}

::::{grid} 1 2 2 2

:::{grid-item-card} For Users
**Installation** and usage instructions
:::

:::{grid-item-card} For Researchers
**Data provenance** and methodology
:::

:::{grid-item-card} For Collaborators
**Contribution** guidelines
:::

:::{grid-item-card} For Science
**Reproducibility** and transparency
:::

::::

{% endif %}

{% if page %}

The goal isn't perfection but clarity. Documentation serves multiple audiences:

- **End users** need to know how to install and run your software
- **Researchers** need to understand your methodology and data sources
- **Potential contributors** need to know how to modify and extend your work
- **Your future self** needs to remember why you made certain design decisions

The core of minimal documentation is a well-structured `README.md` file. Combined with proper licensing and version control (covered in the [Using Git in Academia](https://t4d-gmbh.github.io/using-git-in-academia/) course), this foundation ensures your research software can be understood and reused.

{% endif %}
