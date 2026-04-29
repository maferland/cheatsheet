# CLAUDE.md

Personal cheatsheet repo. The `cheat` bash script renders markdown cheats from this repo, with a GitHub README fallback.

## Adding a new cheat

All cheats live under `cheats/`. Repo metadata (`README.md`, `CLAUDE.md`, `LICENSE`, `.github/`) stays at the root.

- For a tool/plugin: `cheats/<name>.md` (e.g. `cheats/gs.md`, `cheats/fzf.md`).
- To override or summarize a public repo's README: `cheats/<author>/<repo>.md` (e.g. `cheats/mattpocock/skills.md`). Local always wins over the GitHub fetch.
- For multi-page cheats: pair `cheats/<path>.md` (index) with `cheats/<path>/<sub>.md` (sub-pages). `cheat <path>` opens fzf over the index + sub-pages; `cheat <path>/<sub>` jumps straight in.

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
