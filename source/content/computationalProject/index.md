# Computational Project

{% if slide %}

```{toctree}
:maxdepth: 3

./definition
./whatBelongsInAProject
./goodScientificPractice
./gSPAdendum
./structure
./projectScaffolding
```

{% else %}


```{include} ./definition.md
```
```{include} ./goodScientificPractice.md
```
```{include} ./gSPAdendum.md
```
```{include} ./structure.md
```
```{include} ./projectScaffolding.md
```
```{include} ./limitations.md
```

{.smaller}
**Sources**:

* [https://packaging.python.org/en/latest/guides/writing-pyproject-toml/](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/),\
* [https://peps.python.org/](https://peps.python.org/),\
* [https://setuptools.pypa.io/en/latest](https://setuptools.pypa.io/en/latest),\
* [https://docs.python.org/3.12/tutorial/modules.html](https://docs.python.org/3.12/tutorial/modules.html).
* Wilson, G., Bryan, J., Cranston, K., Kitzes, J., Nederbragt, L., and Teal, T. K. (2017). Good enough practices in scientific computing. *PLoS Computational Biology*, 13(6), e1005510. [https://doi.org/10.1371/journal.pcbi.1005510](https://doi.org/10.1371/journal.pcbi.1005510).\
* Slides "STA472 Good Statistical Practice", Week 2 - Reproducibility and data, Project organization and software (by Eva Furrer).
* [https://setuptools.pypa.io/en/latest](https://setuptools.pypa.io/en/latest),\
* [https://docs.python.org/3.12/tutorial/modules.html](https://docs.python.org/3.12/tutorial/modules.html),\
* Marwick, B., Boettiger, C., and Mullen, L. (2018). Packaging Data Analytical Work Reproducibly Using R (and Friends). *The American Statistician*, 72(1), 80–88. [https://doi.org/10.1080/00031305.2017.1375986](https://doi.org/10.1080/00031305.2017.1375986)

{% endif %}
