# kubernetes-info

> Exposes Kubernetes context related information for inclusion in the shell prompt

## Functions

- `kubernetes-info` exposes information about the Kubernetes context that one is
operating in inside of an associative array. The available keys:
  - `context`
    - `.contexts.current-context` from `kubectl config view -ojson`
    - You can change the name that this displays on the prompt using `kubectl
    config rename-context OLD_CONTEXT_NAME NEW_CONTEXT_NAME`
  - `namespace`
    - `.contexts[].context.namespace` from `kubectl config view -ojson` for the
    context that matches the current context

## Adding it to your prompt

All the keys in the associative array can be formatted.

```sh
# %C => current context
zstyle ':prezto:module:kubernetes:info:context' format ' k8s:%C'
# %N => current namespace
zstyle ':prezto:module:kubernetes:info:namespace' format ' k8s:%N'
```

You can now add `$kubernetes_info[context]` (and other supported keys) to
`$PROMPT`.

**Note:** You _must_ call the `kubernetes-info` function in the
`prompt_name_precmd` hook function

## Note about Usage

- This Prezto module will not work if `kubectl` is installed through `gcloud components`. You must
  install `kubectl` and keep the directory in a place where zsh knows about it and can load it into
  the `$+commands` map. This map is checked to ensure that kubectl exists before this module is
  loaded. If `kubectl` is installed through `gcloud components`, then the binary is loaded into the
  `$PATH` dynamically thourgh `/.../google-cloud-sdk/path.zsh.inc`, which probably happens _after_
  the prompt is built.

### Authors

- [Siddharth Kannan](https://github.com/icyflame)
