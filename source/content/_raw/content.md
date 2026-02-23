## Metadata

Comprehensive metadata is the backbone of any transparent software project. It ensures clarity for new users, facilitates reproducibility for researchers, and fosters effective collaboration.
While there are many ways to provide this information, certain standards have emerged.
The most ubiquitous files are `README.md` and `LICENSE`, which are expected in virtually every open-source repository.

For language-specific contexts, other files become relevant, such as `requirements.txt` or `pyproject.toml` in the Python ecosystem.

Before diving into specific files, it is vital to understand a core data management principle that applies directly to metadata:

> **Single Source Of Truth (SSOT)**
> SSOT is the practice of structuring information so that every data element is mastered (or edited) in only one place.
> In the context of project metadata, this prevents redundancy and contradiction. For example, your project's version number or license text should be defined in one file and referenced elsewhere, rather than manually typed into the `README`, the `LICENSE`, and the source code headers separately.
> By adhering to SSOT, you ensure that updating a piece of information (like a dependency version) in one location automatically propagates to all other systems, guaranteeing consistency and reducing maintenance overhead.

### Python project metadata

### The `requirements.txt` file

The `requirements.txt` file is the traditional method for pinning specific dependencies to ensure a reproducible environment.
It acts as a simple list:

* **Package Names**: The library required.
* **Version Specifiers**: strict rules on which versions are allowed (e.g., `pandas>=2.0`, `numpy==1.26.0`).

*Tip: For complex projects, separate your concerns by using multiple files, such as `requirements-dev.txt` for linting/testing tools and `requirements.txt` for the main application.*

### The `pyproject.toml` file

The `pyproject.toml` is the modern, unified configuration file for Python tooling. Written in TOML (Tom's Obvious, Minimal Language), it is designed to be easily readable by both humans and machines.

While it can handle complex configurations for linters, testers, and formatters, its primary role is defining package metadata.
Below is a template demonstrating how to use `pyproject.toml` to enforce the **SSOT** principle by dynamically fetching data from other files:

```toml
[project]
name = "your_project_name"
authors = [
  { name="Your Name", email="your.email@example.com" },
  { name="Another Name", email="your.email@example.com" },
]
# Dynamic fields are not hardcoded here but fetched at build time
dynamic = ["version", "dependencies", "optional-dependencies"]
description = "Brief description of your project"
# Read the description directly from the README to avoid duplication
readme = "README.md"
requires-python = ">=3.12"
classifiers = [
    "Programming Language :: Python :: 3",
    "Operating System :: OS Independent",
]
# Point to the standard LICENSE file
license.file = "LICENSE"

[tool.setuptools.dynamic.dependencies]
# Read dependencies from the standard requirements file
file = ["requirements.txt"]

[tool.setuptools.dynamic.optional-dependencies.testing]
file = ["tests/requirements.txt"]

[tool.setuptools.dynamic.optional-dependencies.docs]
file = ["docs/requirements.txt"]

[project.urls]
Homepage = "https://your_project_homepage.com"
Issues = "https://your_project_homepage.com/issues"

# Configuration to fetch the version automatically from Git tags
[tool.setuptools_scm]

[build-system]
requires = ["setuptools>=64.0", "setuptools_scm>=8"]
build-backend = "setuptools.build_meta"

```

**Why this structure matters:**

The `dynamic` section (line 7) is the key to efficiency.
It tells the build system *not* to look for hard-coded values in this file, but to generate them at build time.

In this specific configuration:

1. **Version:**  
   Fetched from Git tags (via `setuptools_scm`). You never need to manually update a version string in the code.
2. **Dependencies:**  
   Read from `requirements.txt`. You only manage dependencies in one place.
3. **Readme:**
   The long description on PyPI will automatically match your `README.md`.
4. **License:**  
   Referenced from the `LICENSE` file.

This setup ensures that your metadata is always consistent across your source control, your documentation, and your distributed package.


**Additional resources**:  
* Structure and format of TOML files [https://en.wikipedia.org/wiki/TOML](https://en.wikipedia.org/wiki/TOML), [https://toml.io/en/latest](https://toml.io/en/latest)



## The `src/` folder

The `src` directory is central to a well-engineered Python project. Standard tools like `pip` and [`setuptools`](https://www.google.com/search?q=%5Bhttps://setuptools.pypa.io/en/latest/%5D(https://setuptools.pypa.io/en/latest/)) are designed to recognize this layout (often called the "src-layout").

In Python, "installing" a package essentially means telling the interpreter where to find the code so it can be imported from anywhere, regardless of your current working directory.
By placing your code inside `src/my_project`, you ensure that your analysis logic is isolated from your runtime scripts and configuration files.

When you create a subdirectory (e.g., `my_project`) containing an `__init__.py` file, Python treats it as a **package** (see the [official modules tutorial](https://docs.python.org/3.12/tutorial/modules.html)). Any `.py` file inside becomes a submodule that you can import, exactly like you import third-party libraries such as `pandas` or `numpy`.

**Example:**

Consider the following file structure:

```plaintext
.
.
├── src/
│   └── my_project
│       ├── __init__.py
│       └── data.py
├── pyproject.toml
.
.

```

If `data.py` contains a simple function:

```python
# src/my_project/data.py
def say_hello(name:str)->str:
    """Greets a name"""
    print(f"Hello {name}")

```

And assuming you have a valid `pyproject.toml` (as described in [0511Metadata.md](https://www.google.com/search?q=/jump_to_id/0511Metadata.md)), you can integrate this package into your environment:

1. **Install the project** in "editable" mode:
```bash
pip install -e .

```


2. **Import and use** the function in *any* other script, notebook, or shell on your system:
```python
>>> from my_project.data import say_hello
>>> say_hello(name="Bob")
Hello Bob

```



## Testing and Documentation

We will cover testing in depth in Section 07 and documentation compilation in Section 09.

From a structural perspective, it is best practice to keep the dependencies for these tasks separate. This is why you often see dedicated `requirements.txt` files inside `tests/` or `docs/`—you don't need documentation generators installed just to run the analysis, and you don't need testing frameworks installed just to read the docs.

*Note on Notebooks:* While tools like Quarto allow you to author documents using notebooks, we generally keep these source files in `notebooks/`. The `docs/` folder is reserved for the structure and configuration that compiles these notebooks into a final website or book.

## Additional resources

* Research Compendium [https://book.the-turing-way.org/reproducible-research/compendia](https://book.the-turing-way.org/reproducible-research/compendia)

