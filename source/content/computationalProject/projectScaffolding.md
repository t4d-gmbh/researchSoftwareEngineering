## Project Scaffolding

{% if page %}
A fundamental step toward following best practices in any data or software project is to start with a well-structured layout.
This presents a consistent project architecture that is applicable to wide range of projects, from simple analytical pipelines to robust software packages.

Naturally, the exact specifics will shift depending on the subject matter, the technologies used, and the overall purpose of the work.
However, there is a golden rule to maintain sanity and collaboration: **the root of a repository should always look the same.**

Adhering to a standardized root directory structure reduces friction.
It facilitates a faster setup, makes the codebase instantly recognizable to collaborators, and allows anyone to quickly orient themselves without getting lost in a maze of arbitrarily named folders. 

We suggest adopting the following structure for the root folder, commonly referred to as the **Project Scaffolding**.
{% endif %}


:::{raw} html
:file: ./../_static/projectScaffoldingStyle.html
:::

:::{raw} html

<input type="radio" name="tree-nav" id="radio-root" class="tree-radio" checked>
<input type="radio" name="tree-nav" id="radio-readme" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-pyproj" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-reqs" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-git" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-gitlab" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-github" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-env" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-env-example" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-ai" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-license" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-citation" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-contrib" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-codeofconduct" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-data" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-data-readme" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-data-raw" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-data-interim" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-data-final" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-scripts" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-scripts-drafts" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-notebooks" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-notebooks-drafts" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-config" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-src" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-mypkg" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-results" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-tests" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-tests-unit" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-tests-integration" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-tests-file" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-examples" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-docs" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-bench" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-github-workflows" class="tree-radio">

<div class="scaffold-split">
  <div class="tree-pane project-tree">
    
    <details open>
      <summary><label for="radio-root">myProject/</label></summary>
      <ul>
        <li>📄 <label for="radio-readme">README.md</label></li>
        <li>📄 <label for="radio-pyproj">pyproject.toml <span class="context-badge">🔸</span></label></li>
        <li>📄 <label for="radio-git">.gitignore</label></li>
        <li>📄 <label for="radio-env">.env</label></li>
        <li>📄 <label for="radio-env-example">.env.example</label></li>
        <li>📄 <label for="radio-ai">AI_USAGE.md</label></li>
        <li>📄 <label for="radio-license">LICENCE</label></li>
        <li>📄 <label for="radio-citation">CITATION.cff</label></li>
        <li>📄 <label for="radio-contrib">CONTRIBUTING.md</label></li>
        <li>📄 <label for="radio-codeofconduct">CODE_OF_CONDUCT.md</label></li>
        <li>📄 <label for="radio-gitlab">.gitlab-ci.yaml<span class="context-badge">🔸</span></label></li>
        <li>
          <details>
            <summary><label for="radio-data">data/</label></summary>
            <ul>
                <li>📄 <label for="radio-data-readme">README.md</label></li>
                <li>📂 <label for="radio-data-raw">raw/</label></li>
                <li>📂 <label for="radio-data-interim">interim/</label></li>
                <li>📂 <label for="radio-data-final">final/</label></li>
            </ul>
          </details>
        </li>
        <li>
          <details>
            <summary><label for="radio-scripts">scripts/</label></summary>
            <ul>
                <li>📂 <label for="radio-scripts-drafts">drafts/</label></li>
            </ul>
          </details>
        </li>
        <li>
          <details>
            <summary><label for="radio-notebooks">notebooks/</label></summary>
            <ul>
                <li>📂 <label for="radio-notebooks-drafts">drafts/</label></li>
            </ul>
          </details>
        </li>
        <li>📂 <label for="radio-config">config/</label></li>
        <li>
          <details>
            <summary><label for="radio-src">src/ <span class="context-badge">🔸</span></label></summary>
            <ul>
                <li>📂 <label for="radio-mypkg">mypks/</label></li>
            </ul>
          </details>
        </li>
        <li>📂 <label for="radio-results">results/</label></li>
        <li>
          <details>
            <summary><label for="radio-tests">tests/</label></summary>
            <ul>
                <li>📂 <label for="radio-tests-unit">unit/</label></li>
                <li>📂 <label for="radio-tests-integration">integration/</label></li>
                <li>📄 <label for="radio-tests-file">test_mypkg.py</label></li>
            </ul>
          </details>
        </li>
        <li>📂 <label for="radio-examples">examples/</label></li>
        <li>📂 <label for="radio-docs">docs/</label></li>
        <li>📂 <label for="radio-bench">benchmark/</label></li>
        <li>
          <details>
            <summary><label for="radio-github">.github/ <span class="context-badge">🔸</span></label></summary>
            <ul>
                <li>📂 <label for="radio-github-workflows">workflows/</label></li>
            </ul>
          </details>
        </li>
      </ul>
    </details>
    
  </div>

  <div class="desc-pane">
    <div id="desc-root" class="desc-item">
      <h3>🏠 Project Root</h3>
      <p>The root folder of a project should <b>only contain generic files and foldernames</b>.</p>
      {% if page %}
      <p><i>Select a file or folder to read more about its purpose and content</i></p>
      <p><i>Click on the 📁 signs to expand a folder.</i></p>
      <p><i>A 🔸 indicates a specific context in which the element is relevant.</i></p>
      {% endif %}
    </div>
    <div id="desc-readme" class="desc-item">
      <h3>📖 README.md</h3>
      <p>The front page of a repository.<br>It should serve as <b>nexus for all metadata related to a project</b>.</p>
      {% if page %}
        <p>Especially for bigger projects this also means that the `README.md` might **not** contain all metadata directly, but links and instructions on how to find all metadata.</p>
      {% endif %}
    </div>
    <div id="desc-pyproj" class="desc-item">
      <span class="context-label">🔸 python</span>
      <h3>📦 pyproject.toml</h3>
      <p>The modern standard for defining build systems, dependencies, and tool settings (like <code>ruff</code>, <code>pytest</code>, or <code>black</code>).</p>
    </div>
    <div id="desc-env-example" class="desc-item">
      <h3>📄 .env.example</h3>
      <p>A safe template for the <code>.env</code> file. Unlike the actual <code>.env</code> file, this template <b>must</b> be committed to version control.</p>
      {% if page %}
      <p>It provides empty or safe default values to demonstrate exactly which environment variables a collaborator needs to define on their own system to execute the project successfully.</p>
      <p>A minimal example of its contents:</p>
      <pre><code class="language-bash">
# Define the absolute path to the local data directory
RAW_DATA_DIR=/absolute/path/to/local/data/

# Provide the API key for external service access
EXTERNAL_API_KEY=&lt;insert_api_key_here&gt;
      </code></pre>
      {% endif %}
    </div>
    <div id="desc-git" class="desc-item">
      <h3>🙈 .gitignore</h3>
      <p>Specifies intentionally untracked files that Git should ignore (e.g., <code>.env</code>, <code>__pycache__</code>, local data, build artifacts).</p>
    </div>
    <div id="desc-env" class="desc-item">
      <h3>🔐 .env</h3>
      <p>Local environment variables and secrets (such as API keys, database passwords, and personal access tokens). <b>This file should never be added to version control.</b> It should be strictly ignored by Git to prevent leaking sensitive security credentials.</p>
      <p>We recommend to add the <code>.env</code> file to <code>.gitignore</code> and provide a <code>.env.example</code> file along with a repository so to document how exactly the <code>.env</code> file should be structured.</p>
    </div>
    <div id="desc-gitlab" class="desc-item">
      <span class="context-label">🔸 GitLab</span>
      <h3>⚙️ .gitlab-ci.yaml</h3>
      <p>The CI/CD pipeline definition for GitLab. It declares stages, jobs, and rules that automatically run tests, build artifacts, and deploy your project whenever changes are pushed to the repository.</p>
      {% if page %}
      <p>A single YAML file at the repository root controls the entire automation pipeline. Each job specifies a Docker image, a script to execute, and the conditions under which it should run. GitLab Runner picks up these jobs and executes them in isolated containers.</p>
      {% endif %}
    </div>
    <div id="desc-github" class="desc-item">
      <span class="context-label">🔸 GitHub</span>
      <h3>⚙️ .github/</h3>
      <p>The hidden configuration directory for GitHub-specific features: CI/CD workflows, issue templates, pull request guidelines, and more.</p>
    </div>
    <div id="desc-github-workflows" class="desc-item">
      <span class="context-label">🔸 GitHub</span>
      <h3>⚙️ workflows/</h3>
      <p>GitHub Actions workflow files (YAML) that define automated CI/CD pipelines. Each file describes a workflow triggered by events such as pushes, pull requests, or scheduled runs to test, build, and deploy your project.</p>
      {% if page %}
      <p>Unlike GitLab's single-file approach, GitHub Actions uses one YAML file per workflow inside this directory, making it straightforward to maintain separate pipelines for testing, releasing, and documentation deployment.</p>
      {% endif %}
    </div>
    <div id="desc-ai" class="desc-item">
      <h3>🤖 AI_USAGE.md</h3>
      <p>Transparency document detailing how LLMs were used in the creation of code or documentation.</p>
    </div>
    <div id="desc-license" class="desc-item">
      <h3>⚖️ LICENSE</h3>
      <p>The legal framework for a project. It explicitly defines how others can use, modify, and distribute the code and data. Even for internal or proprietary projects, having a clear license is essential.</p>
    </div>
    <div id="desc-citation" class="desc-item">
      <h3>📝 CITATION.cff</h3>
      <p>Plain text YAML file specifying how this project should be cited.</p>
      {% if page %}
      <p>This should be a plain text file with machine-readable citation information.</p>
      <p>A minimalistic example of what this file looks like:</p>
      <pre><code class="language-yaml">
cff-version: 1.2.0
message: "If you use this software, please cite it using these metadata."
authors:
  - family-names: "Lisa"
    given-names: "Mona"
    orcid: "https://orcid.org/xxxx-xxxx-xxxx-xxxx
title: "My Awesome Research"
doi: <the-doi>
      </code></pre>
      <p>For more details visit the <a href="https://github.com/citation-file-format/citation-file-format/blob/main/README.md">cff-format</a> documentation.</p>
      {% endif %}
    </div>
    <div id="desc-contrib" class="desc-item">
      <h3>🤝 CONTRIBUTING.md</h3>
      <p>The onboarding guide for new developers. It outlines the step-by-step process for submitting bug reports, requesting features, and creating pull requests (PRs) that adhere to the project's standards.</p>
    </div>
    <div id="desc-codeofconduct" class="desc-item">
      <h3>🛡️ CODE_OF_CONDUCT.md</h3>
      <p>Establishes the community standards and expected behavior for everyone interacting with the project. It helps ensure a welcoming, inclusive, and professional environment for all contributors.</p>
    </div>
    <div id="desc-data" class="desc-item">
      <h3>📊 Data</h3>
      <p>The root data directory. We use a strict data pipeline separating raw inputs from processed outputs. Expand the folder and select a subfolder on the left to learn more about its specific rules.</p>
    </div>
    <div id="desc-data-readme" class="desc-item">
      <h3>📖 README.md</h3>
      <p>Information specific to the data related to this project.</p>
    </div>
    <div id="desc-data-raw" class="desc-item">
      <h3>📁 raw/</h3>
      <p>Immutable, original data. <b>Do not edit these files.</b> <i>(Note: This also includes pointers/URL links to large external datasets that cannot be stored directly in Git.)</i></p>
    </div>
    <div id="desc-data-interim" class="desc-item">
      <h3>📁 interim/</h3>
      <p>Intermediate data that has been cleaned or transformed, but is not yet ready for final analysis.</p>
    </div>
    <div id="desc-data-final" class="desc-item">
      <h3>📁 final/</h3>
      <p>Final, processed datasets ready for modeling, publication, or deployment.</p>
    </div>
    <div id="desc-scripts" class="desc-item">
      <h3>🚀 Scripts</h3>
      <p>Executable scripts, job launchers, or data preprocessing entry points. These should generally be runnable from the command line.</p>
    </div>
    <div id="desc-scripts-drafts" class="desc-item">
      <h3>📁 drafts/</h3>
      <p>A scratchpad folder for experimental scripts that are not yet production-ready or integrated into the main workflow.</p>
    </div>
    <div id="desc-notebooks" class="desc-item">
      <span class="context-label">🔸 Python/R</span>
      <h3>📓 Notebooks</h3>
      <p>Jupyter notebooks for exploratory data analysis (EDA), prototyping, and interactive visualization.</p>
    </div>
    <div id="desc-notebooks-drafts" class="desc-item">
      <span class="context-label">🔸 Python/R</span>
      <h3>📁 drafts/</h3>
      <p>A scratchpad folder for experimental notebooks that are not yet production-ready or integrated into the main workflow.</p>
    </div>
    <div id="desc-config" class="desc-item">
      <h3>⚙️ Configuration</h3>
      <p>Centralized YAML/TOML files for parameters. This allows changing experiments without modifying code.</p>
    </div>
    <div id="desc-src" class="desc-item">
      <span class="context-label">🔸 python</span>
      <h3>💻 Source Code (src/)</h3>
      <p>Location for all reusable and installable code.</p>
    </div>
    <div id="desc-mypkg" class="desc-item">
      <h3>📁 mypkg/</h3>
      <p>A particular package containing functions, and business logic.</p>
    </div>
    <div id="desc-results" class="desc-item">
      <h3>📈 results/</h3>
      <p>A dedicated directory for the final outputs of of a project. If the project involves data analysis, research, or machine learning, this folder holds the generated artifacts such as figures, summary tables, trained models, and compiled reports.</p>
    </div>
    <div id="desc-tests" class="desc-item">
      <h3>🧪 Testing Suite</h3>
      <p>Ensures code reliability via automated testing. A well-structured test suite separates individual component tests from full workflow tests.</p>
    </div>
    <div id="desc-tests-unit" class="desc-item">
      <h3>📁 unit/</h3>
      <p>Directory for unit tests. These tests are designed to verify that individual functions, classes, or methods operate correctly in strict isolation.</p>
    </div>
    <div id="desc-tests-integration" class="desc-item">
      <h3>📁 integration/</h3>
      <p>Directory for integration tests. These tests verify that multiple modules, databases, or external services function together properly as a unified system.</p>
    </div>
    <div id="desc-tests-file" class="desc-item">
      <span class="context-label">🔸 python</span>
      <h3>📄 test_mypkg.py</h3>
      <p>A standard Python test file (often utilizing <code>pytest</code>). This file contains specific test cases and assertions designed to validate the functionality of the associated <code>mypkg</code> module.</p>
    </div>
    <div id="desc-examples" class="desc-item">
      <h3>💡 Examples</h3>
      <p>Minimal, end-to-end usage demos to help new users get started quickly.</p>
    </div>
    <div id="desc-docs" class="desc-item">
      <h3>📖 Documentation</h3>
      <p>Contains extended documentation specific content, like an online documentation (e.g., with Sphinx or MKDocs).</p>
    </div>
    <div id="desc-bench" class="desc-item">
      <h3>⏱️ Benchmarks</h3>
      <p>Performance tracking scripts to measure execution time, memory usage, and scaling.</p>
    </div>
  </div>
</div>
:::
