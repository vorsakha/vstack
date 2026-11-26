---
name: debrief
description: Use after an agent finishes implementing a feature or task, when the user wants to understand what changed, why, how it was before, and the blast radius.
disable-model-invocation: true
---

# Debrief

The user didn't write this code but must own the PR. Give them, in a two-minute
read, what they need to explain and defend it in review. A long debrief defeats
the purpose: they would rather ask a follow-up than read a report.

Run it in the thread that did the work, since you know which decisions were
yours, the spec's, or a reviewer's. This is read-only. Do not edit, stage,
commit, or post anything, and keep issue trackers read-only.

## Investigate fully

- **Spec:** the ticket or issue when there is one, including the epic or linked
  items when they explain scope, otherwise the user's request.
- **Diff:** unstaged and staged changes plus the branch against its merge base.
  Read every hunk, including tests, fixtures, configs, lockfiles, and migrations.
- **Each change:** why it exists (a spec line, or whose call it was), before →
  after, whether it's needed or just defensive, and whether the repo already
  does it that way. Search for precedent; don't assume it.
- **Consumers:** trace changed surfaces to callers, routes, response shapes,
  shared components, DB columns, config, and sibling apps in the workspace.
- **Proof:** what was actually tested and run, and what wasn't.

## Report only what's surprising

Leave out:

- Anything the user decided or saw in this thread.
- Changes that do exactly what the spec says in the way the repo already does it.
- Pattern evidence for conforming code. Mention patterns only when they are new
  or deviate.
- Lists of things that are unaffected. Summarize safety in one line.
- Empty sections, and sections that would only say "nothing".

Keep in:

- What the change does, in plain words.
- Additions beyond the spec, with why, and whether to keep each.
- Deleted code or dependencies that existed before this work, and what used them.
- New packages, tables, migrations, env vars, or infra.
- Drifts from the spec's wording.
- What could break, and what must happen on deploy.
- Risky gaps in verification.

## Answer

Use this shape, dropping any section with nothing to report:

- **TL;DR:** two or three lines on what it does now versus before, and its size.
- **Not in the spec:** one line each.
- **New here:** new patterns, dependencies, tables, or infra.
- **Removed.**
- **Blast radius:** what could break and deploy needs, plus one line on what's safe.
- **Not verified:** at most three items, only the risky ones.
- **Questions:** decisions only.

One line per item, no tables, `file:line` only where it helps them find it. Aim
for under 250 words. Recommend dropping extras that aren't needed, but leave the
change to the user.
