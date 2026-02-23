{% if build == "slides" %}
## Orthogonal Code
{% else %}
## Orthogonal Code
{% endif %}

{% if slide %}

### The Idea

> Two components are **orthogonal** if changing one does not affect the other.

:::::{grid} 2
::::{grid-item-card} Benefits
- Run parts of your analysis in isolation
- Bugs stay contained to one component
- Reuse components across projects
- Write tests for one module without mocking the rest
::::
::::{grid-item-card} Trade-offs
- More upfront planning required
- Execution flow can be harder to trace
- Over-splitting leads to fragmentation
::::
:::::

### Example: Computation vs. Visualization

:::{admonition} Non-orthogonal
:class: warning
Clustering and plotting mixed in the same loop. Want to change a plot color? Re-run the clustering.
:::

:::{admonition} Orthogonal
:class: tip
Separate the computation from the visualization. Store results, then plot independently. Change colors without re-running a 3-day computation.
:::

{% else %}

### The Concept

In linear algebra, two vectors are orthogonal if their inner product is zero. Movement along one produces no movement along the other. 
Software development borrows this idea: two pieces of code are **orthogonal** if changes in one do not affect the behavior of the other.

Your database code should be orthogonal to your user interface code. Changing the color of a button should not break a database query. Changing the database schema should not change the color of a button.

### Benefits

- **Isolated execution:** Run specific parts of your analysis without re-running everything. No need to redo a heavy computation just to tweak a plot style.
- **Localized bugs:** If a component fails, the issue is likely within that component, not a side effect from somewhere else.
- **Reusability:** A plotting function that knows nothing about how the data was computed can be used for any data.
- **Testability:** Write unit tests for one module without mocking the entire system.

### Trade-offs

- **Upfront effort:** Orthogonal code requires designing interfaces and data structures to pass information between decoupled components.
- **Harder to trace:** The logic jumps between independent functions and modules rather than flowing linearly through a single script.
- **Fragmentation risk:** Taken too far, you end up with hundreds of tiny micro-functions that are tedious to navigate.

### Example

Consider a script that performs K-means clustering on the Iris dataset. A non-orthogonal version mixes computation and visualization in the same loop:

```python
for i, (x_index, y_index) in enumerate(pairs):
    # Computation
    kmeans = KMeans(n_clusters=3, random_state=42)
    kmeans.fit(X[:, [x_index, y_index]])
    labels = kmeans.labels_

    # Visualization that tightly coupled to computation
    axs[i].scatter(X[:, x_index], X[:, y_index], c=labels, cmap='viridis',
                   edgecolor='k', s=100)
```

Want to change the plot color? You re-run the clustering. Want different clusters? You re-draw everything.

The orthogonal version separates the two concerns. Computation runs first and stores its results:

```python
def perform_kmeans(X, x_index, y_index, n_clusters=3):
    kmeans = KMeans(n_clusters=n_clusters, random_state=42)
    kmeans.fit(X[:, [x_index, y_index]])
    return kmeans.labels_

all_labels = [perform_kmeans(X, x, y) for x, y in pairs]
```

Visualization uses the stored results independently:

```python
def plot_clusters(X, labels, x_index, y_index, title, ax):
    ax.scatter(X[:, x_index], X[:, y_index], c=labels, cmap='viridis',
               edgecolor='k', s=100)
    ax.set_title(title)

for i, (x_index, y_index) in enumerate(pairs):
    plot_clusters(X, all_labels[i], x_index, y_index, titles[i], axs[i])
```

The code is longer, but the payoff is that if the computation takes three days on a cluster, you run it once, save `all_labels`, and tweak your plots locally as many times as you want.

{% endif %}
