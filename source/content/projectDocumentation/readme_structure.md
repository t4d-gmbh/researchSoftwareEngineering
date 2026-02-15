{% if build == "slides" %}

## The README.md File

{% else %}

## README Structure

{% endif %}

The `README.md` serves as your project's landing page. Its structure should be predictable and comprehensive.

{% if slide %}

### Essential Components

- **Project Title** and description
- **Installation** instructions
- **Usage** examples
- **Data** information
- **Methodology** summary
- **License** reference
- **Contributors** and contact

{% endif %}

{% if page %}

### Recommended README Structure

A robust `README.md` contains these essential sections:

**Project Title and Description**: Start with a clear project name and a concise "elevator pitch" explaining what the software does and why it exists.

**Installation Instructions**: Step-by-step setup guide that allows users to reproduce your environment. See the next section for best practices.

**Usage**: Code snippets or command-line examples demonstrating core functionality. Show the most common use cases first.

**Data**: Information on dataset origins, access protocols, and usage restrictions. This is crucial for reproducibility.

**Methodology**: A high-level summary of the scientific or technical methods employed. Detailed algorithms can go in separate documentation.

**License**: A reference to the project's licensing terms. Following the Single Source of Truth (SSOT) principle, link to the `LICENSE` file rather than duplicating its content.

**Contributors**: Acknowledgment of the development team and any funding sources.

**Contact Information**: Channels for reaching maintainers (email, issue tracker, or discussion forum).

:::{admonition} Consensus Standard
:class: tip
While no "perfect" README exists, consensus among developers (and training data for Large Language Models) has converged on this structure. Following it makes your project immediately familiar to new users.
:::

{% endif %}

{% if build == "slides" %}

### Template Approach

**Use a consistent structure across projects**

- Reduces cognitive load for users
- Easier to maintain
- Can be automated with templates

**Example**: [cookiecutter](https://cookiecutter.readthedocs.io/) templates

{% endif %}

{% if page %}

### Using Templates

Rather than writing a README from scratch for each project, consider using a template. This ensures consistency and completeness across your research outputs.

Tools like [cookiecutter](https://cookiecutter.readthedocs.io/) can generate project structures with pre-populated README templates. Many research groups maintain their own templates that include institution-specific information and comply with local data management policies.

{% endif %}
