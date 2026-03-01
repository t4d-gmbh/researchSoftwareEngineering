---
sd_hide_title: true
---
## Data & Licensing & Citation
{% if slide %}
::::::{grid}
:gutter: 2

:::::{grid-item-card}
:columns: 6
{% endif %}

### Data

{% if slide %}

**Keep data documentation concise:**

- **Location**: Where does the related data reside?
- **Access**: How is it accessed (and by whom)?
- **Ownership & License**: Who owns the data, and under what data-specific license is it provided?

*Note: All further details should be documented in `data/README.md`.*

:::::
:::::{grid-item-card}
:columns: 6

{% else %}

The data section in your main documentation should be strictly limited to the essentials: **where the data resides**, **how it can be accessed**, and **who owns it**. 

Crucially, if your repository provides data alongside code, you must specify the **Data License**. Software licenses (like MIT) do not properly cover datasets. Specify if the data is covered under a data-specific license like CC-BY-4.0 or ODbL.

Keeping this section concise ensures users immediately know if they can use the data and where to find it. **Any further details**—such as data provenance, processing pipelines, transformations, or structural descriptions—**must reside in a dedicated `README.md` file under the `data/` directory.**

:::{admonition} Restricted Data Sources
:class: important
When data cannot be made public (due to privacy concerns, institutional policies, or proprietary restrictions), you must clearly state:

- **Ownership**: The institution or entity that officially owns the data.
- **Access procedure**: How authorized researchers can request access (e.g., via an institutional data committee or ethics board approval).

Transparency about restrictions is better than silence. This allows others to assess whether pursuing access is worthwhile for their research.
:::

{% endif %}

### License

{% if slide %}

**The LICENSE file is your legal contract**

- A simple link to the `LICENSE` file is usually enough.
- **Crucial**: Explicitly list exceptions if parts of the repo use different licenses!

:::::
:::::{grid-item-card}

{% else %}

Without a license, default copyright laws apply—usually "all rights reserved," meaning no one can legally use your code. A proper `LICENSE` file acts as the legal contract between you and your users.

In most cases, **a simple reference and link to the `LICENSE` file in the root of your repository is enough.** You do not need to duplicate the license text or its standard conditions in your main documentation.

:::{admonition} Mixed Licensing
:class: important
If parts of the repository are differently licensed (for example, the core code is MIT, but you include third-party scripts under GPLv3, or your documentation is CC-BY), **this information must be explicitly stated here!** Provide a clear breakdown of which licenses apply to which directories or specific files.
:::
{% endif %}

### Citation

Provide a citation format directly in the README or link to a `CITATION.cff` file in your repository.

{% if slide %}

:::::
::::::

{% else %}

If you are using this repository for academic or published research, make it easy for others to credit your work:

**Example:**
```bibtex
@software{your_project_2026,
  author = {Your Name},
  title = {Your Project Name},
  year = {2026},
  publisher = {GitHub},
  url = {[https://github.com/your-username/your-repo](https://github.com/your-username/your-repo)}
}

{% endif %}
