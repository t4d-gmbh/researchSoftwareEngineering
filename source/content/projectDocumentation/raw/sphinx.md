# Sphinx

You have likely encountered documentation sites such as:

* [edX Documentation](https://docs.edx.org/)
* [Blender Reference Manual](https://docs.blender.org/manual/en/latest/)
* [conda](https://docs.conda.io/projects/conda/en/latest/)
* [numpy](https://numpy.org/doc/stable/), [pandas](https://pandas.pydata.org/docs/), [NetworkX](https://networkx.org/documentation/stable/), ...
* [Using Git in Academia](https://t4d-gmbh.github.io/using-git-in-academia/)

Despite covering vastly different topics, these sites share a cohesive look and feel:

* They are content-rich and text-focused.
* They share a consistent structure for navigation and organization.

The common thread linking them is [Sphinx](https://www.sphinx-doc.org/en/master/index.html), a robust tool designed to create clean, searchable, and navigable documentation websites.

In their own words:

> Sphinx creates intelligent and beautiful documentation with ease.
> *Source: [https://www.sphinx-doc.org/en/master/index.html*](https://www.sphinx-doc.org/en/master/index.html)

Sphinx is uniquely suited for computational projects because:

* **Code Parsing:** It can parse Python code to automatically extract docstrings and call signatures, keeping documentation in sync with the codebase.
* **Automation:** It supports command-line builds, allowing for easy updates to documentation media.
* **CI/CD Integration:** It integrates seamlessly with pipelines, ensuring documentation is rebuilt automatically when code changes.
* **Hosting:** It pairs perfectly with remote services like GitHub and GitLab, which offer free hosting for the static HTML sites Sphinx generates.

With minimal effort, Sphinx allows you to transform well-documented code into a standalone, professional-grade documentation site.

### Setting Up Sphinx

Installation is straightforward via pip:

```bash
pip install sphinx

```

Once installed, initialize a new project structure using the quickstart command:

```bash
sphinx-quickstart

```

This interactive command will guide you through the basic configuration of your documentation project.

#### Sphinx Themes

Sphinx offers a rich ecosystem of themes to customize the visual presentation of your work. A theme bundles templates, stylesheets, and layouts to define the "look and feel" of the site.

Some popular themes include:

* **Alabaster**: The default Sphinx theme; simple, clean, and text-focused.
* **Read the Docs**: A highly popular theme designed for the *Read the Docs* hosting platform, featuring a distinct sidebar navigation.
* **Pyramid**: A theme optimized for large, complex documentation structures.
* **Sphinx Bootstrap Theme**: Utilizes the Bootstrap CSS framework to ensure a responsive, mobile-friendly design.

For a comprehensive gallery and installation instructions, visit the [Sphinx Themes](https://sphinx-themes.readthedocs.io/en/latest/) website.

To apply a theme, simply edit your `conf.py` configuration file:

```python
html_theme = 'your_theme_name'

```

*Replace `'your_theme_name'` with the actual name of the theme you wish to use.*

Most themes also allow for further customization via `conf.py`, such as changing color schemes or adding project logos.

### Building and deploying documentation

Once your project is configured, generating the website is done with a single command:

```bash
make html

```

This compiles your source files into static HTML within the `build/html` directory.

To deploy this output, you can utilize services like GitHub Pages or GitLab Pages. These platforms are designed to host static content and integrate naturally with Sphinx workflows.

### Integrating Sphinx with CI/CD pipelines

To ensure your documentation never drifts from your codebase, you can integrate Sphinx into your CI/CD pipeline.
This setup ensures that every time you push changes to your repository, the documentation is automatically rebuilt and deployed.

For instance, a simple GitHub Actions workflow can trigger a `make html` command and publish the results to GitHub Pages instantly.

After completing this unit, you are capable of addressing [Task 3 of this week's homework](https://www.google.com/search?q=/jump_to_id/).
You can safely do so now and return to the remaining units later.

---

Source:\

* [https://www.sphinx-doc.org/en/master/index.html](https://www.sphinx-doc.org/en/master/index.html)\
* [https://docs.github.com/en/pages/getting-started-with-github-pages](https://docs.github.com/en/pages/getting-started-with-github-pages)\
* [https://docs.gitlab.com/ee/user/project/pages/](https://docs.gitlab.com/ee/user/project/pages/)
