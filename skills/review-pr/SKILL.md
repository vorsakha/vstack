---
name: review-pr
description: Use when reviewing an existing open GitHub pull request and drafting review comments in the current thread.
disable-model-invocation: true
---

# Review PR

Review an open PR with one reviewer. Draft in the current thread by default.
Keep the checkout and GitHub read-only during review, including for delegates.
An explicit request to post comments authorizes the publishing step below.

## Scope and scan

Resolve the PR from the user's link or number, or the current branch's open PR.
Ask only if the target is ambiguous. Confirm it is open and record its URL, base
and head SHAs, and merge base. Review the merge-base-to-head diff. Preserve the
working tree and use an isolated checkout when it differs from the reviewed head.
Read the PR description, linked requirements, full diff, and existing review
threads, including inline discussions.

Use the `scan` skill before briefing the reviewer. Read a small sample of actual
human inline comments on comparable PRs, including replies and resulting
changes where they explain what the team accepted. Prefer the user's own
reviews when identifiable, then regular reviewers in the affected area. If the
closest PRs have no examples, widen the search to recent repository-wide inline
comments. Carry representative examples into the brief: the team's language,
what it considers worth raising, and how reviewers phrase or suggest edits.
When history is unavailable, say so briefly and use nearby code conventions.

## Review and select

Use the host's delegation tools and routing guidance for one reviewer. Honor the
requested reviewer, otherwise use GPT Sol. Verify availability and report a
missing route rather than substituting. Supply the revision, diff scope, intent,
scan brief, and available checks. Require review only, no writes, fixes, or
further delegates. Ask for locations, evidence, impact, and the smallest edit.

Trace changed code through its callers. Check for regressions and concrete
simplifications a teammate would ask for: a repeated query, an existing helper
that already does the job, or state the component lifecycle can manage. Let the
diff and project history drive the review. Use focused checks or a small
isolated repro when they settle a finding. Request tests only for a specific
behavior they would protect.

Validate candidates yourself. Lead with verified risks such as wrong writes,
data loss, or broken callers. When something should block merge, say why.
Include simplifications with a concrete payoff. Drop low-value observations,
speculative cases without meaningful impact, and issues covered by existing
threads unless you have material new evidence. Merge duplicate causes and use
at most one focused follow-up with the reviewer for a disputed finding.

## Draft in the thread

Write each comment as the user could post it, in the team's language and tone.
Put the exact file, smallest relevant line range, and head-pinned permalink
outside the copyable text. Use the merge-base permalink for deleted code.
Keep severity labels and review narration out of the author's comment.

When the replacement is clear, show a GitHub `suggestion` block containing the
exact replacement lines, including indentation. Show it inline in the first
response. For a coordinated change, give every necessary hunk its own file and
range, explain the reason once on the main hunk, and verify the replacements
apply together to the reviewed revision. An attachment may supplement the
inline suggestions. Use a short question when the author needs to decide intent.

Keep PR-wide product questions, unresolved suspicions, and validation limits
separate from file comments. If nothing warrants a comment, say “No actionable
findings”. Finish with the PR URL, reviewed head, actual reviewer model, checks
and material limits. Recheck the head and flag any change since review.

## Publish when requested

Post only the comments the user authorizes. For code suggestions, use standalone
inline PR comments in Files changed, anchored to the current diff with the
exact replacement range and a `suggestion` block. Use a Conversation comment
for a PR-wide point or an explicit request for that placement. A request for
“comments only” keeps file suggestions inline. Approval, request-changes
verdicts, commits, and fixes require their own explicit request.

Immediately before posting, recheck the head, the affected lines, and existing
threads. If the head moved, validate and re-anchor each still-applicable
suggestion. Skip obsolete or duplicate comments. If asked for a preview first,
show the intended placement and text and wait for authorization. Verify each
posted comment's location and return discussion links.
