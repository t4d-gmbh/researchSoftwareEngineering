
## Basic Git Workflow

### Typical Development Cycle

{% if page %}
::::{grid} 1 2 2 2
:gutter: 2

:::{grid-item}
:class: sd-m-auto

First, code is fetched from a remote repository to a local machine utilizing `git clone` (for initial setup) or `git pull` (for updates).
Modifications are then made within the local working directory and staged via `git add`.
Subsequently, these modifications are permanently recorded to the local repository's history through `git commit`.
Finally, the updated local history is uploaded back to the remote repository utilizing `git push`.

:::
:::{grid-item}
:class: sd-m-auto

{% endif %}
```text
┌──────────┐
│  Remote  │
│Repository│
└────┬─────┘
     │ git clone / git pull
     ▼
┌──────────┐
│   Local  │  git add
│Repository│ ◄───────  Working Directory
└────┬─────┘
     │ git commit
     │
     ▼ git push
┌──────────┐
│  Remote  │
│Repository│
└──────────┘
```
{% if page %}

:::
::::

The basic Git workflow involves moving changes through different stages, from a local working directory to a remote repository where they can be accessed by others.

### The Three States of Git

Git operates using three main states for files:

1. **Working Directory**:  
   The actual project files where changes are made.
2. **Staging Area (Index)**:  
   A preparation area where specific changes are selected for inclusion in the next commit.
3. **Repository**:  
   The committed history safely stored in the `.git` directory.

This three-stage model provides fine-grained control over what is recorded in the project history.
{% endif %}

### Essential Commands

{% if slide %}
::::{tab-set}
:gutter: 2

:::{tab-item} Setup & Clone
{% else %}
**Initial setup** (one-time configuration):
{% endif %}

```bash
# Configure author identity
git config --global user.name "Author Name"
git config --global user.email "author@example.com"

{% if slide %}# Get a repository
git clone <url>
{% else %}# Clone an existing repository
git clone https://github.com/username/repository.git
{% endif %}
```

{% if slide %}
:::

:::{tab-item} Daily Work
{% else %}
**Daily workflow**:
{% endif %}

```bash
# Check repository status
git status

{% if slide %}# Stage changes
git add <file>{% else %}# Stage specific files
git add analysis.py figures/plot.png{% endif %}

# Stage all changes
git add .
{% if slide %}
# Commit changes
git commit -m "Descriptive message"
{% else %}
# Create a commit
git commit -m "Add correlation analysis and visualization"

# View commit history
git log --oneline
{% endif %}

```

{% if slide %}
:::

:::{tab-item} Sync with Remote
{% else %}
**Synchronizing with remotes**:
{% endif %}

```bash
{% if slide %}# Get latest changes{% else %}# Fetch and merge changes from remote{% endif %}
git pull

# Send changes to remote
git push

```

{% if slide %}
:::
::::
{% endif %}


{% if page %}
### Working with Branches

Branches allow features to be developed in isolation:

```bash
# Create and switch to a new branch
git checkout -b feature-analysis

# Make changes, add, commit...

# Switch back to main
git checkout main

# Merge feature branch
git merge feature-analysis

```

{% endif %}

:::{admonition} Best Practice
:class: tip {% if page %}margin{% endif %}
Clear commit messages are essential for reference and orientation.

:::{image} https://imgs.xkcd.com/comics/git_commit.png
:alt: Git Commit
:align: center
:width: {% if page %}100%{% else %}60%{% endif %}
:class: sd-m-auto

{.smaller}
*Source*: [xkcd.com/1296](https://xkcd.com/1296)
:::

{% if page %}
### Commit Message Best Practices

Good commit messages are essential for maintaining a usable project history[^1]([xkcd.com/1296](https://xkcd.com/1296)):

* **Be concise but descriptive**: Summaries should clarify what changed and why.
* **Use imperative mood**: Commands like "Add feature" are preferred over "Added feature".
* **Focus on the what and why**, not the how (the code itself demonstrates the how).
* **Reference issues or tickets** when applicable.

Example:

```bash
git commit -m "Add normalization step to preprocessing pipeline

Raw sensor data varied in scale across experiments. Implements z-score 
normalization to ensure consistent input ranges for downstream analysis. 
Fixes issue #42."

```

{% endif %}
