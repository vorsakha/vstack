---
name: skill-composer
description: Use when creating or refining an agent skill.
---

# Skill composer

Write the smallest skill that reliably improves how an agent handles its task.

Start from a concrete request and the result it should produce. Identify the
decisions the agent needs help making. Inspect related skills for overlap before
adding another. Infer routine details; ask only when the answer changes the skill.

Use a short lowercase hyphenated name and a matching folder containing `SKILL.md`.
Begin with YAML `name` and `description`. The description is only an activation
hook: one short sentence saying when to use it. Put the procedure in the body.

Write direct instructions. Keep domain knowledge, decision boundaries, and
constraints that affect the result. Cut generic advice, repeated rules, exhaustive
inventories, and explanations the agent does not need. Explain a rule only when
its reason changes how to apply it. Preserve useful behavior when shortening.

Define the expected result and when the work is complete. Prescribe an exact
sequence only where order matters. Keep task-specific permission boundaries
explicit without adding approval steps to work the user already authorized.

Default to one file. Add references for substantial conditional detail, scripts
for repeated mechanical work, and assets for actual output needs. Say when to
use each resource. Follow the target project's installation conventions.

Check the hook against an intended request and a similar request that should not
activate it. Check frontmatter, names, and referenced paths. For behavior changes,
try a realistic example and judge the result, not whether it repeats the wording.
Run added scripts. Keep validation proportional and report what was actually
checked. Finish with the skill and a brief validation note.
