# Commitment

Commitment is a very simple shell-based Git hook runner.

This provides a single script `commitments` that can be linked into a Git `hooks` directory to invoke actual hook functions
written as shell functions in plugin scripts.

## Adding/Removing a Hook

Adding a hook is easy, the `install` script in this directory takes the name of a Git hook and will add a symlink to the
`commitments` script with that name so that it will be called for that hook.

``` bash
❯ install pre-commit
```


This installs a *global* hook, i.e. installed in the Git configured global hook directory. This can be done explicitly by
adding the keyword `global` before the hook name in the command above. Similarly it is possible to install a *local* hook
into a specific git repository using the `local` keyword, as shown below.

``` bash
❯ install local pre-commit
```

Removing an installed hook is easy, you prepend the command you used above, whether for a local or global hook, with the
keyword `remove`.

``` bash
❯ install remove local pre-commit
```

## Plugin Path

Plugins are loaded by searching a path environment variable, `CMT_PLUGIN_PATH`. Each entry in the path is a directory
that contains a set of plugins (see next section for the structure of a plugin).

The installer will try and create and `env` file in the `commitments` directory of your local config folder, using
the environment variable `XDG_CONFIG_HOME`. This contains the basic configuration with a path to the standard plugin folder.

```bash
export CMT_PLUGIN_PATH=/path/to/commitments/plugins
```

## Repository `.commitments` file

TBD

## Writing a Plugin

TBD

### The `enabled` Function

```bash
rust_enabled() {
    local repo_root=$1
    log_trace "Looking for ${repo_root}/Cargo.toml to enable Rust plugin"
    test -f ${repo_root}/Cargo.toml
}
```

### A Hook Function

```bash
rust_pre_commit() {
    local repo_root=$1
}
```

## Change Log

TBD

