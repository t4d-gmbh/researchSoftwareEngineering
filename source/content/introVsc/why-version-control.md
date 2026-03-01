## Why Use Version Control?


{% if slide %}
:::::{grid} 1 2 2 2
:gutter: 2

::::{grid-item-card} 🕰️ Track Changes
Work is never lost.
Changes, authors, and timestamps are systematically tracked.
::::

::::{grid-item-card} 🤝 Collaborate
Simultaneous work on the same codebase is enabled.
Contributions are merged systematically.
::::

::::{grid-item-card} 🔬 Reproducibility
Exact analysis states can be recreated.
Code versions are directly linked to published results.
::::

::::{grid-item-card} 🧪 Experiment Safely
New ideas can be tested without risk.
Previous working versions are easily restored.
::::
:::::

{% else %}
Version control systems track changes to files over time, creating a complete history of a project's evolution.
For research and scientific computing, version control provides several critical benefits:

**Preserving history**:  
Every change is recorded with information about the author, timestamp, and rationale.
This creates a complete, searchable audit trail of the project's development.

**Enabling collaboration**:  
Multiple researchers can work on the same codebase simultaneously.
Version control systems help merge contributions and identify conflicts that require manual resolution.

**Supporting reproducibility**:  
By tagging specific versions of code, the exact analysis environment used for a publication or result can be precisely recreated.
This is essential for scientific integrity and allows findings to be independently verified.

**Facilitating experimentation**:  
Version control makes it safe to test new approaches.
Experimental branches can be created without affecting the main codebase, and unsuccessful changes can be easily reverted.

**Disaster recovery**:  
Through the use of remote repositories, work is protected against local hardware failures or accidental deletions.

{% endif %}

{% if slide %}
:::{admonition} Key Insight
:class: tip
Version control transforms "final_version_FINAL_v3_really_final.py" into a systematic, searchable history.
:::
{% endif %}
