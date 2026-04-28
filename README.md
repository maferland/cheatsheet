<div align="center">
<h1>🗒️ cheatsheet</h1>

<p>Browse personal markdown cheats from the terminal</p>
</div>

---

A tiny bash CLI that finds and renders markdown cheat sheets stored in this repo, with a GitHub README fallback when a local copy is missing.

## Prerequisites

- `bat` — markdown renderer
- `fzf` — picker
- `gh` — GitHub README fallback

```bash
brew install bat fzf gh
```

## Install

```bash
git clone https://github.com/maferland/cheatsheet.git ~/dev/cheatsheet
ln -s ~/dev/cheatsheet/cheat ~/.local/bin/cheat
```

Make sure `~/.local/bin` is on `PATH`.

## Usage

```bash
cheat                    # fzf picker over every .md in the repo
cheat <name>             # render <name>.md (picker if multiple matches)
cheat <author>/<repo>    # render local <author>/<repo>.md, or fetch the GitHub README
```

## Layout

Drop markdown files anywhere in the repo. Two conventions:

- `<name>.md` at the repo root for personal notes (e.g. `git.md`, `fzf.md`)
- `<author>/<repo>.md` to override or annotate a public repo's README

## License

[MIT](LICENSE)
