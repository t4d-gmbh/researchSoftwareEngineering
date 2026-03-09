## Git Basics

{% if slide %}

### What is Git?

* **Distributed** version control system
* Tracks changes at the **file content** level
* Works **locally** (network not needed for most operations)
* Synchronizes with **remote** repositories

{% else %}
Git is a distributed version control system created by Linus Torvalds in 2005.
Unlike centralized systems, Git stores the complete project history locally on every machine.
This means offline work is possible, and operations like viewing history or creating branches are instantaneous.

Git tracks changes at the file content level, storing snapshots of the entire project at specific points in time.
These snapshots are called commits.
{% endif %}

{% if slide %}

### Key Building Blocks

::::{grid} 1 2 3 3
:gutter: 2

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

**Repository (repo)**:  
A directory tracked by Git, containing project files and the complete version history stored in a hidden `.git` folder.

**Commit**:  
A snapshot of a project at a specific moment. Each commit has:

* A unique identifier (SHA hash)
* Author information
* Timestamp
* A message describing the changes
* A reference to its parent commit(s)

**Branch**:  
A pointer to a specific commit, representing an independent line of development. Branches allow features or experiments to be worked on without affecting the main codebase. Git's default branch is typically called `main` (or formerly `master`).

**Tag**:  
A named reference to a specific commit, used to mark important milestones like releases. Unlike branches, tags do not move as new commits are added.

**Remote**:  
A version of the repository hosted elsewhere (e.g., GitHub, GitLab). Remotes enable collaboration and serve as backups.
{% endif %}


### The Commit Graph


{% if slide %}
::::{grid}
:gutter: 3

:::{grid-item}
:column: 6
:class: sd-m-auto
* Commits form a **directed acyclic graph** (DAG)
* Branches are just **labels** pointing to commits
* History shows **who** changed **what**, **when**, and **why**
:::
:::{grid-item}
:column: 6
:class: sd-m-auto
[![](https://mermaid.ink/img/pako:eNp1Ts1ugzAMfhXkM0KEUkJy7aS9w5SLR1xAXRLkJdM2xLsvVNs0tZpP9vfnb4UhWAIN4xwfGZfJ-CLPEJyb49-9iDjqwsCbqOqqNnCve2b0w1ScCWNi-uYnGi4hxRv0Lv1G7XD2_xYxHkoYebagIycqwRFnQz5h3YUG4kSODOx1LfJlL7tlz4L-KQT3Y-OQxgn0GV9e85UWi5EeZhwZ3S_K5C3xKSQfQQtxuIaAXuEddNuoqq2VOPSql6prMvmRRUpV4qhqKWXbKdE1civh8_q2rnp53L4AJm9zVw?type=png)](https://mermaid.live/edit#pako:eNp1Ts1ugzAMfhXkM0KEUkJy7aS9w5SLR1xAXRLkJdM2xLsvVNs0tZpP9vfnb4UhWAIN4xwfGZfJ-CLPEJyb49-9iDjqwsCbqOqqNnCve2b0w1ScCWNi-uYnGi4hxRv0Lv1G7XD2_xYxHkoYebagIycqwRFnQz5h3YUG4kSODOx1LfJlL7tlz4L-KQT3Y-OQxgn0GV9e85UWi5EeZhwZ3S_K5C3xKSQfQQtxuIaAXuEddNuoqq2VOPSql6prMvmRRUpV4qhqKWXbKdE1civh8_q2rnp53L4AJm9zVw)
:::
::::
{% else %}

Git organizes commits into a directed acyclic graph (DAG), where each commit points to its parent(s).
This structure allows Git to efficiently track the evolution of a project and identify where different development lines diverged or merged.

[![](https://mermaid.ink/img/pako:eNp1Ts1ugzAMfhXkM0KEUkJy7aS9w5SLR1xAXRLkJdM2xLsvVNs0tZpP9vfnb4UhWAIN4xwfGZfJ-CLPEJyb49-9iDjqwsCbqOqqNnCve2b0w1ScCWNi-uYnGi4hxRv0Lv1G7XD2_xYxHkoYebagIycqwRFnQz5h3YUG4kSODOx1LfJlL7tlz4L-KQT3Y-OQxgn0GV9e85UWi5EeZhwZ3S_K5C3xKSQfQQtxuIaAXuEddNuoqq2VOPSql6prMvmRRUpV4qhqKWXbKdE1civh8_q2rnp53L4AJm9zVw?type=png)](https://mermaid.live/edit#pako:eNp1Ts1ugzAMfhXkM0KEUkJy7aS9w5SLR1xAXRLkJdM2xLsvVNs0tZpP9vfnb4UhWAIN4xwfGZfJ-CLPEJyb49-9iDjqwsCbqOqqNnCve2b0w1ScCWNi-uYnGi4hxRv0Lv1G7XD2_xYxHkoYebagIycqwRFnQz5h3YUG4kSODOx1LfJlL7tlz4L-KQT3Y-OQxgn0GV9e85UWi5EeZhwZ3S_K5C3xKSQfQQtxuIaAXuEddNuoqq2VOPSql6prMvmRRUpV4qhqKWXbKdE1civh8_q2rnp53L4AJm9zVw)

In this example, commit B is the common ancestor of both branches.
The `main` branch has progressed through commits C and D, while `feature-branch` has progressed through commits E and F.
These branches can later be merged back together.
{% endif %}

{% if slide %}
:::{admonition} Remember
:class: note
Git tracks **changes**, not just files.
This makes it powerful for understanding project evolution.
:::
{% endif %}
