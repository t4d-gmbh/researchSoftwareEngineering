---
sd_hide_title: true
---
## Acknowledgments & Contributing & Contact

{% if slide %}

::::::{grid} 1 2 2 3
:gutter: 2

:::::{grid-item-card}

{% else %}

A well-structured repository doesn't just share code; it builds a community around it while giving proper credit to its creators and supporters.
{% endif %}

### Acknowledgments

{% if slide %}
Credit the authors, labs, and funding agencies.

:::::
:::::{grid-item-card}

{% else %}

In academic and research software, giving credit is essential.
Briefly acknowledge the main authors, the affiliated laboratories or institutions, and any funding agencies or grants that supported the work. 

**Example:**
> *This project was developed by the [Your Lab Name] at [Your University]. This work was supported by the [Funding Agency] under Grant No. [123456].*

{% endif %}

### Contributing

{% if slide %}

- State if contributions are welcome or not.
- Link directly to `CONTRIBUTING.md`.

:::::
:::::{grid-item-card}

{% else %}

Just as we moved advanced usage to the `docs/` folder, we do not clutter the README with instructions on how to run tests, format code, or submit Pull Requests.

Simply state that contributions are welcome and provide a direct link to your `CONTRIBUTING.md` file.

:::{admonition} Example Contribution Statement
:class: tip
We welcome contributions from the community! Whether you are fixing bugs, improving documentation, or proposing new features, please read our [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on our development workflow and code standards.
:::

{% endif %}

### Contact Information

{% if slide %}

Define clear channels, e.g.:
- Open an issue for usage related questions.
- For academic inquiries, please contact `me@email.world`.

:::::
::::::

{% else %}

Clearly define how users should get in touch with you, and set boundaries for different types of communication. This prevents your personal inbox from being flooded with basic troubleshooting questions.

* **For bugs, issues, and feature requests:** Direct users to the repository's Issue Tracker (e.g., "Please open a GitHub Issue"). This keeps problem-solving public and searchable for future users.
* **For academic inquiries, private collaboration, or security vulnerabilities:** Provide an official contact email address.

**Example:**
> For bug reports and feature requests, please [open an issue](https://github.com/<owner>/<repo-name>/issues) on GitHub.
> For academic collaborations or private inquiries, please contact `your.email@institution.edu`.

{% endif %}
