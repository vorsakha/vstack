# vstack

Agent skills for repository research, code review, planning, and visual references.
Use them with Claude Code, Codex, or another agent that supports `SKILL.md` skills.

## Skills

| Skill | Say | What it does |
| --- | --- | --- |
| [scan](skills/scan/SKILL.md) | "scan this repo" | Finds project conventions, reusable code, and recurring review expectations before coding. |
| [do](skills/do/SKILL.md) | "/do PROJ-123" | Takes a task, idea, or ticket from brief through implementation, verification, and review. |
| [review-pr](skills/review-pr/SKILL.md) | "review this PR" | Reviews an open PR with one reviewer and returns actionable comment drafts in the thread. |
| [debrief](skills/debrief/SKILL.md) | "debrief" | Explains finished agent work briefly: why each change exists, what's new, and the blast radius. |
| [skill-composer](skills/skill-composer/SKILL.md) | "compose a skill" | Writes concise skills with useful triggers, instructions, and validation. |
| [grill-me](skills/grill-me/SKILL.md) | "grill me" | Stress-tests an idea through rounds of independent questions and recommended answers. |
| [prettyfier](skills/prettyfier/SKILL.md) | "prettyfier" | Reviews or improves code readability while preserving behavior. |
| [test-audit](skills/test-audit/SKILL.md) | "audit these tests" | Keeps tests meaningful and proportional to risk, with evidence before cleanup. |
| [reference-harvester](skills/reference-harvester/SKILL.md) | "harvest references" | Curates visually inspected images and video frames with source records. |
| [conclave](skills/conclave/SKILL.md) | "conclave" | Gets independent assessments from multiple model vendors and checks findings against evidence. |

Install only the folders you want, along with their listed dependencies.

## Install

```bash
git clone https://github.com/vorsakha/vstack.git
mkdir -p ~/.claude/skills ~/.codex/skills
cp -R vstack/skills/* ~/.claude/skills/   # Claude Code
cp -R vstack/skills/* ~/.codex/skills/    # Codex
```

For other agents, copy the selected folders into their supported skills directory.

## Requirements

- `scan` benefits from repository history and access to review discussions. On
  GitHub, use an authenticated GitHub CLI or connector.
- `do` uses `scan`, `grill-me`, and `test-audit` when applicable, and needs
  delegation tools to launch independent read-only reviewers across model
  providers.
- `review-pr` uses `scan` and needs delegation tools with access to the selected
  reviewer model. It defaults to GPT Sol unless you request another reviewer.
- `grill-me` uses read-only research subagents to look up facts when needed.
- `conclave` needs an agent environment that can launch independent reviewers
  across model providers, using accounts and routes you have authorized.
- `reference-harvester` needs tools for image discovery, downloads, and visual
  inspection. Video references also require frame extraction.

## Make them yours

Keep project conventions and personal preferences in your `AGENTS.md` or
`CLAUDE.md`. Choose models and tooling that fit your agent environment, and adapt
the skills when your workflow needs something different.
