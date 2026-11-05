---
name: test-audit
description: Use when writing or reviewing automated tests, deciding whether tests are needed, or auditing existing coverage.
---

# Test audit

Keep tests lean and proportional to risk. Each test should catch a credible
failure in behavior or an independent contract. Optimize for confidence and
maintenance cost; test count, deleted lines, and coverage percentages are not
success criteria.

Adapted from OpenClaw's
[test-audit](https://github.com/openclaw/openclaw/blob/main/.agents/skills/test-audit/SKILL.md).

## Scope and context

Use the authoring gate during ordinary implementation. Audit the existing suite
only when the task asks for it, or when overlapping tests must be understood to
complete the current change. Keep audits to the requested files or subsystem.

A question or review is read-only. An implementation or cleanup request permits
the relevant edits and verification; this skill adds no approval step. Preserve
existing work and Git authorization. Do not touch production, live databases, or
daily-driver build and preview channels without explicit authorization.

Read applicable `AGENTS.md`, testing guidance, the current diff, and nearby
implementations first. Inspect the production owner, real callers, and existing
coverage before choosing a test boundary. Use the project's runner and existing
fixtures. Keep TypeScript types inferred where possible; do not introduce `any`
or casting wrappers to make tests compile.

## Authoring gate

Before adding or substantially changing a test, establish:

1. The observable behavior, invariant, or independent contract it protects.
2. A credible regression that would fail the assertion for the intended reason.
3. Why existing coverage does not already catch that failure.
4. Whether it requires an export, flag, wrapper, or injection hook used only by
   tests. Prefer exercising a real boundary; do not add that seam by default.

If these answers do not justify the test, reuse or extend existing coverage,
choose a better boundary, or omit the test. Explain the decision briefly when it
matters. Do not add tests for reversible, low-impact changes such as formatting
or wording unless an actual contract or project requirement warrants them.

Give each contract a primary test owner at the cheapest reliable boundary.
Another layer needs its own distinct risk, such as serialization, transport, or
lifecycle behavior. Extend a table-driven case or shared fixture before creating
a near-duplicate file or setup. Avoid helper abstractions used only once.

For bug fixes, demonstrate that the regression test fails on the pre-fix code
for the bug's intended reason and passes after the fix. Use an isolated copy or
worktree when needed; never discard current edits to recreate the baseline. If
baseline proof is unavailable, report that limit rather than claiming it.

## Audit candidates

Look for tests that:

- execute code without a meaningful assertion;
- compare a value with itself, or generate expected output using the code under test;
- copy export lists, manifests, fixtures, or declared flags without an independent contract;
- inspect exact source text, private helpers, or call shapes that change during harmless refactoring;
- replay the same failure across layers without covering a distinct risk;
- assert behavior supplied entirely by a mock or fixture rather than the production owner;
- pass for an unrelated reason, such as rejection by the wrong guard;
- keep dead code or test-only exports, globals, and wrappers alive;
- use broad snapshots or whole-object assertions when a focused behavior check would suffice.

For DOM or React identity, assert a boolean with a short failure message rather
than comparing whole objects.

These patterns identify candidates, not automatic deletions. A static source
check, snapshot, ordering assertion, or slow integration test may be the cheapest
independent guard for a real contract. Keep meaningful API, security, storage,
migration, configuration, protocol, release, and architecture coverage. A failing
retained test may reveal a product bug; investigate instead of deleting it.

## Evidence before cleanup

For each proposed deletion or rewrite, establish:

- the exact test and what failure it can detect;
- the production owner and non-test callers of any affected seam;
- the remaining test that catches the same failure, or evidence that the contract
  is obsolete and no replacement is needed;
- relevant history when it could explain the test's purpose;
- the risk, intended edit, and focused validation.

Missing evidence means keep the test and record the uncertainty. In a read-only
audit, report candidates and evidence. In authorized cleanup, apply a small,
coherent batch once the evidence is sufficient; do not wait for extra approval.
Rewrite valuable behavior checks at their owner instead of deleting their only
proof. Remove obsolete support seams only after checking for real callers.

Unchanged coverage does not prove a deletion safe. Check the failure the removed
test caught and whether the retained assertion still detects it.

## Verification and finish

Run tests with enforced memory, CPU, and wall-clock limits for the entire process
tree. On Linux, use a systemd cgroup or container. A Node heap cap or timeout alone
is insufficient. If containment is unavailable, report that limit and use other
available checks. Never retry a resource-exhausting run without containment.

Do not edit files while tests are running in that checkout. Start with affected
tests and relevant neighboring coverage, then required project checks. Broaden
only for changed shared behavior, failures, or unresolved risks. Stop after the
appropriate checks pass. Run the applicable formatter or typecheck and
`git diff --check` for edited code.

Report meaningful tests added, extended, retained, rewritten, or removed and the
reason. Include checks actually run, baseline proof for regressions, and unresolved
limits. Report production and test-support simplifications when relevant. Leave
commit, push, and deployment to the user's authorization and project policy.
