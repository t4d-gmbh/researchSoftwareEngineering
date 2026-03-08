## Python's Elephant in the Room

::::{grid} 1 2 2 2
:gutter: 2

:::{grid-item}
:columns: 6
:class: sd-m-auto

{% if slide %}
**Execution Behavior:**
* Python scripts act as an **orchestration facade**; the actual computational workload is executed by compiled code.
* Libraries (`numpy`, `scipy`, `scikit-learn`, `pytorch`) provide Python interfaces to highly optimized `C`, `C++`, and `Fortran` implementations.
* Compiled extensions can explicitly release the GIL and utilize true multi-core parallelism.

{% else %}

Its prevalence is not due to methodologies being implemented in pure Python, but rather because Python provides a comprehensive portfolio of interfaces to highly effective implementations.

Libraries such as `pandas` (built upon `numpy`), `scipy`, `scikit-learn`, `pytorch`, and `tensorflow` act as abstraction layers, providing a Python interface to highly optimized `C`, `C++`, or `Fortran` libraries.

{% endif %}
:::

:::{grid-item}
:columns: 6
:class: sd-m-auto
```{image} ./../_static/pythonElephant.png
:alt: Python's Elephant
:width: 100%
```
:::
::::

{% if page %}


Carrying out a computational project in Python effectively means orchestrating the computation. The Python script serves as a facade, while the actual computational workload is executed by compiled code. 

{% endif %}
