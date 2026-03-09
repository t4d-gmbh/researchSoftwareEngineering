# Environments 2.0

{% if slide %}

```{toctree}
:maxdepth: 1
:caption: Virtualized Environments

./containerEnv
./containerImplementation
./toolingSecurityDistribution
./vmEnv
./vmLimitsPitfalls
```

{% else %}

## Virtualized Environments

### Container

```{include} ./containerEnv.md
```
```{include} ./containerImplementation.md
```
```{include} ./apptainerRuntime.md
```
```{include} ./layeringFilesystems.md
```
```{include} ./toolingSecurityDistribution.md
```
```{include} ./limitationsPitfalls.md
```

### Virtual Machines

```{include} ./vmEnv.md
```
```{include} ./vmStorageState.md
```
```{include} ./vmOrchestrationSecurity.md
```
```{include} ./vmLimitsPitfalls.md
```

{% endif %}





