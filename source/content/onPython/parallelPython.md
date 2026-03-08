## Gotcha 1: Parallelization

::::{grid} 1 2 2 2
:gutter: 2

:::{grid-item}
:columns: 6
:class: sd-m-auto
{% if slide %}
**Execution Behavior of Compiled Extensions:**
* Python scripts act as an orchestration facade.
* Underlying libraries (e.g., NumPy) can save state, explicitly release the GIL, and delegate tasks to compiled C/Fortran code.
* The compiled code utilizes true multi-core parallelism.
{% else %}

When Python is utilized to orchestrate computational workloads, an additional layer of complexity is introduced, as the Python process often executes compiled code. 

This behavior can be observed by monitoring system resources while executing a standard matrix operation:

{% endif %}
:::
:::{grid-item}
:columns: 6
:class: sd-m-auto

```python
import numpy as np

size = 4000
arr1 = np.random.rand(size, size)
arr2 = np.random.rand(size, size)

for _ in range(100):
    np.dot(arr1, arr2)
```
:::
::::

::::{grid} 1 2 2 2
:gutter: 2

:::{grid-item}
:columns: 6
:class: sd-m-auto

```{image} ./../_static/numpyParallel.png
:alt: Python's Elephant
:width: 100%
```

:::

:::{grid-item}
:columns: 6
:class: sd-m-auto

{% if slide %}

```{compound}
{.centered}
⚠️ **The Oversubscription Risk:**  
Naively parallelizing a Python loop over operations that are already internally parallelized leads to severe thread contention and drastic performance degradation.*
```
{% else %}

Its prevalence is not due to methodologies being implemented in pure Python, but rather because Python provides a comprehensive portfolio of interfaces to highly effective implementations.

Libraries such as `pandas` (built upon `numpy`), `scipy`, `scikit-learn`, `pytorch`, and `tensorflow` act as abstraction layers, providing a Python interface to highly optimized `C`, `C++`, or `Fortran` libraries.

{% endif %}
:::
::::

{% if page %}

On a Unix-based system, resource monitors (such as `btop`) will reveal that a single Python process effectively utilizes all available CPU cores.

This occurs because libraries like NumPy utilize highly optimized C frameworks (such as BLAS) for algebraic operations. When the Python process invokes the `dot` product, the implementation saves its state, explicitly releases the Global Interpreter Lock (GIL), and delegates the task to the compiled C code. The C code then executes a multi-threaded, parallel computation utilizing all available hardware cores. Upon completion, the Python thread is restored, the GIL is reacquired, and standard execution resumes.

Attempting to explicitly parallelize the outer Python `for`-loop in this scenario is highly counterproductive. If parallelized, each individual Python task would trigger the underlying C library to spawn its own set of threads across all CPUs. This results in a scenario where every CPU runs multiple processes, each attempting to spawn threads across all CPUs simultaneously. This phenomenon, known as oversubscription or thread contention, leads to massive context-switching overhead and a drastic reduction in execution speed.

Consequently, writing efficient code in high-level orchestration languages (including Python and R) requires a fundamental understanding of the dependencies utilized and their specific internal execution models.
{% endif %}

