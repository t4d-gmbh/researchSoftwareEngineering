{% if build == "slides" %}
## Why Version Control?
{% else %}
## Why Use Version Control?
{% endif %}

{% if slide %}
:::::{grid} 2
::::{grid-item-card} 🕰️ Track Changes
Never lose work  
See who changed what, when
::::

::::{grid-item-card} 🤝 Collaborate
Multiple people, same codebase  
Merge changes systematically
::::

::::{grid-item-card} 🔬 Reproducibility
Recreate exact analysis states  
Link code versions to results
::::

::::{grid-item-card} 🧪 Experiment Safely
Try new ideas without fear  
Easily return to working versions
::::
:::::

{% else %}
Version control systems track changes to files over time, creating a complete history of your project's evolution. For research and scientific computing, version control provides several critical benefits:

**Preserving history**: Every change is recorded with information about who made it, when, and why. This creates a complete audit trail of your project's development.

**Enabling collaboration**: Multiple researchers can work on the same codebase simultaneously. Version control systems help merge contributions and identify conflicts that need manual resolution.

**Supporting reproducibility**: By tagging specific versions of your code, you can recreate the exact analysis environment used for a publication or result. This is essential for scientific integrity and allows others to verify your findings.

**Facilitating experimentation**: Version control makes it safe to try new approaches. You can create experimental branches without affecting the main codebase, and easily revert changes that don't work out.

**Disaster recovery**: With remote backups, your work is protected against local hardware failures or accidental deletions.
{% endif %}

{% if slide %}
:::{admonition} Key Insight
:class: tip
Version control transforms "final_version_FINAL_v3_really_final.py" into a systematic, searchable history
:::
{% endif %}
