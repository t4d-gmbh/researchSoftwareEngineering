{% if build == "slides" %}

## Profiling and Debugging

### Key Principle

```{important}
**Profile before optimizing** — Intuition about performance is often wrong
```

:::::{grid} 1 1 2 2
:gutter: 3

::::{grid-item-card} 📊 Profiling Tools
**Quick timing**: `time.perf_counter()`  
**Full analysis**: `cProfile`  
**Line-by-line**: `line_profiler`  
**Memory**: `memray`

*Find bottlenecks first*
::::

::::{grid-item-card} 🐛 Debugging Strategy
1. Test **sequentially** first
2. Use **logging** (not print)
3. Reduce parallelism (2 workers)
4. Validate intermediate results

*Isolate before parallelizing*
::::

:::::

### Debugging Workflow

```{mermaid}
graph LR
    A[Identify Bug] --> B[Reproduce]
    B --> C[Locate Source]
    C --> D[Fix & Verify]
```

```{tip}
**Integration test**: Verify expected speedup (4 processes ≈ 4x faster)
```

{% else %}

## Profiling and Debugging Parallel Code

Developing efficient parallel code requires more than just distributing work across processors. Understanding where your code spends its time and identifying issues are critical skills for producing high-quality, performant software.

### The Importance of Profiling

Before attempting to parallelize code, you should understand its performance characteristics:

- **Where is time spent?** Computation, I/O, memory allocation, or communication?
- **What are the bottlenecks?** Identifying the 20% of code consuming 80% of runtime
- **Is parallelization appropriate?** Some bottlenecks (I/O, single-threaded libraries) won't benefit from parallelization

**Key principle**: Profile before optimizing. Intuition about performance is often wrong. Data-driven decisions prevent wasted effort.

### Profiling Tools for Python

Python offers several profiling approaches, each suited to different scenarios:

#### Ad-hoc Timing

For quick measurements of specific code blocks:

```python
import time

start = time.perf_counter()
# Code to measure
result = expensive_function()
elapsed = time.perf_counter() - start
print(f"Execution time: {elapsed:.3f} seconds")
```

**When to use**: Quick checks, comparing alternatives, timing specific functions

#### Deterministic Profiling with cProfile

The standard library's [`cProfile`](https://docs.python.org/3/library/profile.html) provides comprehensive statistics:

```python
import cProfile
import pstats

# Profile a function
profiler = cProfile.Profile()
profiler.enable()
your_function()
profiler.disable()

# Print results
stats = pstats.Stats(profiler)
stats.sort_stats('cumulative')
stats.print_stats(20)  # Top 20 functions
```

Or profile an entire script from the command line:

```bash
python -m cProfile -s cumulative your_script.py > profile_output.txt
```

**When to use**: Understanding overall program performance, identifying hot spots across the entire call stack

#### Line-by-Line Profiling

[`line_profiler`](https://github.com/pyutils/line_profiler) provides granular timing for each line in a function:

```bash
pip install line_profiler
```

```python
# Add @profile decorator (no import needed)
@profile
def your_function():
    result = []
    for i in range(1000):
        result.append(expensive_operation(i))
    return result
```

```bash
kernprof -l -v your_script.py
```

Output shows time spent per line, making it easy to identify specific bottlenecks.

**When to use**: Understanding performance within a specific function, identifying which lines are slowest

#### Memory Profiling with memray

[`memray`](https://bloomberg.github.io/memray/) tracks memory allocations with minimal overhead:

```bash
pip install memray
```

```bash
# Profile memory usage
memray run your_script.py

# Generate flamegraph visualization
memray flamegraph memray-output.bin
```

For pytest integration:

```bash
pip install memray pytest-memray
pytest --memray tests/
```

**When to use**: Identifying memory leaks, understanding memory allocation patterns, optimizing memory-intensive workflows

### Debugging Parallel Code

Debugging introduces additional challenges when code runs in parallel:

- Race conditions may appear intermittently
- Output from multiple processes can interleave
- Breakpoints in parallel contexts require careful handling

#### Types of Bugs

**Nice Bugs** cause immediate, obvious failures with clear tracebacks. These are relatively easy to fix once you understand how to read Python tracebacks. The [Real Python traceback tutorial](https://realpython.com/python-traceback/) is an excellent resource.

**Nasty Bugs** produce incorrect results without crashing, or cause errors far downstream from the actual problem. These require systematic debugging.

#### Systematic Debugging Process

1. **Identify the bug**: Confirm the behavior is genuinely wrong, not just unexpected due to input data variations

2. **Reproduce consistently**: Create a minimal test case that reliably triggers the bug. Ideally, write a unit test that fails.

3. **Locate the source**: Determine where logic diverges from expected behavior. Options include:
   - Adding diagnostic output (prefer logging over print statements)
   - Using interactive debuggers to inspect state
   - Binary search: comment out sections to isolate the problem

4. **Fix and verify**: Apply the fix, confirm it resolves the issue, and ensure no regressions

#### Debugging Tools

**Python's logging module**: Prefer structured logging over print statements:

```python
import logging

logging.basicConfig(level=logging.DEBUG)
logger = logging.getLogger(__name__)

def process_data(data):
    logger.debug(f"Processing {len(data)} items")
    result = complex_operation(data)
    logger.info(f"Completed processing, result size: {len(result)}")
    return result
```

Benefits:
- Control verbosity with log levels
- Timestamps and source location automatically included
- Can redirect to files or external systems
- Works well in parallel contexts (each process can log independently)

**Interactive debugging with ipdb**: [`ipdb`](https://github.com/gotcha/ipdb) provides an enhanced debugging interface:

```bash
pip install ipdb
```

Insert breakpoints in your code:

```python
def problematic_function(data):
    processed = initial_processing(data)
    
    import ipdb; ipdb.set_trace()  # Execution pauses here
    
    result = further_processing(processed)
    return result
```

When execution reaches the breakpoint, you get an interactive prompt to:
- Inspect variables: `print(processed)`
- Execute code: `len(processed)`
- Step through execution: `n` (next), `s` (step into), `c` (continue)
- View source context: `l` (list)

**IDE debugging**: Most modern IDEs (VS Code, PyCharm, Spyder) provide graphical debuggers with:
- Visual breakpoint setting
- Variable inspection panels
- Step-through controls
- Conditional breakpoints

#### Debugging Parallel Code Specifically

**Challenges:**
- Multiple processes produce interleaved output
- Debuggers may not attach to child processes automatically
- Non-deterministic timing can hide bugs

**Strategies:**

1. **Test sequentially first**: Debug your logic with serial execution before parallelizing

2. **Use process-safe logging**:
```python
import multiprocessing
import logging

def worker(task_id):
    logger = multiprocessing.get_logger()
    logger.info(f"Worker {task_id} starting")
    # Work here
    logger.info(f"Worker {task_id} completed")
```

3. **Reduce parallelism during debugging**: Test with 2 processes instead of 20 to simplify output

4. **Add deterministic checks**: Validate intermediate results within each process

### Best Practices

**Isolate profiling types**: Don't run memory and timing profiling simultaneously—overhead from one distorts results from the other.

**Establish baselines**: Profile before optimization to establish baseline performance. This enables measuring improvement objectively.

**Profile realistic workloads**: Use representative data sizes and problem complexity. Toy examples may not reveal actual bottlenecks.

**Automate profiling**: Integrate profiling into CI/CD pipelines to detect performance regressions early.

**Document expectations**: Add comments noting expected performance characteristics. Deviations signal potential issues.

### Further Resources

- [Real Python's tutorial on tracebacks](https://realpython.com/python-traceback/)
- [GeeksforGeeks ipdb tutorial](https://www.geeksforgeeks.org/using-ipdb-to-debug-python-code/)
- [Python logging module documentation](https://docs.python.org/3/library/logging.html)
- [Python profilers comparison](https://docs.python.org/3/library/profile.html)
- [Debugging multiprocessing](https://docs.python.org/3/library/multiprocessing.html#logging)

```{tip}
**Integration Testing for Parallel Code**: Write tests that verify not just correctness but also expected speedup. If 4 processes don't provide ~4x speedup for an embarrassingly parallel problem, investigate why.
```

{% endif %}
