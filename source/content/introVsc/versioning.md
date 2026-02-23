## Versioning

{% if page %}
Various methods exist to document the state of a repository.
To improve both readability and functionality, the adoption of a consistent structure when describing its state is highly recommended.
A key element of this structure is often a version identifier.
{% endif %}

[Versioning](https://en.wikipedia.org/wiki/Software_versioning) provides a logical framework for labeling specific states of a repository.

{% if page %}
It offers a structured way to describe these states, though the exact method may vary depending on the versioning approach used.
Many different options exist, each with its own logic.

Choosing the most appropriate versioning approach can be somewhat subjective.
However, certain methods are more commonly adopted than others.
Here, one of the most widely adopted approaches is presented: [SemVer](https://semver.org).

In short,{% endif %} *SemVer* is a versioning system that utilizes a three-part number (`X.Y.Z`) to track changes to a software project or dataset.

```{math}
\underset{\overbrace{\text{Major}}}{\bf{X}}.\overset{\underbrace{\text{Minor}}}{\bf{Y}}.\underset{\overbrace{\text{Patch}}}{\bf{Z}}

```

::::{grid}
:::{grid-item-card} Major
Incremented when **breaking changes** or **significant updates** are made that are not backwards-compatible.
:::
:::{grid-item-card} Minor
Incremented when **new features** or **functionality** are added in a backwards-compatible manner.
:::
:::{grid-item-card} Patch
Incremented when backwards-compatible **bug fixes** or **minor updates** are introduced.
:::
::::

Defining a new version of a repository is straightforward when utilizing `git tag`:

```bash
git tag -a X.Y.Z -m 'short description of state'

```
