# Orthogonal Code

> **Mathematical Definition:**
> Orthogonality is the generalization of perpendicularity in linear algebra. Two vectors are orthogonal if their inner product is zero, meaning the projection of one onto the other is .
> In simple terms: movement along one vector produces **no** movement along the other. They are independent.

In computer science, we borrow this concept to describe the relationship between software components.
Two pieces of code are **orthogonal** if changes in one do not affect the behavior or state of the other. Ideally, your "database code" should be orthogonal to your "user interface code"—changing the color of a button should not break the database query, and changing the database schema should not change the color of the button.

## Benefits

Why is this independence so valuable?

* **Step-by-Step Execution:** Orthogonal design allows you to run specific parts of your analysis in isolation. You don't need to re-run a heavy computation just to test a new plotting style.
* **Localized Changes:** Bugs are contained. If a specific component fails, you know the issue is likely within that component, not a side effect from an unrelated part of the system.
* **Reusability:** Independent components can be plugged into new projects easily. A plotting function that doesn't "know" about how the data was calculated can be used for any data.
* **Easier Testing:** You can write unit tests for one module without mocking the entire system.

## Drawbacks and Challenges

* **Initial Complexity:** Writing orthogonal code requires more upfront planning. You have to design interfaces and data structures to pass information between decoupled components.
* **Learning Curve:** For new developers, tracing the flow of execution can be harder because the logic isn't just a single linear script; it jumps between independent functions and modules.
* **Fragmentation:** If taken too far, you risk "fragmentation"—a codebase consisting of hundreds of tiny, disconnected micro-functions that are tedious to manage.

## Example for Non-Orthogonal Code

Consider the following script, which performs K-means clustering on the IRIS dataset.
At first glance, it looks fine. However, notice that the **computation** (clustering) and the **visualization** (plotting) are mixed inside the same loop.

This is **non-orthogonal** because they are tightly coupled. If you want to change the plot color, you have to re-run the clustering. If you want to change the number of clusters, you have to re-draw the plots.

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn import datasets
from sklearn.cluster import KMeans

# Load the Iris dataset
iris = datasets.load_iris()
X = iris.data  # Extract features

# Define the pairs of axes to plot
pairs = [(0, 1), (0, 2), (1, 2)]  # (Sepal Length, Sepal Width), 
                 # (Sepal Length, Petal Length), (Sepal Width, Petal Length)
titles = [
    'Sepal Length vs. Sepal Width (K-means Clustering)',
    'Sepal Length vs. Petal Length (K-means Clustering)',
    'Sepal Width vs. Petal Length (K-means Clustering)'
]

# Create a figure with 3 subplots in a row
fig, axs = plt.subplots(1, 3, figsize=(18, 5))

# Loop over the pairs of axes
for i, (x_index, y_index) in enumerate(pairs):
    # --- COMPUTATION ---
    # Perform K-means clustering on the selected feature pair
    kmeans = KMeans(n_clusters=3, random_state=42)
    kmeans.fit(X[:, [x_index, y_index]])  # Use only the selected features
    labels = kmeans.labels_
    
    # --- VISUALIZATION ---
    # Create scatter plot inside the same loop
    axs[i].scatter(X[:, x_index], X[:, y_index], c=labels, cmap='viridis',
                   edgecolor='k', s=100)
    axs[i].set_title(titles[i])
    axs[i].set_xlabel(iris.feature_names[x_index])
    axs[i].set_ylabel(iris.feature_names[y_index])

# Adjust layout
plt.tight_layout()
plt.show()

```

## Orthogonalized Version

To fix this, we separate the concerns. We create one block of code responsible *only* for generating data (Computation) and another responsible *only* for displaying it (Visualization).
The list `all_labels` acts as the interface between these two independent worlds.

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn import datasets
from sklearn.cluster import KMeans

# Load the Iris dataset
iris = datasets.load_iris()
X = iris.data  # Features

# Define the pairs of features to cluster
pairs = [(0, 1), (0, 2), (1, 2)]  # (Sepal Length, Sepal Width), 
                 # (Sepal Length, Petal Length), (Sepal Width, Petal Length)

# Store labels for each feature pair
all_labels = []

# ###
# PART 1: COMPUTATION (The "K-means part")
# ###
def perform_kmeans(X, x_index, y_index, n_clusters=3):
    """Perform K-means clustering on the specified features."""
    kmeans = KMeans(n_clusters=n_clusters, random_state=42)
    kmeans.fit(X[:, [x_index, y_index]])  # Use only the selected features
    return kmeans.labels_

# Loop over the pairs of axes to compute K-means clustering
for x_index, y_index in pairs:
    labels = perform_kmeans(X, x_index, y_index)
    all_labels.append(labels)

# ###
# PART 2: VISUALIZATION (The "Plotting part")
# ###
# Define axes titles
titles = [
    'Sepal Length vs. Sepal Width (K-means Clustering)',
    'Sepal Length vs. Petal Length (K-means Clustering)',
    'Sepal Width vs. Petal Length (K-means Clustering)'
]

def plot_clusters(X, labels, x_index, y_index, title, x_label, y_label, ax):
    """Plot the clusters for the specified features."""
    ax.scatter(X[:, x_index], X[:, y_index], c=labels, cmap='viridis', edgecolor='k', s=100)
    ax.set_title(title)
    ax.set_xlabel(x_label)
    ax.set_ylabel(y_label)

# Create a figure with 3 subplots in a row
fig, axs = plt.subplots(1, 3, figsize=(18, 5))

# Now plot the results using the pre-computed data
for i, (x_index, y_index) in enumerate(pairs):
    plot_clusters(X, all_labels[i], x_index, y_index, titles[i], iris.feature_names[x_index], iris.feature_names[y_index], axs[i])

# Adjust layout
plt.tight_layout()
plt.show()

```

While the code is longer, the advantage is massive.
Imagine if the **Computations** took 3 days to run on a supercomputer.
In the orthogonal version, you could run Part 1 once, save `all_labels` to a file, and then run Part 2 hundreds of times on your laptop to tweak the colors, font sizes, and titles without ever re-running the heavy calculation.

## Reflection

Interpret the output of the clustering.

1. What happens to the visual result if you change `n_clusters` to 2 or 4?
2. How would you mathematically determine the optimal number of clusters?

---

Source:\

* Hunt, A., & Thomas, D. (2019). The Pragmatic Programmer: Your journey to mastery. Addison-Wesley. ISBN 9780135957059. (Original publication)
