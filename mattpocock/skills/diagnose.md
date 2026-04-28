# diagnose

Disciplined diagnosis loop for hard bugs and perf regressions. Skip phases only when explicitly justified.

Trigger: "diagnose this" / "debug this" / bug report / something throwing or slow.

## The 6 phases

| # | Phase | Goal |
|---|---|---|
| 1 | Build a feedback loop | Fast, deterministic pass/fail signal **for the bug** |
| 2 | Reproduce | Confirm the loop produces the user's failure mode, not a nearby one |
| 3 | Hypothesise | 3–5 ranked, falsifiable hypotheses **before** testing any |
| 4 | Instrument | One probe per hypothesis. Tag debug logs `[DEBUG-xxxx]` |
| 5 | Fix + regression test | Test before fix, only if a correct seam exists |
| 6 | Cleanup + post-mortem | Remove probes; ask "what would have prevented this?" |

## Phase 1 is the skill

Everything else is mechanical. Spend disproportionate effort here. **Be aggressive. Be creative. Refuse to give up.**

### Loops to try, in rough order

1. Failing test at the right seam (unit / integration / e2e)
2. Curl / HTTP script vs running dev server
3. CLI invocation with fixture, diff stdout vs golden
4. Headless browser script (Playwright / Puppeteer)
5. Replay a captured trace (HAR, payload, event log)
6. Throwaway harness — minimal subset that hits the code path
7. Property / fuzz loop for "sometimes wrong"
8. Bisection harness for "appeared between X and Y"
9. Differential loop: same input, old vs new
10. HITL bash script — last resort

### Iterate on the loop itself

- Make it faster (cache setup, narrow scope)
- Make the signal sharper (assert on the symptom, not "didn't crash")
- Make it deterministic (pin time, seed RNG, isolate fs/network)

A 30s flaky loop is barely better than no loop. A 2s deterministic loop is a superpower.

### Non-deterministic bugs

Goal isn't a clean repro — it's a **higher reproduction rate**. Loop 100×, parallelise, narrow timing windows, inject sleeps. 50% flake → debuggable; 1% → not.

## Phase 3 — Hypothesise

Each hypothesis must be **falsifiable**:

> "If X is the cause, then changing Y will make it disappear / changing Z will make it worse."

Show the ranked list to the user before testing — they often re-rank instantly with domain knowledge.

## Phase 5 — Correct seam

A correct seam exercises the **real bug pattern** at the call site. If the only seam is too shallow, a regression test gives false confidence. **The absence of a correct seam is itself a finding.** Note it.

## Phase 6 — Cleanup checklist

- [ ] Original repro no longer reproduces (re-run loop)
- [ ] Regression test passes (or absence documented)
- [ ] All `[DEBUG-...]` probes removed (single grep)
- [ ] Throwaway prototypes deleted
- [ ] Correct hypothesis stated in the commit / PR

If the answer to "what would have prevented this?" involves architecture, hand off to `improve-codebase-architecture` **after** the fix.

Upstream: <https://github.com/mattpocock/skills/tree/main/skills/engineering/diagnose>
