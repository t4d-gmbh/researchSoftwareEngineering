---
sd_hide_title: true
---
## Further Resources and Topics

### Additional Topics

{% if slide %}
::::{grid} 2
:gutter: 2

:::{grid-item}
**Topics Covered**:

* Why version control matters
* Git's core concepts
* Basic workflow commands

:::

:::{grid-item}
**Further Exploration**:

* Collaboration workflows
* Conflict resolution
* Remote services (GitHub, GitLab)
* CI/CD automation
* Reproducibility practices
:::
::::

{% else %}
While the fundamental concepts of version control and Git have been covered, there is much more to learn for effective application in academic and research settings.


**[Collaboration workflows](https://t4d-gmbh.github.io/using-git-in-academia/content/working-with-git/source/content/principles/index.html)**: Effective collaboration utilizing branches, pull requests, and code review processes.

**[Handling conflicts](https://t4d-gmbh.github.io/using-git-in-academia/content/working-with-git/source/content/exercise/index.html)**: When the same files are modified concurrently, Git helps identify conflicts that require manual resolution.

**[Remote services](https://t4d-gmbh.github.io/using-git-in-academia/content/git-and-its-remotes/source/content/remote_services/index.html)**: Platforms such as GitHub and GitLab provide project management tools, issue tracking, and collaboration features beyond Git itself.

**[Advanced Git operations](https://t4d-gmbh.github.io/using-git-in-academia/content/working-with-git/source/content/useful_commands/index.html)**: Rebasing, cherry-picking, bisecting, and other powerful commands for managing complex histories.

**[CI/CD automation](https://t4d-gmbh.github.io/using-git-in-academia/content/ci-cd-workflows/source/content/why_automation/index.html)**: The utilization of automated workflows to test code, build documentation, or ensure reproducibility.

**[Git for scientific reproducibility](https://t4d-gmbh.github.io/using-git-in-academia/content/git-and-science/source/content/intro/index.html)**: Strategies for versioning data (Git LFS), managing multi-repository projects (submodules), and linking code versions to published results.
{% endif %}


### Recommended Learning Path

{% if slide %}

:::{admonition} Using Git in Academia
:class: note
**Full course**: [t4d-gmbh.github.io/using-git-in-academia](https://t4d-gmbh.github.io/using-git-in-academia/)

**Covers**:

1. Working with Git (commands, collaboration, versioning)
2. Git and Remote Services (GitHub/GitLab features)
3. CI/CD Workflows (automation for research)
4. Git and Science (reproducibility, data versioning)

**Format**: Hands-on exercises and practical examples
:::

{% else %}

For a comprehensive treatment of Git in academic contexts, the course **"Using Git in Academia"** maintained by T4D GmbH is highly recommended:

🔗 [**t4d-gmbh.github.io/using-git-in-academia**](https://t4d-gmbh.github.io/using-git-in-academia/)

This four-part course provides:

::::{grid} 1 2 2 2
:gutter: 2

:::{grid-item-card} Part 1: Working with Git

* Detailed exploration of Git's building blocks
* Collaboration workflows including "feature branch" development
* Hands-on conflict resolution exercises
* Versioning strategies and semantic versioning

:::
:::{grid-item-card} Part 2: Git and its Remotes

* Understanding GitHub vs. GitLab features
* Project organization and team management
* Contributing to open-source projects
* Advanced project management tools

:::
:::{grid-item-card} Part 3: CI/CD Workflows

* Automated testing and deployment
* Creating reproducible computational environments
* Workflow triggers and integration with project management
* Security considerations for automation

:::
:::{grid-item-card} Part 4: Git and Science

* Versioning large datasets with Git LFS
* Managing multi-repository analyses with submodules
* Bridging the gap between versioning and full reproducibility
* Automated analysis pipelines

:::
::::

The course includes practical exercises with real repositories, providing hands-on experience with all concepts.
{% endif %}

{% if slide %}

### Next Steps

1. **Practice**: Git can be utilized for upcoming analyses or projects.
2. **Explore**: Remote hosting platforms like GitHub or GitLab can be tested.
3. **Learn more**: The full course can be attended when appropriate.

:::{admonition} Remember
:class: tip
Version control is a skill that improves with practice. Starting small and gradually building up is recommended.
:::
{% endif %}

{% if page %}

### Getting Help

When issues are encountered:

* **Git documentation**: `git help <command>` or [git-scm.com/doc](https://git-scm.com/doc)
* **Interactive tutorials**: [learngitbranching.js.org](https://learngitbranching.js.org/)
* **Stack Overflow**: Most Git questions have already been answered.
* **GitHub/GitLab documentation**: Platform-specific features and best practices.

### Practical Advice

Immediate adoption of Git is recommended, even for solo work.
The benefits of version control (history tracking, safe experimentation, and backup) apply to individual projects just as much as collaborative ones.
As basic operations become familiar, more advanced features can be gradually explored.

:::{admonition} Playground Repository
:class: tip
A "Playground Repository" should be utilized to safely test the effects of different Git commands.
:::

The key is consistent use. Like any tool, Git becomes intuitive with regular practice.
{% endif %}
