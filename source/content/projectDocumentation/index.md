# Project Documentation

{% if build == "slides" %}

```{toctree}
:maxdepth: 1

./introduction
./readme_structure
./installation_usage
./data_license
./extended_docs
```

{% else %}

Documentation is the bridge between your code and its users (including future you). Even minimal documentation makes a project usable and maintainable. This section establishes the baseline requirements for research software documentation.

```{include} ./introduction.md
```

```{include} ./readme_structure.md
```

```{include} ./installation_usage.md
```

```{include} ./data_license.md
```

```{include} ./extended_docs.md
```

{% endif %}

