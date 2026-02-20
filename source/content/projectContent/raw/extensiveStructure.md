# Extensive structure

There is no single "correct" way to structure a scientific Python project, but consistency is key.
The structure below is a robust, widely accepted standard that balances simplicity with functionality. It aligns closely with modern data science best practices often recommended by senior engineers and AI assistants alike.

```bash
my_data_science_project/
│
├── data/
│   ├── raw/                  # Original, immutable data dumps (often linked via git-lfs)
│   ├── processed/            # Cleaned, tidy data ready for analysis
│   └── synthesized/          # Aggregated data for visualizations and reporting
│
├── src/                      # Source code for the project
│   └── my_project            # The actual Python package directory
│       ├── __init__.py       # Marks this directory as a Python package
│       │                     # Submodules below are examples of logical separation:
│       ├── data.py           # Functions to download or generate data
│       ├── cleaning.py       # Functions to transform raw data into features
│       ├── visualization.py  # Functions for generating plots
│       └── ...
│
├── notebooks/                # Jupyter notebooks for interactive exploration
│   └── explore/              # Notebooks specific to EDA
│
├── scripts/                  # Standard Python scripts for batch execution
│   └── explore/              # Scripts specific to EDA
│
├── results/                  # Directory for project outputs
│   ├── figures/              # Generated plots and graphics
│   ├── tables/               # CSVs or Excel files of summary statistics
│   └── reports/              # PDF or HTML reports
│
├── tests/                    # Automated unit tests
│   ├── requirements.txt      # Dependencies specifically for running tests (e.g., pytest)
│   └── test_<module>.py      # Test suites corresponding to src modules
│
├── docs/                     # Documentation source files
│   ├── requirements.txt      # Dependencies for building docs (e.g., Sphinx, MkDocs)
│   └── source/               # Source files (rst/md) for the documentation site
│
├── pyproject.toml            # Project metadata and build configuration
├── requirements.txt          # Core dependencies needed to run the analysis
├── README.md                 # Entry point for developers (overview and setup)
├── LICENSE                   # Legal usage terms
└── .gitignore                # Rules for file exclusion in version control

```

* **Note on redundancy:** `scripts` and `notebooks` often serve similar purposes. If your workflow is entirely notebook-based, you may omit `scripts`, and vice-versa.
* **Optional folders:** `docs` and `tests` are only necessary if you are compiling formal documentation or running automated tests—though both are highly recommended for robust research.

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

---

Source:\

* [https://setuptools.pypa.io/en/latest](https://setuptools.pypa.io/en/latest),\
* [https://docs.python.org/3.12/tutorial/modules.html](https://docs.python.org/3.12/tutorial/modules.html),\
* Marwick, B., Boettiger, C., and Mullen, L. (2018). Packaging Data Analytical Work Reproducibly Using R (and Friends). *The American Statistician*, 72(1), 80–88. [https://doi.org/10.1080/00031305.2017.1375986](https://doi.org/10.1080/00031305.2017.1375986)
