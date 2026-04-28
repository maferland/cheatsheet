# tdd

Test-driven development with a strict red-green-refactor loop. Trigger: "TDD this", "red-green-refactor", "test-first".

## Core principle

Tests verify behavior **through public interfaces**, not implementation details. Code can change entirely; tests shouldn't.

| Good test | Bad test |
|---|---|
| Exercises real code paths through public APIs | Mocks internal collaborators |
| Reads like a spec — "user can checkout with valid cart" | Tests private methods |
| Survives refactors | Breaks when you rename an internal function |
| Asserts via the interface | Asserts via the database directly |

Rename test: if you rename an internal function and tests fail, the tests were testing implementation, not behavior.

## Anti-pattern: horizontal slices

**DO NOT** write all tests first, then all implementation. That produces tests of *imagined* behavior — they pass when behavior breaks.

```
WRONG (horizontal):
  RED:   test1, test2, test3, test4, test5
  GREEN: impl1, impl2, impl3, impl4, impl5

RIGHT (vertical / tracer bullet):
  RED→GREEN: test1 → impl1
  RED→GREEN: test2 → impl2
  ...
```

One test → one impl → repeat. Each test responds to what you learned from the previous cycle.

## Workflow

### 1. Plan (with the user)

- [ ] Confirm interface changes
- [ ] Confirm which behaviors matter most (you can't test everything)
- [ ] List behaviors to test (not implementation steps)
- [ ] Get user approval

Ask: "What should the public interface look like? Which behaviors matter most?"

### 2. Tracer bullet

ONE test confirming ONE thing end-to-end.

```
RED:   write test for first behavior → fails
GREEN: minimal code to pass → passes
```

### 3. Incremental loop

For each remaining behavior:

```
RED:   next test → fails
GREEN: minimal code → passes
```

Rules:
- One test at a time
- Only enough code to pass the current test
- Don't anticipate future tests
- Stay on observable behavior

### 4. Refactor

After all tests pass:

- Extract duplication
- Deepen modules (small interface, deep impl)
- Apply SOLID where natural
- Run tests after each refactor step

**Never refactor while RED.** Get to GREEN first.

## Per-cycle checklist

- [ ] Test describes behavior, not implementation
- [ ] Test uses public interface only
- [ ] Test would survive an internal refactor
- [ ] Code is minimal for this test
- [ ] No speculative features added

Upstream: <https://github.com/mattpocock/skills/tree/main/skills/engineering/tdd>
