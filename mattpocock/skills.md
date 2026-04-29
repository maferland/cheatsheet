# mattpocock/skills

Claude Code skills for real engineering. Small, composable, model-agnostic.

## Install

```bash
npx skills@latest add mattpocock/skills
```

Pick the skills you want and which agents (Claude Code, Codex, etc.) to install them on.

## Skills

### Engineering
| Skill | Use when |
|---|---|
| `diagnose` | Hard bugs or perf regressions. Reproduce → minimise → hypothesise → instrument → fix → regression-test. |
| `tdd` | Build a feature or fix a bug test-first. Red-green-refactor loop. |
| `github-triage` | Working through incoming issues; label-based state machine. |
| `to-prd` | Turn the current conversation into a PRD as a GitHub issue. |
| `to-issues` | Break a plan/PRD into vertical-slice GitHub issues. |
| `grill-with-docs` | Stress-test a plan against `CONTEXT.md` + ADRs; updates docs inline. |
| `improve-codebase-architecture` | Find refactoring opportunities; informed by `CONTEXT.md` + ADRs. |
| `zoom-out` | Get higher-level context on unfamiliar code. |

### Misc
| Skill | Use when |
|---|---|
| `git-guardrails-claude-code` | Block dangerous git commands (push, reset --hard, branch -D, …) via hooks. |
| `setup-pre-commit` | Husky + lint-staged + typecheck + tests on commit. |
| `migrate-to-shoehorn` | Replace test `as` casts with `@total-typescript/shoehorn`. |
| `scaffold-exercises` | New exercise dirs (sections/problems/solutions/explainers). |

### Productivity
| Skill | Use when |
|---|---|
| `caveman` | Ultra-compressed responses (~75% fewer tokens). Trigger: "caveman mode". |
| `grill-me` | Get interviewed on a plan until decisions are resolved. |
| `write-a-skill` | Author a new skill with proper structure + progressive disclosure. |

### Personal
| Skill | Use when |
|---|---|
| `edit-article` | Restructure + tighten article drafts. |
| `obsidian-vault` | Search/create/manage Obsidian notes with wikilinks + index notes. |

## Notes

- Most skills auto-trigger on intent ("diagnose this", "TDD this"). A few are opt-in only (`grill-with-docs`, `zoom-out` set `disable-model-invocation: true`).
- `CONTEXT.md` (project domain language) and `docs/adr/` (decision records) feed several engineering skills — worth setting up first.

Upstream: <https://github.com/mattpocock/skills>
