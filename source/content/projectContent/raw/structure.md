# Structure for good practices

A well structured project facilitates development for you and your collaborators, but it can also ease the usage of cloud and cluster infrastructures.

## Research compendium

A **Research Compendium** is more than just a folder of files; it is a comprehensive collection of all digital materials and artifacts associated with a research project.

Its primary purpose is to enhance transparency, reproducibility, and accessibility. A complete compendium includes everything a third party would need to understand, replicate, and build upon your work. By structuring your project as a compendium, you ensure that others (including your future self) can verify your findings and reuse your data using the same methods or new ones.

In the following sections of this unit and the next, we will step through the process of building such a compendium.

## Separation of data, method, and output

When organizing scientific projects—especially in data science—one principle stands above the rest:

<center>

<span style="color = #b20032;"><strong>The separation of data, method, and output</strong></span>

</center>

This principle is fundamental for reproducibility, clarity, and maintainability. It dictates how the digital artifacts of a project should be physically organized on your disk.

At the most basic level, this implies creating distinct subdirectories for your inputs (data), your logic (scripts/methods), and your deliverables (results).

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

However, a robust project structure goes deeper. regarding **data**, we must strive to save both raw and intermediate forms. This allows us to trace the lineage of our results, document processing steps, and ensure we are working with "tidy data" amenable to analysis.

We expand the structure to reflect this:

```bash
my_data_science_project/
│
├── data/              # Directory for data
│   ├── raw/           # Original, immutable data dumps (often linked via git-lfs)
│   ├── processed/     # Cleaned and tidy data ready for analysis
│   └── synthesized/   # Data generated specifically for visualizations/presentation
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
│   ├── processed/     # Cleaned and processed data
│   └── synthesized/   # Synthesized data
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

## Detailed recommendations

Wilson et al. (2017) provide a comprehensive list of "good enough" practices for scientific computing. We provide their recommendations verbatim below, categorized by the aspect of the workflow they address.

---

**1. Data management**

* Save the raw data.
* Ensure that raw data are backed up in more than one location.
* Create the data you wish to see in the world.
* Create analysis-friendly data.
* Record all the steps used to process data.
* Anticipate the need to use multiple tables, and use a unique identifier for every record.
* Submit data to a reputable DOI-issuing repository so that others can access and cite it.

**2. Software**

* Place a brief explanatory comment at the start of every program.
* Decompose programs into functions.
* Be ruthless about eliminating duplication.
* Always search for well-maintained software libraries that do what you need.
* Test libraries before relying on them.
* Give functions and variables meaningful names.
* Make dependencies and requirements explicit.
* Do not comment and uncomment sections of code to control a program's behavior.
* Provide a simple example or test data set.
* Submit code to a reputable DOI-issuing repository.

**3. Collaboration**

* Create an overview of your project.
* Create a shared "to-do" list for the project.
* Decide on communication strategies.
* Make the license explicit.
* Make the project citable.

**4. Project organization**

* Put each project in its own directory, which is named after the project.
* Put text documents associated with the project in the doc directory.
* Put raw data and metadata in a data directory and files generated during cleanup and analysis in a results directory.
* Put project source code in the src directory.
* Put external scripts or compiled programs in the bin directory.
* Name all files to reflect their content or function.

**5. Keeping track of changes**

* Back up (almost) everything created by a human being as soon as it is created.
* Keep changes small.
* Share changes frequently.
* Create, maintain, and use a checklist for saving and sharing changes to the project.
* Store each project in a folder that is mirrored off the researcher's working machine.
* Add a file called CHANGELOG.txt to the project's docs subfolder.
* Copy the entire project whenever a significant change has been made.
* Use a version control system.

**6. Manuscripts**

* Write manuscripts using online tools with rich formatting, change tracking, and reference management.
* Write the manuscript in a plain text format that permits version control.

*We will discuss tracking changes in Sessions 06 and 08, and documentation and manuscript writing in Session 09 in much greater detail.*

## Reflection

Take a moment to consider the list above.
**Are the detailed recommendations of Wilson et al. (2017) aligned with the principle of separation of data, method, and output?**
**Which of their recommendations extend beyond this core principle?**

## Additional resources

* Nüst, D., Boettiger, C. and Marwick, B. (2018). How to Read a Research Compendium, arXiv:1806.09525. [https://doi.org/10.48550/arXiv.1806.09525](https://doi.org/10.48550/arXiv.1806.09525)
* The Turing Way: Research Compendia [https://book.the-turing-way.org/reproducible-research/compendia](https://book.the-turing-way.org/reproducible-research/compendia)

---

Source:\

* Wilson, G., Bryan, J., Cranston, K., Kitzes, J., Nederbragt, L., and Teal, T. K. (2017). Good enough practices in scientific computing. *PLoS Computational Biology*, 13(6), e1005510. [https://doi.org/10.1371/journal.pcbi.1005510](https://doi.org/10.1371/journal.pcbi.1005510).\
* Slides "STA472 Good Statistical Practice", Week 2 - Reproducibility and data, Project organization and software (by Eva Furrer).
