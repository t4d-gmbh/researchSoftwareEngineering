{% if build == "slides" %}

## Parallelism in Python

### The GIL Challenge

:::::{grid} 1 1 2 2
:gutter: 3

::::{grid-item-card} 🔒 Global Interpreter Lock
Only **one thread** executes Python bytecode at a time

**Threading**: Concurrency (task switching)  
**Multiprocessing**: True parallelism
::::

::::{grid-item-card} 🎯 Python's Role
**Orchestration layer** for compiled code

`numpy`, `pandas`, `scipy` → C/C++/Fortran  
Python releases GIL → multi-core execution
::::

:::::

### Performance Patterns

| Scenario | Approach | Speedup |
|----------|----------|---------|
| CPU-bound | `multiprocessing` | ~N cores |
| I/O-bound | `threading`/`asyncio` | Significant |
| Vectorized (NumPy) | **Already parallel** | None needed |

```{warning}
**Anti-pattern**: Iterating over NumPy arrays with Python loops
```

```{tip}
**Golden Rule**: Optimize sequential code (vectorization) before parallelizing
```

{% else %}

## Parallelism in Python: Capabilities and Constraints

Python presents a unique case in parallel computing. While it is the dominant language in data science and scientific computing, it has specific constraints that affect how parallelism can be achieved.

### The Global Interpreter Lock (GIL)

Python's most common implementation, [CPython](https://en.wikipedia.org/wiki/CPython), uses a mechanism called the [Global Interpreter Lock (GIL)](https://en.wikipedia.org/wiki/Global_interpreter_lock) to ensure thread safety. 

**Key implications of the GIL:**

- Multiple threads can exist within a Python process and run concurrently
- However, only **one thread can execute Python bytecode at any given instant**
- This prevents race conditions but limits parallel execution within a single process
- CPU-bound tasks see little to no speedup from multi-threading
- I/O-bound tasks can benefit significantly because the GIL is released during I/O waits

### Threading vs. Multi-Processing in Python

Python provides different libraries for different parallelization needs:

**For concurrency (task switching):**
- [`threading`](https://docs.python.org/3/library/threading.html): Standard interface for multi-threaded processes
- [`asyncio`](https://docs.python.org/3/library/asyncio.html): Cooperative multitasking for asynchronous I/O operations
- [`aiohttp`](https://github.com/aio-libs/aiohttp): Asynchronous HTTP client/server framework

**For true parallelism (simultaneous execution):**
- [`multiprocessing`](https://docs.python.org/3/library/multiprocessing.html): Bypass the GIL by spawning separate processes, each with its own Python interpreter

### Experimental Comparison: Threading vs. Multi-Processing

The following code demonstrates the performance difference between threading and multi-processing for a CPU-bound task:

```python
import time
import threading
import multiprocessing 
import numpy as np

def report_work(t_start, array, target_index:int=1):
    """
    Function repeatedly adding the moment of its execution to a binned array.
    """
    if t_start is None:
        t_start = time.perf_counter_ns()
    dt = array[1,0] - array[0, 0]
    while True:
        since_start = time.perf_counter_ns() - t_start
        i = int(since_start/dt)
        if i >= len(array):
            break
        array[i, target_index] += 1
    return array

def main(nbr_intervals:int=1000):
    """
    Run workload in a single process with a single thread
    """
    t_start = time.perf_counter_ns()
    array = np.zeros((nbr_intervals, 2), dtype=int)
    array[:, 0] = 50000 * np.arange(1, nbr_intervals + 1)
    report_work(t_start, array)
    return array

def multi_threading_main(nbr_intervals:int=1000, nbr_threads:int=4):
    """
    Run the work using multiple threads in a single process
    """
    t_start = time.perf_counter_ns()
    array = np.zeros((nbr_intervals, nbr_threads + 1), dtype=int)
    array[:, 0] = 50000 * np.arange(1, nbr_intervals + 1)
    threads = []
    for i in range(nbr_threads):
        threads.append(
            threading.Thread(target=report_work,
                             args=(t_start, array, i + 1))
        )
    for thread in threads:
        thread.start()
    for thread in threads:
        thread.join()
    return array

def multi_processed_main(nbr_intervals:int=1000, nbr_processes:int=4):
    """
    Run the work using multiple independent processes
    """
    array = np.zeros((nbr_intervals, 2), dtype=int)
    array[:, 0] = 50000 * np.arange(1, nbr_intervals + 1)
    multiprocessing.set_start_method('spawn')
    with multiprocessing.Pool(nbr_processes) as pool:
        arrays = pool.starmap(report_work,
                              [(None, np.copy(array), 1)
                               for _ in range(nbr_processes)])
    return arrays
```

**Key observations:**

1. **Multi-threaded performance**: Performs roughly the same total operations as single-process execution. This demonstrates the GIL in action—only one thread executes at a time for CPU-bound work.

2. **Multi-process performance**: Performs approximately 4x the operations (with 4 processes), showing true parallel execution on different cores.

3. **Memory considerations**: Multi-threaded version shares the same `array` object. Multi-process version requires each process to receive its own copy since processes cannot directly share memory.

### Python's Dual Nature: Orchestration vs. Execution

This raises an important question: **Why is Python the dominant language for computationally intensive data science if it's "slow"?**

**The answer: Python is not doing the heavy computation.**

Python excels as an **orchestration layer** for high-performance compiled code. Key libraries are essentially wrappers:

- `numpy` and `pandas`: Interfaces to optimized C/C++ code
- `scipy`: Fortran and C implementations
- `scikit-learn`, `pytorch`, `tensorflow`: Optimized C++/CUDA kernels

When you call `np.dot()`, you're not running Python code for the computation. Instead:

1. Python passes control to compiled C code (NumPy/BLAS)
2. Python releases the GIL
3. The C library spawns multiple threads and saturates all available cores
4. Computation completes, control returns to Python
5. Python re-acquires the GIL

**Demonstration:**

```python
import numpy as np

size = 4000
arr1 = np.random.rand(size, size)
arr2 = np.random.rand(size, size)

for _ in range(100):
    np.dot(arr1, arr2)  # Single Python call, multi-core execution
```

Monitoring with `htop` or `btop` reveals all CPU cores at 100% utilization, despite running a single Python process.

### The Cost of Context Switching: Data Marshaling

Using Python as a facade for compiled code introduces a cost: **data marshaling**—converting between Python objects and C-compatible data structures.

**Benchmark demonstration:**

```python
import numpy as np
import time

def timeit(func, iterations=100, *args, **kwargs):
    start_time = time.perf_counter()
    for _ in range(iterations):
        func(*args, **kwargs)
    end_time = time.perf_counter()
    print(f"{iterations} calls: {round(end_time - start_time, 3)}s")

def numpy_sum(np_array):
    return np.sum(np_array)

def python_sum(collection):
    return sum(collection)

def python_loop(collection):
    result = 0
    for num in collection:
        result += num
    return result

# Create test data
np_array = np.random.rand(1000000)
py_list = np_array.tolist()

print("NumPy array:")
timeit(numpy_sum, 100, np_array)        # ~0.04s - pure C loop
timeit(python_sum, 100, np_array)       # ~6.1s - Python iteration
timeit(python_loop, 100, np_array)      # ~6.9s - marshaling overhead!

print("Python list:")
timeit(python_sum, 100, py_list)        # ~0.75s - Python built-in
timeit(python_loop, 100, py_list)       # ~2.1s - pure Python loop
```

**Key findings:**

1. **NumPy sum is 100x faster**: The loop runs entirely in C with minimal Python interaction
2. **Worst case: Python loop over NumPy array**: 100x slower than pure NumPy, 3x slower than Python list loop
3. **Marshaling penalty**: Each array element access converts from C type to Python object, creating massive overhead

```{warning}
**Anti-pattern**: Iterating over NumPy arrays with Python loops defeats the purpose of using NumPy. Always use vectorized operations when possible.
```

### Practical Guidelines for Python Parallelism

1. **For CPU-bound tasks**: Use `multiprocessing` to bypass the GIL

2. **For I/O-bound tasks**: Use `threading` or `asyncio` to overlap wait times

3. **Leverage vectorization**: Use NumPy/Pandas operations instead of Python loops

4. **Don't parallelize already-parallel code**: Libraries like NumPy already use all cores; adding multiprocessing creates contention

5. **Profile first**: Use profiling tools to identify actual bottlenecks before parallelizing

6. **Consider established frameworks**: For complex parallel workflows, use specialized libraries:
   - [dask](https://docs.dask.org/): Parallel computing with task scheduling
   - [joblib](https://joblib.readthedocs.io/): Simple parallelization and caching
   - [ray](https://www.ray.io/): Distributed computing framework
   - [pyspark](https://spark.apache.org/docs/latest/api/python/): Big data processing

### When to Avoid Parallelization in Python

- When the task is already vectorized (NumPy, Pandas operations)
- When marshaling overhead exceeds computation time
- For tightly coupled problems requiring frequent synchronization
- When the task completes quickly enough sequentially

```{tip}
**Golden Rule**: Make your sequential code as efficient as possible (using vectorization, compiled libraries) before attempting parallelization. Often, proper use of NumPy eliminates the need for manual parallel coding.
```

{% endif %}
