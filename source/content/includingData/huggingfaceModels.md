## Managing Hugging Face Models

{% if slide %}

::::{grid}
:gutter: 2

:::{grid-item}
:class: sd-m-auto

**Treat models exactly like large datasets:**
- **Pin your versions**: Models update; always link a specific revision/commit.
- **Control your cache**: Point downloads to fast local storage, not network drives.
- **Separate adapters**: Save tiny LoRA weights, not entire base models.
:::
:::{grid-item-card} Referring to Models
:class: sd-m-auto

{% else %}

In modern machine learning, pre-trained models (like LLMs or vision models) are essentially massive, complex data artifacts.
Just like raw datasets, the models should be strictly versioned and efficiently managed — especially when running on cluster infrastructures. 


The [Hugging Face Hub](https://huggingface.co/) is _de facto_ standard for hosting these models.
However, naively downloading models can quickly exhaust storage and ruin reproducibility.

### Referring to Models

{% endif %}
{% if slide %}

Never just write: *"We used Llama-3."*
- Use the **exact repository ID**: `meta-llama/Meta-Llama-3-8B`
- Always **specify the `revision`** (commit SHA or tag).

:::
::::

{% else %}

A common reproducibility failure is vaguely stating the model used (e.g., *"We used Mistral 7B"*).
Model repositories are updated frequently to fix bugs or remove toxic data. 

To ensure exact reproducibility define:
1. **The exact Model ID**: e.g., `mistralai/Mistral-7B-v0.1`
2. **The exact Revision**: A Git commit SHA or branch tag (e.g., `revision="26bca36b..."`).

By hardcoding the model ID and the commit hash in configuration files (e.g. `config.yaml`), anyone running the code will pull the exact identical weights.

{% endif %}

### Downloading and Storing Snapshots

{% if slide %}

::::{grid} 1 2 2 2
:gutter: 2

:::{grid-item}
:class: sd-m-auto

**Control download location:**
```python
from huggingface_hub import snapshot_download

# Download exactly what you need to a specific folder
path = snapshot_download(
    repo_id="mistralai/Mistral-7B-v0.1",
    revision="26bca36b...",
    local_dir="data/raw/models/mistral"
)
```
:::
{% else %}

By default, Hugging Face libraries download massive files to a hidden cache folder in your home directory (`~/.cache/huggingface/`). **On a High-Performance Computing (HPC) cluster, this is often a disaster**, as home directories have strict quotas and slow network drives.

**Best Practice 1: Environment Variables**
When deploying to a cluster, always set the `HF_HOME` environment variable to point to your fast, high-capacity scratch space.

```bash
export HF_HOME=/scratch/your_username/hf_cache
uv run python scripts/train.py
```

**Best Practice 2: Explicit Local Snapshots**
Alternatively, use the `huggingface_hub` Python library to explicitly download the required files directly into your project's `data/models/` directory before running heavy computations:

```python
from huggingface_hub import snapshot_download

model_path = snapshot_download(
    repo_id="mistralai/Mistral-7B-v0.1",
    revision="26bca36b...", # Pin the version!
    local_dir="data/models/mistral_7b", # Save locally
    ignore_patterns=["*.msgpack", "*.h5"] # Only download PyTorch/Safetensors
)
```

### Storing Adaptations (Fine-Tuning)
{% endif %}


{% if slide %}
:::{grid-item-card} Storing Adaptations (Fine-Tuning)
:class: sd-m-auto

Do not duplicate base models!

* Fine-tuning a 15GB model creates another 15GB model.
* With PEFT / LoRA save only the adapter weights (~50MB).
* Track these small adapters with standard Git or DVC.

:::
::::

:::{admonition} Cluster Tip:
:class: tip
Set the `HF_HOME` environment variable to point to `$SCRATCH` or `$TMPDIR` to avoid crashing shared network drives!

_Just be aware that the data will be purged!_
:::

{% else %}

If your project involves fine-tuning a model, you face a storage problem: fine-tuning a 15GB model normally results in a brand-new 15GB model. Saving multiple checkpoints will instantly fill your hard drive.

**Use Parameter-Efficient Fine-Tuning (PEFT)**
Instead of training the whole model, use techniques like **LoRA (Low-Rank Adaptation)**. LoRA freezes the original base model and only trains a tiny set of new adapter weights.

* The base model remains untouched (and downloaded via Hugging Face).
* Your fine-tuned adaptation is saved as a tiny folder containing a few megabytes of adapter weights (e.g., `adapter_config.json` and `adapter_model.safetensors`).

:::{admonition} Versioning Adapters
:class: tip
Because LoRA adapters are usually under 100MB, you can often version them directly in Git alongside your code (e.g., in `data/models/my_lora_v1/`), or easily track them via DVC without needing massive cloud storage quotas.
:::

{% endif %}
