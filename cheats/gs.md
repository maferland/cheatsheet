# gs — git-spice

Stacked branches and stacked PRs. Each branch sits on top of the one below; trunk is the base.

## Setup

```bash
gs repo init             # one-time per repo
gs auth login            # one-time per machine
```

## Daily flow

| Step | Command |
|---|---|
| Start a stacked branch | `gs b c <name>` |
| Commit | `gs c c -m "msg"` |
| Amend (auto-restacks upstack) | `gs c a` |
| Sync trunk + restack everything | `gs r s` |
| Submit current branch as PR | `gs b s` |
| Submit whole stack | `gs s s` |
| Submit stack as drafts | `gs s s --draft` |
| Auto-fill PR title/body | add `--fill` |

## Navigation

| Command | Meaning |
|---|---|
| `gs up` / `gs down` | one branch up / down |
| `gs top` / `gs bottom` | top / bottom of stack |
| `gs trunk` | back to main |
| `gs b co <name>` | checkout by name |

## Visualize

```bash
gs l s         # short log: branches + status
gs l l         # long log: branches + commits
gs l s -a      # all stacks
```

## Restack

| When | Command |
|---|---|
| Current branch only | `gs branch restack` |
| Current + upstack | `gs us r` |
| Whole stack | `gs s r` |
| Every tracked branch | `gs repo restack` |

## Manipulate

```bash
gs branch fold           # merge into base (collapse)
gs branch squash         # squash branch into one commit
gs branch onto <other>   # move branch onto a different base
gs us onto <other>       # move branch + upstack
gs branch rename <name>
gs branch delete <name>
gs branch track          # adopt an existing branch
```

## Rebase recovery

```bash
gs rebase continue       # gs rb c
gs rebase abort
```

## Headless flags

- `gs --no-prompt` for CI
- `gs b s --no-publish` push only, no PR
- `gs b s --update-only` update PR, don't create new

## Worktree gotcha

`gs trunk` / `gs b c` fail if trunk is checked out elsewhere. Bare-repo pattern avoids it: no worktree owns trunk.

```bash
mv .git .bare
echo "gitdir: ./.bare" > .git
git -C .bare config core.bare true
```

## Pitfalls

- `gs repo init` must run first — nothing tracks until then.
- `gs c a` auto-restacks the upstack. Don't run `gs us r` after.
- `gs r s` pulls trunk **and** restacks all tracked branches.
- `gs b c <name>` checks out the new branch (unlike `git branch`).
- `gs b s` updates the existing PR — no duplicates.
- `gs branch edit`, `gs commit split`, `gs r i` are interactive — not headless-safe.

Upstream: <https://abhinav.github.io/git-spice/>
