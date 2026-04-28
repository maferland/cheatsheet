# cheatsheet

Personal markdown cheat sheets for tools and plugins, browsable from the terminal.

## Install

```bash
ln -s "$PWD/cheat" ~/.local/bin/cheat
```

Requires `bat`, `fzf`, `gh` on PATH.

## Usage

```bash
cheat                    # fzf picker over all .md files in this repo
cheat <name>             # render <name>.md (picker if multiple matches)
cheat <author>/<repo>    # render local <author>/<repo>.md, or fetch the GitHub README
```

## Layout

Drop markdown files anywhere in the repo. Two conventions:

- `<name>.md` at repo root for personal notes (e.g. `git.md`, `fzf.md`)
- `<author>/<repo>.md` to override or annotate a public repo's README
