## Project Scaffolding

<!-- NOTE: This presents a consisten project structure that should be applicable to most projects, including software packages -->
<!-- NOTE: Golden rule: The root of a repository always looks the same (i.e. contains the same files and folders. -->
<!-- NOTE: We suggest to following structure of the root folder, aka. the Project scaffolding: -->


:::{raw} html
:file: ./../_static/projectScaffoldingStyle.html
:::

:::{raw} html

<input type="radio" name="tree-nav" id="radio-root" class="tree-radio" checked>
<input type="radio" name="tree-nav" id="radio-readme" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-pyproj" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-reqs" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-git" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-ai" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-licence" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-citation" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-contrib" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-codeofconduct" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-data" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-data-raw" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-data-interim" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-data-results" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-scripts" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-scripts-drafts" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-notebooks" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-config" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-src" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-tests" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-examples" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-docs" class="tree-radio">
<input type="radio" name="tree-nav" id="radio-bench" class="tree-radio">

<div class="scaffold-split">
  <div class="tree-pane project-tree">
    
    <details open>
      <summary><label for="radio-root">myProject/</label></summary>
      <ul>
        <li>📄 <label for="radio-readme">README.md</label></li>
        <li>📄 <label for="radio-pyproj">pyproject.toml</label></li>
        <li>📄 <label for="radio-reqs">requirements.txt</label></li>
        <li>📄 <label for="radio-git">.gitignore</label></li>
        <li>📄 <label for="radio-ai">AI_USAGE.md</label></li>
        <li>📄 <label for="radio-licence">LICENCE</label></li>
        <li>📄 <label for="radio-citation">CITATION.cff</label></li>
        <li>📄 <label for="radio-contrib">CONTRIBUTING.md</label></li>
        <li>📄 <label for="radio-codeofconduct">CODE_OF_CONDUCT.md</label></li>
        <li>
          <details>
            <summary><label for="radio-data">data/</label></summary>
            <ul>
                <li>📁 <label for="radio-data-raw">raw/</label></li>
                <li>📁 <label for="radio-data-interim">interim/</label></li>
                <li>📁 <label for="radio-data-results">results/</label></li>
            </ul>
          </details>
        </li>
        <li>
          <details>
            <summary><label for="radio-scripts">scripts/</label></summary>
            <ul>
                <li>📁 <label for="radio-scripts-drafts">drafts/</label></li>
                <li>📄 run_sims.py</li>
            </ul>
          </details>
        </li>
        <li>
          <details>
            <summary><label for="radio-notebooks">notebooks/</label></summary>
            <ul><li>01_intro.ipynb</li></ul>
          </details>
        </li>
        <li>
          <details>
            <summary><label for="radio-config">config/</label></summary>
            <ul><li>default.yaml</li></ul>
          </details>
        </li>
        <li>
          <details>
            <summary><label for="radio-src">src/</label></summary>
            <ul><li>📁 mypkg/</li></ul>
          </details>
        </li>
        <li>
          <details>
            <summary><label for="radio-tests">tests/</label></summary>
            <ul><li>🧪 unit/</li><li>🧪 integration/</li></ul>
          </details>
        </li>
        <li>📂 <label for="radio-examples">examples/</label></li>
        <li>
          <details>
            <summary><label for="radio-docs">docs/</label></summary>
            <ul><li>📄 conf.py</li><li>📄 index.rst</li></ul>
          </details>
        </li>
        <li>📂 <label for="radio-bench">benchmark/</label></li>
      </ul>
    </details>
    
  </div>

  <div class="desc-pane">
    <div id="desc-root" class="desc-item">
      <h3>🏠 Project Root</h3>
      <p>The root folder of a project should only contain generic files and foldernames.</p>
      <p><i>Select a file or folder to read more about their purpose and content</i></p>
      <p><i>Click on the 📂 signs to expand a folder.</i></p>
    </div>
    <div id="desc-readme" class="desc-item">
      <h3>📖 README.md</h3>
      <p>The front page of your repository. Provides the project overview, installation instructions, and quickstart examples.</p>
    </div>
    <div id="desc-pyproj" class="desc-item">
      <h3>📦 pyproject.toml</h3>
      <p>The modern standard for defining build systems, dependencies, and tool settings (like ruff, pytest, or black).</p>
    </div>
    <div id="desc-reqs" class="desc-item">
      <h3>📝 requirements.txt</h3>
      <p>A simple list of pip dependencies. While <code>pyproject.toml</code> is preferred for packages, this file is still highly useful for pinning exact dependency versions in isolated environments.</p>
    </div>
    <div id="desc-git" class="desc-item">
      <h3>🙈 .gitignore</h3>
      <p>Specifies intentionally untracked files that Git should ignore (e.g., <code>__pycache__</code>, local data, build artifacts).</p>
    </div>
    <div id="desc-ai" class="desc-item">
      <h3>🤖 AI_USAGE.md</h3>
      <p>Transparency document detailing how LLMs were used in the creation of code or documentation.</p>
    </div>
    <div id="desc-license" class="desc-item">
      <h3>🤖 LICENSE</h3>
      <p>.</p>
    </div>
    <div id="desc-citation" class="desc-item">
      <h3>CITATION.cff</h3>
      <p>.</p>
    </div>
    <div id="desc-contrib" class="desc-item">
      <h3>CONTRIBUTIONS</h3>
      <p>.</p>
    </div>
    <div id="desc-codeofconduct" class="desc-item">
      <h3>CODE_OF_CONDUCT.md</h3>
      <p>.</p>
    </div>
    <div id="desc-data" class="desc-item">
      <h3>📊 Data</h3>
      <p>The root data directory. We use a strict data pipeline separating raw inputs from processed outputs. Expand the folder and select a subfolder on the left to learn more about its specific rules.</p>
    </div>
    <div id="desc-data-raw" class="desc-item">
      <h3>📁 raw/</h3>
      <p>Immutable, original data. <b>Do not edit these files.</b> <i>(Note: This also includes pointers/URL links to large external datasets that cannot be stored directly in Git.)</i></p>
    </div>
    <div id="desc-data-interim" class="desc-item">
      <h3>📁 interim/</h3>
      <p>Intermediate data that has been cleaned or transformed, but is not yet ready for final analysis.</p>
    </div>
    <div id="desc-data-results" class="desc-item">
      <h3>📁 results/</h3>
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
      <h3>📓 Notebooks</h3>
      <p>Jupyter notebooks for exploratory data analysis (EDA), prototyping, and interactive visualization.</p>
    </div>
    <div id="desc-config" class="desc-item">
      <h3>⚙️ Configuration</h3>
      <p>Centralized YAML/TOML files for parameters. This allows changing experiments without modifying code.</p>
    </div>
    <div id="desc-src" class="desc-item">
      <h3>💻 Source Code (src/)</h3>
      <p>The "hearts and lungs" of the project. We use the <code>src/</code> layout to ensure the code is tested as an installed package.</p>
    </div>
    <div id="desc-tests" class="desc-item">
      <h3>🧪 Testing Suite</h3>
      <p>Ensures code reliability via unit tests (individual functions) and integration tests (full workflows).</p>
    </div>
    <div id="desc-examples" class="desc-item">
      <h3>💡 Examples</h3>
      <p>Minimal, end-to-end usage demos to help new users get started quickly.</p>
    </div>
    <div id="desc-docs" class="desc-item">
      <h3>📖 Documentation</h3>
      <p>Contains the Sphinx/MkDocs source files. This is where the website you are currently reading is generated from.</p>
    </div>
    <div id="desc-bench" class="desc-item">
      <h3>⏱️ Benchmarks</h3>
      <p>Performance tracking scripts to measure execution time, memory usage, and scaling.</p>
    </div>
  </div>
</div>
:::
