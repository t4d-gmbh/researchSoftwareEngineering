{% if build == "slides" %}

## Beyond README: Extended Documentation

{% else %}

## Extended Documentation with Sphinx

{% endif %}

{% if slide %}

### When README Isn't Enough

For larger projects:

- **API documentation** from code
- **Tutorials** and guides
- **Searchable** documentation
- **Version-specific** docs

**Tool**: [Sphinx](https://www.sphinx-doc.org/)

{% endif %}

{% if page %}

A well-crafted `README.md` is sufficient for many research projects. However, as your codebase grows or your user base expands, you may need more comprehensive documentation infrastructure.

### Sphinx: Documentation from Code

[Sphinx](https://www.sphinx-doc.org/) is the standard tool for creating professional documentation websites for Python projects. You've likely encountered it:

- [NumPy](https://numpy.org/doc/stable/), [pandas](https://pandas.pydata.org/docs/), and most scientific Python libraries
- [Using Git in Academia](https://t4d-gmbh.github.io/using-git-in-academia/)
- This course material itself

Sphinx excels at:

- **Parsing Python code** to automatically extract docstrings and function signatures
- **Generating searchable HTML** from reStructuredText or Markdown
- **Integrating with CI/CD** to rebuild documentation automatically
- **Hosting on GitHub/GitLab Pages** for free

{% endif %}

{% if build == "slides" %}

### Getting Started

```bash
pip install sphinx
sphinx-quickstart
```

**Build documentation:**
```bash
make html
```

**Deploy** to GitHub Pages or GitLab Pages

{% endif %}

{% if page %}

### Setting Up Sphinx

Installation is straightforward:

```bash
pip install sphinx
```

Initialize a new documentation project:

```bash
sphinx-quickstart
```

This interactive command guides you through basic configuration. Once configured, build your documentation with:

```bash
make html
```

The output appears in `build/html/` as static HTML files ready for hosting.

:::{admonition} Exemplary Project
:class: tip
For a complete example of a research project with Sphinx documentation, see the course repository itself. The source files in `source/` generate both the course website and presentation slides using conditional rendering.
:::

### Themes and Customization

Sphinx offers numerous themes to customize your documentation's appearance. Popular choices include:

- **Read the Docs** theme (used by most Python projects)
- **Sphinx Book Theme** (used by this course)
- **PyData Theme** (used by scientific Python ecosystem)

Themes are installed via pip and activated in `conf.py`.

### Beyond Scope

Comprehensive Sphinx documentation (including automatic API generation, cross-referencing, and CI/CD integration) is beyond the scope of this course. For most research projects, a well-maintained README remains the priority. Sphinx becomes valuable when:

- You have a public API that external developers will use
- Your project has multiple interconnected modules requiring navigation
- You need version-specific documentation for different releases
- You're building a tool for a broader community beyond your research group

For detailed Sphinx tutorials, refer to the [official documentation](https://www.sphinx-doc.org/en/master/tutorial/index.html).

{% endif %}
