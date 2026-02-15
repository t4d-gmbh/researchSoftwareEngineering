{% if build == "slides" %}
## Going Further with Git
{% else %}
## Further Resources and Topics
{% endif %}

{% if slide %}
### This Was Just the Beginning!

:::::{grid} 2
::::{grid-item}
**We covered**:
- Why version control matters
- Git's core concepts
- Basic workflow commands

::::

::::{grid-item}
**Much more to explore**:
- Collaboration workflows
- Conflict resolution
- Remote services (GitHub, GitLab)
- CI/CD automation
- Reproducibility practices
::::
:::::

{% else %}
This introduction covered the fundamental concepts of version control and Git, but there's much more to learn for effective use in academic and research settings.

### Topics We Haven't Covered

**Collaboration workflows**: How to work effectively with others using branches, pull requests, and code review processes.

**Handling conflicts**: When multiple people change the same files, Git helps identify conflicts that need manual resolution.

**Remote services**: GitHub, GitLab, and other platforms provide project management tools, issue tracking, and collaboration features beyond Git itself.

**Advanced Git operations**: Rebasing, cherry-picking, bisecting, and other powerful commands for managing complex histories.

**CI/CD automation**: Using automated workflows to test code, build documentation, or ensure reproducibility.

**Git for scientific reproducibility**: Strategies for versioning data (Git LFS), managing multi-repository projects (submodules), and linking code versions to published results.
{% endif %}

{% if slide %}
### Comprehensive Course Available

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
### Recommended Learning Path

For a comprehensive treatment of Git in academic contexts, we recommend the course **"Using Git in Academia"** maintained by T4D GmbH:

**🔗 [t4d-gmbh.github.io/using-git-in-academia](https://t4d-gmbh.github.io/using-git-in-academia/)**

This four-part course provides:

**Part 1: Working with Git**
- Detailed exploration of Git's building blocks
- Collaboration workflows including "feature branch" development
- Hands-on conflict resolution exercises
- Versioning strategies and semantic versioning

**Part 2: Git and its Remotes**
- Understanding GitHub vs. GitLab features
- Project organization and team management
- Contributing to open-source projects
- Advanced project management tools

**Part 3: CI/CD Workflows**
- Automated testing and deployment
- Creating reproducible computational environments
- Workflow triggers and integration with project management
- Security considerations for automation

**Part 4: Git and Science**
- Versioning large datasets with Git LFS
- Managing multi-repository analyses with submodules
- Bridging the gap between versioning and full reproducibility
- Automated analysis pipelines

The course includes practical exercises with real repositories, providing hands-on experience with all concepts.
{% endif %}

{% if slide %}
### Next Steps

1. **Practice**: Use Git for your next analysis or project
2. **Explore**: Try GitHub or GitLab for remote hosting
3. **Learn more**: Work through the full course when ready

:::{admonition} Remember
:class: tip
Version control is a skill that improves with practice. Start small and build up!
:::
{% endif %}

{% if page %}
### Getting Help

When you encounter issues:

- **Git documentation**: `git help <command>` or [git-scm.com/doc](https://git-scm.com/doc)
- **Interactive tutorials**: [learngitbranching.js.org](https://learngitbranching.js.org/)
- **Stack Overflow**: Most Git questions have already been answered
- **GitHub/GitLab documentation**: Platform-specific features and best practices

### Practical Advice

Start using Git for your projects now, even if you're working alone. The benefits of version control—history tracking, safe experimentation, and backup—apply to individual projects just as much as collaborative ones. As you become comfortable with basic operations, gradually explore more advanced features.

The key is consistent use. Like any tool, Git becomes intuitive with regular practice.
{% endif %}
