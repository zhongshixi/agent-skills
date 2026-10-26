# CLAUDE.md

Rules for adding a skill to this catalog.

## Where it goes

One directory per skill, directly under `skills/`:

| Kind | Directory | `name` |
| --- | --- | --- |
| Engineering | `skills/<topic>/` | `<topic>` |
| Language | `skills/<language>-<topic>/` | `<language>-<topic>` |

`<language>` is a lowercase id such as `golang` or `typescript`. The full name is lowercase letters, numbers, and single hyphens, at most 64 characters, and it matches the directory name.

`.claude-plugin/plugin.json` and `.cursor-plugin/plugin.json` stay in sync. Bump both versions together when the catalog version changes. Bump `metadata.version` when that skill changes.

## SKILL.md

```yaml
---
name: golang-error-handling
description: "Idiomatic error handling in Golang. Use when creating, wrapping, or logging errors in Go."
user-invocable: true
license: Apache-2.0
compatibility: Designed for Claude Code, Cursor, and similar AI coding agents.
metadata:
  author: zhongshixi
  version: "1.0.0"
  category: language
  language: golang
allowed-tools: Read Edit Write Glob Grep Bash Agent
---
```

Engineering skills omit `metadata.language` and set `category: engineering`.

| Field | Rule |
| --- | --- |
| `description` | What it does and when to load it. Name the language in a language skill. An engineering skill names the task, not a language. 1–1024 characters. |
| `user-invocable` | `true` so Claude Code lists `/skill-name`. |
| `allowed-tools` | Start from `Read Edit Write Glob Grep Bash Agent`. Add a tool only when this skill runs it. |

When two skills could match the same request, the one that should stay quiet points at the owner: `→ See \`zhongshixi/agent-skills@skill-name\``.

## Body

1. One sentence on the posture this skill captures.
2. Numbered practices. Each one says the rule and why.
3. Links to `references/<topic>.md` for anything too long to sit in `SKILL.md`. One level deep, and only after the file exists.
4. Cross-references for concepts this skill does not own.

Each concept lives in one skill. Put configs and templates in `assets/` and link them.

`evals/evals.json` is optional. When present, `skill_name` matches the directory, and each eval has a `prompt`, the `trap` that prompt invites, and `assertions`.
