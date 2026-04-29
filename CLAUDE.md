# CLAUDE.md

Personal cheatsheet repo. The `cheat` bash script renders markdown cheats from this repo, with a GitHub README fallback.

## Adding a new cheat

- For a tool/plugin: drop `<name>.md` at the repo root (e.g. `gs.md`, `fzf.md`).
- To override or summarize a public repo's README: write `<author>/<repo>.md` (e.g. `mattpocock/skills.md`). Local always wins over the GitHub fetch.

Keep cheats tight — table of commands or a short list. Lead with the install/setup step. No marketing.

## Running the script

```bash
./cheat            # picker
./cheat <name>     # render local <name>.md
./cheat <a>/<b>    # local first, then GitHub README
```

## Lint

```bash
shellcheck cheat
```

## Don't

- Don't add packaging/release machinery — the install path is `git clone` + symlink.
- Don't render with `glow` or `mdcat`. `bat -l md` is intentional: cheatsheets are read for commands, not prose.
