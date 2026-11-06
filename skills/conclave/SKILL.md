---
name: conclave
description: Use when the user requests a conclave or independent assessments from multiple AI models.
---

# Conclave

Bring independent perspectives to the user's question, design, or code.
Honor requested members, panel size, and reasoning effort.

Use the host's available delegation tools to launch separate reviewers. Inspect
available models and supported reasoning effort, following any applicable routing
guidance. Verify their actual vendors before dispatch. Keep the user's existing
account, permission, and spending constraints.

Aim for three strong flagship models from different vendors at extra-high
reasoning effort where supported, for example Claude Opus, GPT Sol, and Grok 4.7.
Report any effort limitation.
For the default panel, two eligible vendors suffice; report the reduced panel.
If fewer than two are available or an explicitly requested panel cannot be
formed, report the gap. Never simulate panel members in one conversation,
substitute named members, or use unapproved accounts or paid routes to fill it.

A question or review request stays read-only. When implementation is already
authorized, fix known issues and run relevant checks before presenting the change.
If replacing the implementation, skip fixes to code being discarded.
Settle edits before review and give every member the same revision and scope.
Keep that revision unchanged while reviewers work.

Give each reviewer the request, relevant context, constraints, and verification
evidence. Ask for an independent assessment with concrete findings, supporting
evidence, and uncertainties. Keep first responses independent of one another.
Delegates remain read-only throughout and must not create further delegates.

For reviews, ask each member for a score out of 10 and a short assessment of
the work's strengths, weaknesses, and suggested improvements. Count each full
review pass as one round; a fresh review after fixes starts another round.

For UI changes, compare actual before-and-after screenshots and relevant
reference apps or designs when available. Capture screenshots using available
browser or computer-use tools. Score typography, hierarchy, spacing and density,
color and contrast, iconography, consistency and polish, clarity, and overall
quality.

Accept when every participating reviewer meets the user's requested score target,
or 9/10 by default, and no substantive findings remain. Apply per-category targets
when requested. Do not pursue a higher target unless requested or let a high
score override an unresolved issue.

Inspect every response. Check findings yourself, combine duplicates, and preserve
disagreements. Prefer evidence over votes or scores. Reject scope expansion and
unsupported suggestions with a reason. A missing response is incomplete review.

For authorized implementation, make the smallest justified fixes, verify them,
then ask the same reviewers to recheck changed behavior and unresolved findings.
Repeat until every participating reviewer meets the target and is satisfied
with the result. Honor explicit round, time, and spending limits. If a limit or
unavailable reviewer prevents completion, report remaining concerns and unmet
targets; stopping is not approval. Reviewers remain read-only and never take
over implementation.

Return the actual models and vendors used, rounds, supported findings,
disagreements, and recommended next step. For code, identify the revision and
verification limits. Keep findings in the conversation unless the user also
requested publishing them to a PR.

For reviews, include a table of actual scores and verdicts by round, with columns
for every round performed. Include category scores when assessed. Use
`not provided` for missing scores and `not run` for rounds that did not happen.
Never invent scores. Example format; replace labels with the actual reviewers:

| Delegate | Round 1 | Round 2 |
| --- | --- | --- |
| Claude Opus | 7/10 · 2 issues | 9/10 · approved |
| GPT Sol | 8/10 · 1 issue | 10/10 · approved |
| Grok 4.7 | 7/10 · blocker | 9/10 · approved |
