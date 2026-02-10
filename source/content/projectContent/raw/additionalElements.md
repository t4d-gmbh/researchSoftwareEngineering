# Additional features

We will briefly cover a few supplementary features that enhance the utility of a research compendium.

## Citation file

Research projects are frequently linked to academic publications. To ensure that readers can easily and accurately cite your work, it is best practice to include a citation file.
The standard format for this is `CITATION.cff` (Citation File Format), a plain text YAML file placed in the root directory.
Below is a minimalistic example of what this file looks like:

```yaml
authors:
  - family-names: Muster
    given-names: Urs
cff-version: 1.2.0
message: "If you use this software, please cite it using these metadata."
title: "My first Python research compendium"

```

## Configuration files

The project structure presented in previous sections is agnostic to specific tools or deployment environments. Consequently, it does not include configuration files for automation pipelines, as these vary by service provider.
For example, you might encounter a `.gitlab-ci.yml` for GitLab, a `.travis.yml` for Travis CI, or files within `.github/workflows/` for GitHub Actions. These files are essential for CI/CD but are specific to the platform you choose.

## Linking external content

The structure we have proposed consolidates data, scripts, tests, and documentation into a single repository.
The primary advantage of this "monolithic" approach is simplicity: it allows you to track and version all elements of the project jointly.

However, cramming everything into one repository can become problematic as a project scales:

* **Distribution:** Different components may need to be shared under different licenses or restrictions. For instance, your data might be reused across multiple projects, or it might originate from a third-party study that prohibits redistribution.
* **Complexity:** Large repositories can become unwieldy, obscuring the relationship between individual elements and making the history difficult to navigate.

To avoid a monolithic repository while maintaining structure, you can link multiple smaller repositories using `git submodules` (see Section 06).
This allows you to include an external element (such as a raw dataset) by pointing to a specific commit in another Git repository.

Deciding when to split a project into multiple repositories is somewhat arbitrary, but a separate repository is generally recommended if:

* An element (e.g., a specific dataset) can be useful in isolation for other contexts.
* An element (e.g., documentation or a specific software module) needs to evolve independently of the main analysis.
* An element is subject to different ownership, licensing, or terms of use.

**A note on manuscripts:**
For papers, book chapters, or theses, we strongly recommend creating dedicated repositories.
You can still reference resources from your analysis repository (e.g., figures or tables) by including the analysis repo as a submodule.
However, a manuscript and the underlying analysis often follow different lifecycles and editing patterns, so they benefit from having distinct version histories.
*Note: For the purposes of this course, a single repository containing your Jupyter notebooks and analysis is sufficient.*

## Additional resources

* BibTeX to CFF Converter [https://www.bibtex.tools/bibtex-to-cff](https://www.bibtex.tools/bibtex-to-cff).
* See also the many available tools at [https://github.com/citation-file-format/citation-file-format/blob/main/README.md](https://github.com/citation-file-format/citation-file-format/blob/main/README.md#tools-to-work-with-citationcff-files-wrench).
