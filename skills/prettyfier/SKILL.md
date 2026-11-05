---
name: prettyfier
description: Use when reviewing or improving code readability without changing behavior.
---

# Prettyfier

Improve how code reads without changing what it does.

Default to read-only review. Apply edits only when explicitly requested. Never stage, commit, discard, or otherwise alter Git state.

## Establish the Style

Before judging code, inspect:

- project instructions;
- formatter and linter configuration;
- the current diff;
- nearby accepted implementations.

Configured formatters own mechanical formatting. Local project conventions outrank general aesthetic preferences.

## Review

Look for:

- distinct logical phases packed together without breathing room;
- excessive blank lines fragmenting one operation;
- dense expressions, nested ternaries, or long conditions;
- awkward wrapping not owned by the formatter;
- unclear local names;
- unnecessary nesting or `else` after an unconditional return;
- redundant temporaries or repeated conditions;
- comments that restate code, are stale, or interrupt the flow;
- changed code that visually conflicts with its surroundings.

Prioritize code reviewers must actively reason through. Ignore harmless personal preferences.

## Restraint

Use the smallest patch that solves the reading problem.

- A blank line can be the complete fix.
- Prefer a named local before extracting a helper.
- Do not answer spacing feedback with a new module, hook, class, or abstraction.
- Do not change behavior, evaluation order, error paths, or public APIs.
- Do not reformat unrelated code.
- Do not expand the scope into architecture, correctness, or performance review.
- If the readability fix requires semantic changes, report it instead of applying it.

## Apply Fixes

When fixes are requested:

1. Edit only the relevant regions.
2. Run the formatter or focused linter for touched files.
3. Run a focused typecheck or existing tests when the edit could affect behavior or project guidance requires them.
4. Run `git diff --check`.
5. Leave all changes unstaged unless instructed otherwise.

## Report

Use at most a handful of findings:

- **Rough** — meaningfully interrupts comprehension.
- **Polish** — small, worthwhile improvement.

Format:

```text
path/file.ts:120 — setup, mutation, and dispatch are visually compressed
→ Separate the dispatch phase with one blank line.
```

Finish with:

- **Reads:** clean / mostly clean / cramped
- conventions and formatter consulted
- fixes applied, if any
- checks run and results

If the code already reads well, say so briefly and stop. Do not manufacture findings.
