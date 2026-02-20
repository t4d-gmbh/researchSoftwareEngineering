## Good Scientific Practice

{% if slide %}
According to Wilson et al.[^1] (condensed):
{% else %}

The question of what should, and what should not, be part of a project in computational science is determined by whatever is considered good scientific practice.

A detailed list of recommendations of what are good practices for a computational science project is provided by Wilson et al. (2017)[^1].
Provided here-below is a condensed representation:
{% endif %}

::::{grid} 1 1 2 2
:gutter: 2

:::{grid-item-card} 📂 Data Management
:class: sd-shadow-s

* **Preserve:** Save and back up original raw data in multiple locations.
* **Structure:** Create analysis-ready, tidy data with unique identifiers.
* **Traceability:** Document all processing steps and archive in a DOI-issuing repository.
:::

:::{grid-item-card} 💻 Software
:class: sd-shadow-s

* **Clean Code:** Use modular functions, meaningful names, and avoid duplication.
* **Dependencies:** Use/test external libraries and make requirements explicit.
* **Documentation:** Provide header comments, a test dataset, and a DOI for the code.
:::

:::{grid-item-card} 🤝 Collaboration & Org
:class: sd-shadow-s

* **Roadmap:** Maintain a project overview and shared to-do list.
* **Sync:** Define communication strategies and explicit licensing.
* **Citation:** Ensure the project is citable for others.
:::

:::{grid-item-card} 🔄 Tracking Changes
:class: sd-shadow-s

* **Version Control:** Use a VCS (like Git) for all human-created files.
* **Frequency:** Share small, frequent changes rather than large, rare ones.
* **Logs:** Maintain a `CHANGELOG` and mirror work to a remote server.
:::

:::{grid-item-card} 📝 Manuscripts
:class: sd-shadow-s

* **Format:** Use plain text formats (like Markdown) to allow for version control.
* **Tools:** Use platforms with rich formatting and automated reference management.
:::
::::

{.smaller}
[^1]: Wilson, G., et al. (2017). Good enough practices in scientific computing. *PLoS Comp Bio*. [https://doi.org/10.1371/journal.pcbi.1005510](https://doi.org/10.1371/journal.pcbi.1005510).
