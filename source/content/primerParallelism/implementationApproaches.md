{% if build == "slides" %}
# Primer on Parallelism

## Implementation Approaches

:::::{grid} 1 1 2 2
:gutter: 3

::::{grid-item-card} 🧵 Multi-Threading
**Shared memory** within process

✅ Fast communication  
✅ Low overhead  
⚠️ Race conditions  
⚠️ Python GIL limitation

*Tightly coupled tasks*
::::

::::{grid-item-card} ⚙️ Multi-Processing
**Isolated processes** with IPC

✅ True parallelism  
✅ No race conditions  
⚠️ Communication overhead  
⚠️ Higher memory use

*Embarrassingly parallel*
::::

:::::

### Communication Trade-off

```{mermaid}
graph LR
    subgraph "Multi-Threading"
    T1[Thread 1] -.shared.-> M[Memory]
    T2[Thread 2] -.shared.-> M
    end
    
    subgraph "Multi-Processing"
    P1[Process 1] -->|IPC| P2[Process 2]
    end
```

```{tip}
**Litmus test**: "Do the same thing to 1000 inputs independently" → Multi-processing
```

{% else %}

## Implementing Parallelism: Multi-Threading vs. Multi-Processing

Different programming approaches enable parallelism at different architectural levels. Understanding the distinction between multi-threading and multi-processing is crucial for implementing efficient parallel solutions.

### Multi-Threading: Shared Memory Parallelism

**Multi-threading** involves running multiple threads within a single process. All threads share the same memory space, enabling efficient communication but requiring careful synchronization.

**Characteristics:**
- Threads within a process share memory and resources
- Efficient information exchange through shared variables
- Risk of race conditions and deadlocks if not properly managed
- Lower overhead for thread creation and context switching

**Languages with native parallel multi-threading support:**
- Rust
- Go
- C++
- Java

These languages can achieve true parallelism via multi-threading, with multiple threads executing simultaneously on different cores.

**When to use multi-threading:**
- Fine-grained parallelism requiring frequent data exchange
- Tasks that benefit from shared state
- When using languages that support thread-level parallelism without restrictions

### Multi-Processing: Isolated Execution

**Multi-processing** involves running multiple independent processes, each with its own memory space and Python interpreter instance.

**Characteristics:**
- Processes are completely isolated from each other
- Communication requires explicit Inter-Process Communication (IPC) mechanisms
- Eliminates race conditions but adds communication overhead
- Higher memory footprint (each process has its own memory)

**When to use multi-processing:**
- CPU-intensive tasks in Python or other GIL-restricted languages
- Embarrassingly parallel problems with minimal communication needs
- When memory isolation is desirable for stability or security
- Tasks that can tolerate IPC overhead

### The Communication Trade-off

The key distinction between these approaches lies in communication efficiency:

```{mermaid}
graph LR
    subgraph "Multi-Threading"
    T1[Thread 1] -.shared memory.-> M[Memory]
    T2[Thread 2] -.shared memory.-> M
    T3[Thread 3] -.shared memory.-> M
    end
    
    subgraph "Multi-Processing"
    P1[Process 1] -->|IPC| P2[Process 2]
    end
```

**Multi-threading advantages:**
- Near-instantaneous data sharing through memory
- Minimal overhead for communication
- Ideal for tightly coupled problems

**Multi-threading challenges:**
- Synchronization complexity
- Potential for difficult-to-debug race conditions
- Limited or restricted in some languages (Python's GIL)

**Multi-processing advantages:**
- True parallelism regardless of language restrictions
- Process isolation prevents cross-contamination
- Well-suited for coarse-grained parallelism

**Multi-processing challenges:**
- IPC overhead can be substantial
- Higher memory consumption
- More complex data sharing mechanisms

### Language-Specific Considerations

Many languages offer abstractions that simplify multi-core parallelism, handling task lifecycle and communication automatically. However, for cluster or cloud environments, additional software infrastructure is required:

- **Workload managers**: Systems like [Slurm](https://en.wikipedia.org/wiki/Slurm_Workload_Manager) handle job scheduling and resource allocation on HPC clusters
- **Distributed computing frameworks**: Tools like Dask, Ray, or Spark provide abstractions for managing parallelism across multiple machines
- **Orchestration platforms**: Kubernetes and similar systems manage containerized workloads in cloud environments

### Practical Guidance

1. **Identify coupling level**: Determine if your problem is embarrassingly parallel, loosely coupled, or tightly coupled

2. **Choose the appropriate approach**:
   - Embarrassingly parallel → Multi-processing or distributed execution
   - Loosely coupled → Multi-processing with periodic synchronization
   - Tightly coupled → Multi-threading (if language supports it) or single high-performance node

3. **Start simple**: Begin with the simplest parallel approach that addresses your needs. Avoid premature optimization of communication patterns.

4. **Profile before scaling**: Test your parallel implementation on a small scale before deploying to large clusters or cloud resources. Identify bottlenecks early.

5. **Consider existing frameworks**: Before implementing custom parallelization, investigate whether established libraries or frameworks already solve your problem (see language-specific resources below).

### Communication Overhead in Practice

The impact of IPC overhead varies dramatically with problem characteristics:

**Negligible overhead scenarios (ideal for multi-processing):**
- Processing thousands of independent files
- Parameter sweeps with no inter-task dependencies
- Monte Carlo simulations
- Batch processing of images or data samples

**Significant overhead scenarios (consider multi-threading or reduce parallelization):**
- Iterative algorithms requiring frequent synchronization
- Shared mutable state updated by all tasks
- Fine-grained operations with minimal computation between communications
- Real-time systems with strict latency requirements

```{tip}
**The embarrassingly parallel litmus test**: If you can describe your problem as "do the same thing to 1000 different inputs independently," you likely have an embarrassingly parallel problem—an ideal candidate for multi-processing or distributed computing.
```

{% endif %}
