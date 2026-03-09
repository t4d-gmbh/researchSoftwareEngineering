# Notes on Python

{% if slide %}
<!-- BUILDING THE SLIDES -->
```{toctree}
:maxdepth: 3

./noteOnPython
./slowPython.md
./theElephant.md
./parallelPython
./contextSwitching
./profilingDebugging
./implementationApproaches.md
./pythonParallelism
```

{% else %}
<!-- BUILDING THE PAGES -->


```{include} ./noteOnPython.md
```
```{include} ./slowPython.md
```
```{include} ./theElephant.md
```
```{include} ./parallelPython.md
```
```{include} ./contextSwitching.md
```
```{include} ./profilingDebugging.md
```

# Primer on Parallelism

Parallelism lets you handle resource-intensive and data-heavy computations. This section covers the basics: what parallelism is, where it happens, and how to implement it (in Python).

```{include} ./implementationApproaches.md
```

```{include} ./pythonParallelism.md
```

{% endif %}

