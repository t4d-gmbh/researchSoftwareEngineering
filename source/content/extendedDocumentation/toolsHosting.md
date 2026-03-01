## Documentation Tools and Hosting

{% if slide %}

**Static Site Generators**
- **Sphinx**: The Python ecosystem standard (reST/Markdown).
- **MkDocs**: Fast, Markdown-centric alternative.
- **Quarto**: Built for scientific and technical publishing.
- **MyST**: Markdown ecosystem fully compatible with Sphinx.

**Hosting Platforms**
- **Read the Docs (RTD)**: Automated versioning and building.
- **GitHub / GitLab Pages**: Direct CI/CD integration.

{% else %}

Extended documentation is typically managed utilizing Static Site Generators (SSGs), which compile plain text files (Markdown or reStructuredText) into searchable, interlinked HTML websites.



### Documentation Generators

Several standard tools exist for technical documentation generation:

* **Sphinx**: The standard documentation engine within the Python ecosystem. It is engineered to extract docstrings directly from Python code and supports both reStructuredText and Markdown (via extensions).
* **MkDocs**: A Markdown-centric static site generator. It is frequently preferred for non-code-heavy documentation due to its rapid build times and simplified configuration compared to Sphinx.
* **Quarto**: An open-source scientific and technical publishing system. It is designed to execute code (Python, R, Julia) directly within the documentation, making it suitable for reproducible research reports.
* **MyST (Markedly Structured Text)**: A superset of Markdown designed to integrate seamlessly with Sphinx, bridging the gap between standard Markdown syntax and the advanced referencing capabilities of reStructuredText.

### Hosting Options

Once HTML files are generated, they must be hosted. Standard platforms automate this process via Continuous Integration/Continuous Deployment (CI/CD) pipelines.

* **Read the Docs (RTD)**: A dedicated platform that automatically builds, versions, and hosts Sphinx and MkDocs documentation upon every repository push.
* **GitHub Pages**: A hosting service integrated directly into GitHub repositories. Documentation is compiled and deployed utilizing GitHub Actions.
* **GitLab Pages**: The equivalent service within the GitLab ecosystem, heavily utilized in institutional and academic environments via GitLab CI.

{% endif %}
