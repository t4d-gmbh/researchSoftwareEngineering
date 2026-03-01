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

