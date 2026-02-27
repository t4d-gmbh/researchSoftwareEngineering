## Building Documentation with Sphinx

{% if slide %}

**Sphinx Workflow**

```bash
# 1. Installation and initialization
pip install sphinx
sphinx-quickstart

# 2. Compilation
make html

```

**Key Capabilities:**

* Parses Python code for automatic API extraction.
* Generates searchable HTML.
* Customizable via ecosystem themes (e.g., Read the Docs theme).

{% else %}

[Sphinx](https://www.sphinx-doc.org/) functions as the standard tool for creating professional documentation websites for Python projects. It is utilized by major scientific libraries, including NumPy and pandas.

Sphinx is specifically engineered to:

* **Parse Python code** to automatically extract docstrings and function signatures.
* **Generate searchable HTML** from plain text source files.
* **Integrate with CI/CD** to rebuild documentation automatically upon code updates.

### Setting Up Sphinx

Installation is executed via the standard Python package manager:

```bash
pip install sphinx

```

A new documentation project is initialized utilizing the integrated configuration tool:

```bash
sphinx-quickstart

```

This interactive command generates the basic configuration files (e.g., `conf.py` and an `index.rst`). Once configured, the documentation is compiled with:

```bash
make html

```

The compiled output is deposited in the `build/html/` directory as static HTML files, ready for deployment to a hosting platform.

### Themes and Customization

The visual presentation of Sphinx documentation is modified through themes. Common selections within the scientific Python ecosystem include:

* **Read the Docs Theme**: The default visual standard for Python projects.
* **Sphinx Book Theme**: Designed for educational material and extended tutorials.
* **PyData Theme**: Utilized by the core scientific Python ecosystem.

Themes are installed via package managers and activated by modifying the `html_theme` variable within `conf.py`.

### Scope and Implementation

Comprehensive Sphinx configuration (including automatic API generation via `sphinx.ext.autodoc` and cross-referencing) requires significant setup. Sphinx implementation is recommended when:

* A public API is exposed for external utilization.
* The project contains multiple interconnected modules requiring structured navigation.
* Version-specific documentation is required for different software releases.

For isolated scripts, a well-maintained `README.md` is prioritized over full Sphinx integration. Detailed configuration instructions are maintained in the [official Sphinx documentation](https://www.sphinx-doc.org/en/master/tutorial/index.html).

{% endif %}
