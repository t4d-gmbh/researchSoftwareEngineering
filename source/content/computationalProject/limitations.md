### Delimination

{% if page %}
A well-planned project structure naturally encourages consolidating data, scripts, tests, and documentation into a single repository.
The primary advantage of this "monolithic" approach is simplicity: all elements of a project can be tracked, versioned, and shared as one cohesive unit.

However, consolidating absolutely everything into a single repository can become problematic as a project scales.
Issues may eventually be encountered regarding:

* **Distribution & Licensing:**  
  Different components often need to be shared under different restrictions.
  For instance, custom code might be open-source, but it may rely on a proprietary third-party dataset that explicitly prohibits public redistribution.
* **Complexity & Bloat:**  
  Massive repositories can quickly become unwieldy, obscuring the relationship between individual elements, slowing down Git operations, and making the commit history difficult to navigate.

To avoid a bloated monolithic repository while maintaining a unified workflow, multiple smaller, focused repositories can be linked together using `git submodules`.
This allows a main project to include an external element (such as a raw dataset or a shared utility library) by securely pointing to a specific commit in another Git repository.
{% endif %}

{% if slide %}
One repository keeps things simple, but can break down at scale:

:::::{grid} 2
::::{grid-item-card} <i class="fas fa-balance-scale"></i> Distribution & Licensing
Code might be open-source while a dataset it depends on prohibits redistribution.
::::

::::{grid-item-card} <i class="fas fa-weight-hanging"></i> Complexity & Bloat
Large repositories get slow, the history becomes noisy, and relationships between parts become unclear.
::::
:::::

**Solution:** Link focused repositories with `git submodules`.

{% endif %}

{% if page %}
Deciding exactly when to break a project into multiple repositories is ultimately somewhat arbitrary, but a separate repository is generally recommended if:
{% endif %}
{% if slide %}
**When to create a separate repository:**
{% endif %}

* An element (e.g., a curated dataset) is broadly useful in isolation for entirely different projects.
* An element (e.g., public-facing documentation or a web dashboard) needs to evolve or be deployed independently of the main analytical code.
* An element is subject to different ownership, access rights, or terms of use.

{% if page %}
**📝 A Note on Manuscripts**  
For papers, book chapters, or theses, the creation of a dedicated, separate repository is strongly recommended.
Resources from a primary analysis repository (such as auto-generated figures or tables) can still be easily referenced by including the analysis repository as a submodule.
However, a written manuscript and the underlying code analysis follow fundamentally different editing lifecycles; their separation keeps the writing history clean and prevents the codebase from being flooded with minor typo fixes.
{% endif %}

{% if slide %}
:::{admonition} Manuscripts
:class: tip
Papers, theses, and book chapters deserve their own repository. Include the analysis repo as a submodule to reference generated figures and tables.
:::
{% endif %}
