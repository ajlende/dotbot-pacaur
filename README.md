# Dotbot `pacaur` Plugin

Plugin for [dotbot](https://github.com/anishathalye/dotbot) that adds a `pacaur` directive. It installs [official](https://www.archlinux.org/packages/) and [AUR](https://aur.archlinux.org/packages/) packages on Arch Linux with [`pacaur`](https://github.com/E5ten/pacaur).

This plugin will also attempt to install `pacaur` if not already installed which should make it easier when setting up a new computer.

## Installation

1. Add `dotbot-pacaur` as a submodule of your dotfiles.

    ```sh
    git submodule add https://github.com/ajlende/dotbot-pacaur
    ```

2. Add the `pacaur` directive to your `install.conf.yaml`.

    ```yaml
    - pacaur:
      - zsh
      - neovim
      - atom-editor-bin
      - gitkraken
    ```

3. Edit your `install` script to enable `dotbot-pacaur` plugin by modifying the last line with the `-p` option shown below.

    ```sh
    "${BASEDIR}/${DOTBOT_DIR}/${DOTBOT_BIN}" -d "${BASEDIR}" -c "${CONFIG}" \
      -p "${BASEDIR}/dotbot-pacaur/pacaur.py" "${@}"
    ```

## Other Usages

### Run Separately

If you want to run `dotbot-pacaur` separately from your main configuration, you can do so with the `-p` option and a `packages.conf.yaml` configuration that contains only the `pacaur` section from your `install.conf.yaml`.

```sh
dotbot/bin/dotbot -p dotbot-pacaur/pacaur.py -c packages.conf.yaml
```

### Alternative Directive Name

If you want to separate your official packages from your AUR packages, you can put them in a directive named `pacman`. Both directives are functionally the same (everything still gets installed with `pacaur`), but this may allow you to organize things a little more.

```yaml
- pacman:
  - zsh
  - neovim
- pacaur:
  - atom-editor-bin
  - gitkraken
```

## Basic Example

```sh
# ./install

#!/usr/bin/env bash

set -e

CONFIG="install.conf.yaml"
DOTBOT_DIR="dotbot"

DOTBOT_BIN="bin/dotbot"
BASEDIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

cd "${BASEDIR}"

(cd "${DOTBOT_DIR}" && git submodule update --init --recursive)
"${BASEDIR}/${DOTBOT_DIR}/${DOTBOT_BIN}" -d "${BASEDIR}" -c "${CONFIG}" "${@}"
```

```yaml
# ./install.conf.yaml

- defaults:
    link:
      relink: true

- clean: ['~']

- link:
    ~/.dotfiles: ''
    ~/.tmux.conf: tmux.conf
    ~/.vim: vim
    ~/.vimrc: vimrc

- shell:
  - [git submodule update --init --recursive, Installing submodules]

- pacaur:
  - zsh
  - neovim
  - atom-editor-bin
  - gitkraken
```

## Advanced Example

[My own dotfiles configuration](https://github.com/ajlende/dotfiles/tree/3f47be1e2ad898047644ebc39b2364cac50f2be8) shows an example of a more advanced usage, splitting up different sections into different files and swapping `dotbot-pacaur` for `dotbot-brew` on MacOS.
