## Structure for good practices

{% if page %}
A well structured project facilitates development for you and your collaborators, but it can also ease the usage of cloud and cluster infrastructures.
{% endif %}


### Separation of data, method, and output

{% if page %}
When organizing scientific projects (especially in data science) one principle stands above the rest:

<center>

<span style="color = #b20032;"><strong>The separation of data, method, and output</strong></span>

</center>

This principle is fundamental for reproducibility, clarity, and maintainability. It dictates how the digital artifacts of a project should be physically organized on your disk.

At the most basic level, this implies creating distinct subdirectories for your inputs (data), your logic (scripts/methods), and your deliverables (results).
{% endif %}

{% if slide %}

::::{tab-set}
:::{tab-item} Basic
Distinct subdirectories for inputs, logic, and deliverables:

```bash
my_data_science_project/
│
├── data/              # Directory for input data
│
├── scripts/           # Directory for Python scripts (exploration and analysis)
│
├── results/           # Directory for output (plots, figures, tables)
.  
.

```
:::

:::{tab-item} Data stages
Preserve raw, intermediate, and final data:

```bash
my_data_science_project/
│
├── data/              # Directory for data
│   ├── raw/           # Original, immutable data dumps (often linked via git-lfs)
│   ├── interim/       # Intermediary data resulting from filtering, cleaning, etc. 
│   ├── final/         # Cleaned, tidy data used for an analysis
│   └── synth/         # Aggregated data used for visualizations and reporting
│
├── scripts/           # Directory for Python scripts
│
├── results/           # Directory for output
.
.

```
:::

:::{tab-item} + Metadata
Make the project self-describing:

```bash
my_data_science_project/
│
├── data/
│   ├── raw/           # Original, immutable data dumps
│   ├── interim/       # Intermediary data
│   ├── final/         # Cleaned, tidy data
│   └── synth/         # Aggregated data for reporting
│
├── scripts/           # Python scripts
│
├── results/           # Output
│
├── pyproject.toml     # Project metadata and dependencies (SSOT)
├── requirements.txt   # Python package dependencies
├── README.md          # Project overview and instructions
├── LICENSE            # License governing usage
└── .gitignore         # Files and directories to ignore in Git

```
:::
::::

{% else %}

```bash
my_data_science_project/
│
├── data/              # Directory for input data
│
├── scripts/           # Directory for Python scripts (exploration and analysis)
│
├── results/           # Directory for output (plots, figures, tables)
.  
.

```

However, a robust project structure goes deeper. Regarding **data**, we must strive to save both raw and intermediate forms. This allows us to trace the lineage of our results, document processing steps, and ensure we are working with "tidy data" amenable to analysis.

We expand the structure to reflect this:

```bash
my_data_science_project/
│
├── data/              # Directory for data
│   ├── raw/           # Original, immutable data dumps (often linked via git-lfs)
│   ├── interim/       # Intermediary data resulting from filtering, cleaning, etc. 
│   ├── final/         # Cleaned, tidy data used for an analysis
│   └── synth/         # Aggregated data used for visualizations and reporting
│
├── scripts/           # Directory for Python scripts
│
├── results/           # Directory for output
.
.

```

Finally, as discussed in the previous unit, a project must contain essential metadata to be self-describing. We add these files to the root:

```bash
my_data_science_project/
│
├── data/              # Directory for data
│   ├── raw/           # Original, immutable data dumps
│   ├── interim/       # Intermediary data resulting from filtering, cleaning, etc. 
│   ├── final/         # Cleaned, tidy data used for an analysis
│   └── synth/         # Aggregated data used for visualizations and reporting
│
├── scripts/           # Directory for Python scripts
│
├── results/           # Directory for output
│
├── pyproject.toml     # Project metadata and dependencies (SSOT)
├── requirements.txt   # Python package dependencies
├── README.md          # Project overview and instructions
├── LICENSE            # License governing usage
└── .gitignore         # Files and directories to ignore in Git

```

{% endif %}

### Extensive structure

{% if page %}
There is no single "correct" way to structure a scientific Python project, but consistency is key.
The structure below is a robust, widely accepted standard that balances simplicity with functionality. It aligns closely with modern data science best practices often recommended by senior engineers and AI assistants alike.

```bash
my_data_science_project/
│
├── data/
│   ├── raw/                  # Original, immutable data dumps (often linked via git-lfs)
│   ├── interim/              # Intermediary data resulting from filtering, cleaning, etc. 
│   ├── final/                # Cleaned, tidy data usdef for an analysis
│   └── synth/                # Aggregated data used for visualizations and reporting
│
├── src/                      # Source code for the project
│   └── my_project            # The actual Python package directory
│       ├── __init__.py       # Marks this directory as a Python package
│       │                     # Submodules below are examples of logical separation:
│       ├── data.py           #    Functions to download or generate data
│       ├── cleaning.py       #    Functions to transform raw data into features
│       ├── visualization.py  #    Functions for generating plots
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
* **Optional folders:** `docs` and `tests` are only necessary if you are compiling formal documentation or running automated tests, though both are highly recommended for robust research.

**Additional resources**:

* Nüst, D., Boettiger, C. and Marwick, B. (2018). How to Read a Research Compendium, arXiv:1806.09525. [https://doi.org/10.48550/arXiv.1806.09525](https://doi.org/10.48550/arXiv.1806.09525)
* The Turing Way: Research Compendia [https://book.the-turing-way.org/reproducible-research/compendia](https://book.the-turing-way.org/reproducible-research/compendia)
{% endif %}

{% if slide %}
Beyond the basics, a full project adds dedicated folders for source packages, tests, documentation, and results:

:::::{grid} 2
::::{grid-item-card} Core
- `src/my_project/` — Python package
- `scripts/` — batch execution
- `notebooks/` — interactive exploration
- `config/` — settings, parameters
::::
::::{grid-item-card} Quality & Output
- `tests/` — automated unit tests
- `docs/` — documentation source
- `results/figures/` — plots, tables, reports
- `benchmark/` — performance tracking
::::
:::::

:::{admonition} Full tree
:class: dropdown

```bash
my_data_science_project/
│
├── data/
│   ├── raw/           ├── interim/
│   ├── final/         └── synth/
├── src/my_project/
│   ├── __init__.py    ├── data.py
│   ├── cleaning.py    └── visualization.py
├── notebooks/         ├── scripts/
├── results/           ├── tests/
├── docs/              ├── benchmark/
├── pyproject.toml     ├── requirements.txt
├── README.md          ├── LICENSE
└── .gitignore
```
:::
{% endif %}

