{% if build == "slides" %}
## Basic Git Workflow
{% else %}
## The Basic Git Workflow
{% endif %}

{% if slide %}
### Typical Development Cycle

```text
┌─────────────┐
│   Remote    │
│ Repository  │
└──────┬──────┘
       │ git clone / git pull
       ▼
┌─────────────┐
│    Local    │     git add
│ Repository  │ ◄──────────  Working Directory
└──────┬──────┘
       │ git commit
       │
       ▼ git push
┌─────────────┐
│   Remote    │
│ Repository  │
└─────────────┘
```

{% else %}
The basic Git workflow involves moving changes through different stages, from your working directory to the remote repository where others can access them.

### The Three States of Git

Git has three main states for your files:

1. **Working Directory**: Your actual project files where you make changes
2. **Staging Area (Index)**: A preparation area where you select which changes to include in the next commit
3. **Repository**: The committed history stored in the `.git` directory

This three-stage model gives you fine-grained control over what gets recorded in your project history.
{% endif %}

{% if slide %}
### Essential Commands

::::{tab-set}
:::{tab-item} Setup & Clone
```bash
# Configure identity
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Get a repository
git clone <url>
```
:::

:::{tab-item} Daily Work
```bash
# Check status
git status

# Stage changes
git add <file>
git add .

# Commit changes
git commit -m "Descriptive message"
```
:::

:::{tab-item} Sync with Remote
```bash
# Get latest changes
git pull

# Send your changes
git push
```
:::
::::

{% else %}
### Common Commands

**Initial setup** (one-time configuration):
```bash
# Set your identity
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Clone an existing repository
git clone https://github.com/username/repository.git
```

**Daily workflow**:
```bash
# Check what's changed
git status

# Stage specific files
git add analysis.py figures/plot.png

# Stage all changes
git add .

# Create a commit
git commit -m "Add correlation analysis and visualization"

# View commit history
git log --oneline
```

**Synchronizing with remotes**:
```bash
# Fetch and merge changes from remote
git pull

# Send your commits to remote
git push
```

### Working with Branches

Branches allow you to develop features in isolation:

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

{% if slide %}
:::{admonition} Best Practice
:class: tip
Write clear commit messages! Future you (and collaborators) will thank you.

**Good**: "Fix temperature unit conversion in processing script"  
**Bad**: "fixed bug"
:::
{% endif %}

{% if page %}
### Commit Message Best Practices

Good commit messages are essential for maintaining a usable project history[^1]:

[^1]: [xkcd.com/1296](https://xkcd.com/1296)

- **Be concise but descriptive**: Summarize what changed and why
- **Use imperative mood**: "Add feature" not "Added feature"
- **Focus on the what and why**, not the how (the code shows how)
- **Reference issues or tickets** when applicable

Example:
```bash
git commit -m "Add normalization step to preprocessing pipeline

Raw sensor data varied in scale across experiments. This commit
implements z-score normalization to ensure consistent input ranges
for downstream analysis. Fixes issue #42."
```
{% endif %}
