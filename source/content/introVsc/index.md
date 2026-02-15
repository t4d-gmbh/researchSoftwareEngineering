{% if build == "slides" %}
# Introduction to Version Control

```{toctree}
:maxdepth: 1
:numbered:

./why-version-control
./git-basics
./basic-workflow
./further-resources
```

{% else %}
# Introduction to Version Control

Version control is a fundamental practice in research software engineering that tracks changes to files over time, enabling collaboration, reproducibility, and safer experimentation.

```{include} ./why-version-control.md
```

```{include} ./git-basics.md
```

```{include} ./basic-workflow.md
```

```{include} ./further-resources.md
```

{% endif %}
