{% if slide %}
<!-- BUILDING THE SLIDES -->
```{toctree}
:maxdepth: 3

./refactoring
./implementationApproaches
./pythonParallelism
./profilingDebugging
```

{% else %}
<!-- BUILDING THE PAGES -->


```{include} ./refactoring.md
```

# Primer on Parallelism

Parallelism lets you handle resource-intensive and data-heavy computations. This section covers the basics: what parallelism is, where it happens, and how to implement it (in Python).

```{include} ./implementationApproaches.md
```

```{include} ./pythonParallelism.md
```

```{include} ./profilingDebugging.md
```

{% endif %}
