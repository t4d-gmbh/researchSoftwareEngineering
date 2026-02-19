{% if build == "slides" %}
## Git Basics
{% else %}
## Understanding Git: Core Concepts
{% endif %}

{% if slide %}
### What is Git?

- **Distributed** version control system
- Tracks changes at the **file content** level
- Works **locally** (no network needed for most operations)
- Synchronizes with **remote** repositories

{% else %}
Git is a distributed version control system created by Linus Torvalds in 2005. Unlike centralized systems, Git stores the complete project history locally on every user's machine. This means you can work offline, and operations like viewing history or creating branches are instantaneous.

Git tracks changes at the file content level, storing snapshots of your entire project at specific points in time. These snapshots are called commits.
{% endif %}

{% if slide %}
### Key Building Blocks

::::{grid} 3
:::{grid-item-card} Commits
📸 Snapshots of project state  
Unique identifier (hash)
:::

:::{grid-item-card} Branches
🌿 Parallel development lines  
Lightweight pointers to commits
:::

:::{grid-item-card} Tags
🏷️ Named milestones  
Mark important versions
:::
::::

{% else %}
### Core Concepts

**Repository (repo)**: A directory tracked by Git, containing your project files and the complete version history stored in a hidden `.git` folder.

**Commit**: A snapshot of your project at a specific moment. Each commit has:
- A unique identifier (SHA hash)
- Author information
- Timestamp
- A message describing the changes
- A reference to its parent commit(s)

**Branch**: A pointer to a specific commit, representing an independent line of development. Branches allow you to work on features or experiments without affecting the main codebase. Git's default branch is typically called `main` (or formerly `master`).

**Tag**: A named reference to a specific commit, used to mark important milestones like releases. Unlike branches, tags don't move as new commits are added.

**Remote**: A version of your repository hosted elsewhere (e.g., GitHub, GitLab). Remotes enable collaboration and serve as backups.
{% endif %}

{% if slide %}
### The Commit Graph

```text
A --- B --- C --- D  (main)
       \
        E --- F  (feature-branch)
```

- Commits form a **directed acyclic graph** (DAG)
- Branches are just **labels** pointing to commits
- History shows **who** changed **what**, **when**, and **why**

{% else %}
### How Git Stores History

Git organizes commits into a directed acyclic graph (DAG), where each commit points to its parent(s). This structure allows Git to efficiently track the evolution of your project and identify where different development lines diverged or merged.

```text
A --- B --- C --- D  (main branch)
       \
        E --- F  (feature-branch)
```

In this example, commit B is the common ancestor of both branches. The `main` branch has progressed through commits C and D, while `feature-branch` has commits E and F. These branches can later be merged back together.
{% endif %}

{% if slide %}
:::{admonition} Remember
:class: note
Git tracks **changes**, not just files. This makes it powerful for understanding project evolution.
:::
{% endif %}
