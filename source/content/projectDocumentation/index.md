# Project Documentation

{% if slide %}

```{toctree}
:maxdepth: 1

./introduction
./readme_structure
./title_description
./installation_usage
./data_license
./contrib_contact

```

{% else %}

Documentation is the bridge between your code and its users (including future you).
Even minimal documentation makes a project usable and maintainable.
This section establishes the baseline requirements for research software documentation.

```{include} ./introduction.md
```

```{include} ./readme_structure.md
```

```{include} ./title_description.md
```

```{include} ./installation_usage.md
```

```{include} ./data_license.md
```

```{include} ./contrib_contact.md
```

{% endif %}
