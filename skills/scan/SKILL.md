---
name: scan
description: Use before coding to learn a project's conventions and recurring review expectations.
---

# Scan

Learn how contributors work here so the next change fits the project.
Focus on the planned change. Without one, map the main boundaries and contribution
workflow. Research only unless implementation is already authorized.

Read project instructions, contributor docs, PR templates, and relevant CI config.
Trace nearby implementations, callers, shared helpers, tests, and explanatory
comments. Find examples worth following and understand why they look that way.

Use Git history to find PRs touching the same code or solving similar problems.
Read descriptions, review summaries, inline discussions, and replies. Follow
linked issues or design decisions when they explain a constraint. On GitHub,
`gh pr view --comments` alone misses inline review threads; retrieve those too
and follow pagination.

Recover what reviewers objected to, how the author responded, and what ultimately
landed. Check that the lesson still applies to current code. A resolved thread
or merged PR does not make every suggestion a project rule.

Prefer current scoped instructions and repeated local patterns. Separate durable
expectations from isolated preferences, legacy code, and guesses. Investigate
conflicting evidence; don't invent consensus. If history is unavailable, say so
and continue locally. Stop when further searches repeat what you already know.

Return a short brief with concrete examples to follow, existing code to reuse,
review objections to avoid, and expected validation and PR details. Link the files
and discussions behind each recommendation. Mention uncertainties that could
change the approach. Apply the findings when continuing authorized implementation.
