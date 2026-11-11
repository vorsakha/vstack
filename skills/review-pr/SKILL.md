---
name: review-pr
description: Use when reviewing an existing open GitHub pull request and drafting review comments in the current thread.
---

# Review PR

Review an open PR with one reviewer. Return actionable comment drafts in the
current thread. Do not fix code, commit, push, or write to GitHub, including
pending reviews and PR descriptions. These limits also apply to delegates.

## Scope and scan

Resolve the PR from the user's link or number, or the current branch's open PR.
Ask only if the target is ambiguous. Confirm it is open and record its URL, base
and head SHAs, and merge base. Review the merge-base-to-head diff, not local edits.
Preserve the working tree; use an isolated checkout when it differs from that head.

Before detailed review, use the `scan` skill on the changed areas. Apply its brief
on project conventions, nearby implementations, past review expectations, and
validation. Read the PR description, linked requirements, full diff, and existing
review threads, including inline discussions.

## Review

Use the host's available delegation tools to run one reviewer, following any
applicable routing guidance. The user's requested reviewer takes priority;
otherwise default to GPT Sol. Verify the selected model is available and report
a missing route instead of substituting.

Give the reviewer the exact revision, diff scope, intended behavior, scan brief,
and available check results. Require review only, no GitHub writes, no fixes, and
no further delegates. Ask for concrete findings with file locations, evidence,
impact, and the smallest suggested correction.

Look for bugs introduced by the PR, broken callers, and mismatches with its
intent. Skip style preferences, speculative future needs, and unrelated cleanup.
Judge rare cases by their real impact. Do not demand extra tests without a
specific behavior they would protect.

Validate each finding yourself against the code and relevant callers. Use focused
existing checks or a small isolated repro when useful; state what could not be
verified. Merge duplicate root causes and omit findings already covered by an
existing review thread unless you add material evidence. Push back on unsupported
findings. Use at most one focused follow-up to clarify disputed findings.

## Comment drafts

Return one ready-to-copy comment per supported finding, most serious first:

- Priority and a short title.
- Exact file and smallest relevant line range, with a source permalink pinned
  to the reviewed head. For deleted code, use the merge-base revision and lines.
- A concise comment explaining the triggering case, what breaks, why it matters,
  and the smallest suggested correction. Include evidence when it helps.

Keep unresolved suspicions separate from comment drafts. If no supported findings
remain, say "No actionable findings" without inventing comments.

Finish with the PR URL, reviewed head SHA, actual reviewer model, checks and their
results, and material review limits. Recheck the PR head before finishing; if it
changed, clearly mark the review as covering the recorded revision only. Stop
after returning the drafts and review summary in the thread.
