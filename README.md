# Dotbot `pacaur` Plugin

Plugin for [dotbot](https://github.com/anishathalye/dotbot) that adds a `pacaur`
directive. It allows installation of packeges using `pacaur`, and by extension
`pacman`, packages.

This plugin was based off of the [apt-get plugin](https://github.com/rubenvereecken/dotbot-apt-get) and [brew plugin](https://github.com/d12frosted/dotbot-brew).

## Installation

Add it as a submodule of your dotfiles repository.

```bash
git submodule add https://github.com/ajlende/dotbot-pacaur
```

## Usage

One option is having your packages list in a separate file. This way you can
run it separately from your main configuration.

```bash
./install -p dotbot-pacaur/pacaur.py -c packages.conf.yaml
```

Example of the `packages.conf.yaml`:

```yaml
- pacaur:
  - zsh
  - neovim
  - atom-editor
  - gitkraken
```

## Alternative Usage

Alternatively, you can add the directive directly in `install.conf.yaml` and
modify your `install` script so it automatically enables the `pacaur` plugin.

```bash
"${BASEDIR}/${DOTBOT_DIR}/${DOTBOT_BIN}" -d "${BASEDIR}" -c "${CONFIG}" \
  --plugin-dir "${BASEDIR}/dotbot-pacaur" "${@}"
```
