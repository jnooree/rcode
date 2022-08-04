# rcode

## Introduction

`rcode` is a `code` command line of [Visual Studio Code](https://github.com/microsoft/vscode) for ssh sessions.

## Basic Usage

If path is not specified, `rcode` will open the current directory as default.
To read from stdin, supply `-` to `rcode`.

```txt
Usage: rcode [-nrwcigf] [PATHS...]

Options forwarded to `code` executable:
    -n: Force to open a new window.
    -r: Force to open a file or folder in an already opened window.
    -w: Wait for the files to be closed before returning.

Options for convenience:
    -c: Change to the root of the workspace after opening the files.
    -i: Create a .code-workspace file for the workspace if it doesn't exist.
    -g: Run `git init` if the workspace is not a git repository.
    -f: Run `git fetch` if the workspace is a git repository.
```

## Prerequisite

- `code` command line must be installed in your `$PATH`.
- Both local and remote machines must be accessible over SSH.

## Configuration

`rcode` need the following environment variables.

- `RCODE_REMOTE`: The target remote server. Supplied to `code` in the following format:

  ```bash
  code --<file|folder>-uri "vscode-remote://ssh-remote+${RCODE_REMOTE}/path/to/<file|folder>"
  ```

- `LC_HOSTNAME`: The local host to be connected via ssh. `rcode` will use it in the following command (issued in the remote host):

  ```bash
  ssh "${LC_HOSTNAME}" -T "code ..."
  ```

  It is recommended to be set via `SetEnv` section in the `~/.ssh/config` file.

  ```ssh_config
  Host *
    SetEnv LC_HOSTNAME=<local hostname>
  ```

## License and Disclaimer

The [MIT License](LICENSE).
