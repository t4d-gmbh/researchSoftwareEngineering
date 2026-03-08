## ✏️ Project Exercise 1 ✏️

```{epigraph}
{.centered}
**Separation of Concerns (SoC)**
```

```{epigraph}
{.centered}
*Recall:*
```

::::{grid} 2 2 4 4
:gutter: 2

:::{grid-item-card} 🌍 Environment
Machine-specific settings (`HF_HOME`, device map, CUDA cache, ...)
:::
:::{grid-item-card} ⚙️ Configuration
Model ID, LoRA hyperparameters, training arguments, paths, ...
:::
:::{grid-item-card} 🧠 Code
The actual logic: loading, tokenizing, training, saving.
:::
:::{grid-item-card} 💾 Data
What is raw, what is interim, what is a result?
:::
::::

{.centered}
Head over to the [HelloWorld](https://github.com/pSciComp/exoHelloWorld) repository and have a look at [`Project - Exo 1`](https://github.com/pSciComp/exoHelloWorld/blob/main/exercises/project/Exo_1.md).
