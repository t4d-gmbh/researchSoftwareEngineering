# Virtualized Environments

{% if slide %}

```{toctree}
:maxdepth: 1

./containerEnv
./toolingSecurityDistribution
./vmEnv
./vmLimitsPitfalls
```

{% else %}

## Container

```{include} ./containerEnv.md
```
```{include} ./layeringFilesystems.md
```
```{include} ./toolingSecurityDistribution.md
```
```{include} ./limitationsPitfalls.md
```

## Virtual Machines

```{include} ./vmEnv.md
```
```{include} ./vmStorageState.md
```
```{include} ./vmOrchestrationSecurity.md
```
```{include} ./vmLimitsPitfalls.md
```

{% endif %}




