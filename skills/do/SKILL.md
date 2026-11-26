---
name: do
description: Use when the user asks to implement a task, feature, idea, or ticket end to end, such as `/do PROJ-123` or `/do add sidebar shortcuts`.
disable-model-invocation: true
---

# Do

Take a request from spec or idea to a verified, reviewed change the user can
ship without steering. Explicit requirements outrank existing patterns, which
outrank generic conventions.

## 1. Brief

Gather the spec and codebase context before coding:

- **When a ticket, issue, or doc exists:** read it, linked and related items,
  and relevant PRs or threads. Keep issue trackers read-only.
- **Codebase context:** use `scan` when the area is unfamiliar to learn
  structure, callers, history, and expected checks.
- **When starting from an idea or prompt:** ground scope in the codebase. If
  the design itself is unsettled, run `grill-me` first or settle open decisions
  in step 2.

Write a short brief (for example `<slug>/brief.md` in scratch or thread storage
when available):

- **Requirements:** numbered. Quote acceptance criteria verbatim when a written
  spec exists; otherwise state concrete, testable outcomes.
- **Non-goals:** what is explicitly left out or deferred.
- **Preserve:** existing behavior that must keep working. Remove behavior only
  when the request says so.
- **Decisions:** open details you settled, one line each.
- **Questions:** only those that pass step 2.

## 2. Ask once, only if needed

A question qualifies only when the spec, codebase, and history are silent (name
where you looked), the decision belongs to the user, and a wrong guess is
costly to undo. Send qualifying questions in one batch with a recommended
default before coding. Decide everything else, record it under Decisions, and
continue.

## 3. Implement

Limit the change to the requirements. Match nearby code for structure and
naming. When a local pattern conflicts with an explicit requirement, follow the
requirement.

Add guards only for inputs the contract or real data can produce, with evidence.
Add no hardening, locking, retries, or infrastructure the request does not ask
for unless correctness requires it.

Before verifying, read the full diff against the user's and project's written
rules. Strip stray comments, single-use helpers, confusing names, and
unnecessary nesting.

## 4. Verify

Get the project running. When a check needs sudo or local credentials, request
them through the host's secure secret prompt instead of skipping the check. Run
formatters, static analysis, and the tests required by the project or risk of
the change under enforced resource limits. Add tests for meaningful new
behavior following `test-audit`. Name anything that could not run and why.

## 5. Review

Unless the user names others, spawn two independent read-only reviewers from
different model vendors using the host's delegation tools and routing guidance.
Give each the brief, the diff, the verification results, and the rule that
explicit requirements outrank local patterns. Ask each for findings tagged:

- **spec:** misses, violates, or drifts from a Requirement or Preserve item.
- **bug:** fails on input that can realistically occur; state that input.
- **preference:** breaks the user's or project's written rules.
- **speculative:** anything else.

Check every finding yourself. Apply `spec`, `bug`, and `preference` findings.
List `speculative` ones in one line as not applied. Ask the same reviewers to
recheck only when a fix changed behavior. Reviewers never edit.

## 6. Report

Follow the project's Git and PR instructions; do not stage, commit, push, or
open a PR unless asked. Keep the report short:

- A table mapping each requirement to files and tests.
- **Extras:** changes no requirement asks for, each with its reason. Aim for none.
- Decisions made, findings not applied, verification commands with real results,
  and anything still open.
