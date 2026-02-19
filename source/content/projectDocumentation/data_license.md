{% if build == "slides" %}

## Data & Licensing

{% else %}

## Data Provenance and Licensing

{% endif %}

{% if slide %}

### Data Section

**Document the complete data pipeline:**

- **Origin**: Where did the data come from?
- **Processing**: What transformations were applied?
- **Restrictions**: What are the usage limitations?

### License Section

**The LICENSE file is your legal contract**

- Use standard licenses (MIT, GPLv3, Apache 2.0)
- Don't write your own, rather [choosealicense.com](https://choosealicense.com/)

{% endif %}

{% if page %}

### Documenting Data


The data section establishes the provenance of your datasets which is a fundamental requirement for reproducible research. It must declare the origin of the raw data: was it scraped from a website, generated through simulation, or downloaded from a public repository?

:::{admonition} Restricted Data Sources
:class: important
When raw data cannot be made public (due to privacy concerns, institutional policies, or proprietary restrictions) you still must document:

- **Access procedure**: How authorized researchers can request access (e.g., institutional data committee, ethics board approval)
- **Data characteristics**: General description without revealing sensitive details (e.g., "patient records from 2015-2020," "internal company logs")
- **Reproducibility limitations**: Explicitly state that full reproduction requires data access approval

Transparency about restrictions is better than silence. This allows others to assess whether pursuing access is worthwhile for their research.
:::

Crucially, you must document the **processing pipeline**. Research data rarely arrives in analysis-ready form. If you handled missing values, removed outliers, normalized features, or performed any other transformations, those decisions must be recorded. This ensures the scientific validity of your project and allows others to assess your methodology.

Finally, explicitly state any licensing restrictions regarding the data's redistribution or use. Many datasets come with terms of service that prohibit certain uses or require attribution.

:::{admonition} Example Data Documentation
:class: note
**Origin**: Raw legal text downloaded from [fedlex.admin.ch](https://www.fedlex.admin.ch/) on 2025-11-15 using the public XML API.

**Processing**: Extracted article text using wildcard namespace matching, filtered out authorial notes, split documents into individual articles. Processing script: `scripts/preprocess.py`.

**Restrictions**: Content is public domain (Swiss government works), but third-party annotations may have separate terms.
:::

### The LICENSE File

Without a license, default copyright laws apply—usually "all rights reserved," meaning no one can legally use your code. A proper `LICENSE` file acts as the legal contract between you and your users.

A standard license file includes:

**License Type**: The specific open-source license used (e.g., MIT, GPLv3, Apache 2.0).

**Copyright Notice**: The year and the name of the copyright holder.

**Permissions**: Rights granted to the user (e.g., commercial use, modification, distribution).

**Conditions**: Obligations the user must fulfill (e.g., including the original license, disclosing source code).

**Limitations**: Disclaimers of warranty and liability—essential for protecting the author.

:::{admonition} Don't Reinvent the Wheel
:class: warning
Avoid writing your own license. Use standard templates from [choosealicense.com](https://choosealicense.com/) and copy the full text into a `LICENSE` file. Custom licenses create legal uncertainty and discourage reuse.
:::

In your `README.md`, link to the `LICENSE` file rather than duplicating its content. This follows the SSOT principle and keeps your documentation maintainable.

{% endif %}
