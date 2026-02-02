# Claude Code Skills

Personal skills library for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Skills

| Skill | Purpose |
|-------|---------|
| [`architecture-reviewer`](./architecture-reviewer/SKILL.md) | Reviews technical plans, design docs, and architecture proposals with deep specificity across all system dimensions |
| [`blog-reviewer`](./blog-reviewer/SKILL.md) | Critical review of blog post drafts — authenticity, logic, grammar, AI slop detection |
| [`first-principles-tutor`](./first-principles-tutor/SKILL.md) | Deep-learning tutor using Socratic questioning and exercises that force genuine understanding |
| [`pr-reviewer`](./pr-reviewer/SKILL.md) | Code review for PRs — correctness, bugs, security, performance, scalability |
| [`prd`](./prd/SKILL.md) | Generate Product Requirements Documents for new features |
| [`ralph`](./ralph/SKILL.md) | Convert PRDs to prd.json format for the Ralph autonomous agent system |

## Installation

These skills are designed for `~/.claude/skills/`. Clone directly:

```bash
git clone git@github.com:ravisankar-r/claude-skills.git ~/.claude/skills
```

Or symlink if you want to keep the repo elsewhere:

```bash
git clone git@github.com:ravisankar-r/claude-skills.git ~/repos/claude-skills
ln -s ~/repos/claude-skills ~/.claude/skills
```

## Usage

Skills trigger automatically based on their descriptions, or invoke explicitly:

```
/architecture-reviewer
/first-principles-tutor
/pr-reviewer
/blog-reviewer
/prd
/ralph
```

## Structure

```
skills/
├── skill-name/
│   └── SKILL.md      # Skill definition with YAML frontmatter
└── README.md
```

Each skill follows the Claude Code skill format:
- YAML frontmatter with `name` and `description`
- Description defines trigger conditions
- Markdown body contains the skill instructions

## Creating New Skills

```markdown
---
name: skill-name
description: >
  Use when [triggering conditions]. Triggers on: "phrase1", "phrase2".
---

# Skill Name

[Instructions for Claude when this skill is invoked]
```
