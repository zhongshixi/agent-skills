# agent-skills

Skills for software engineers, for Claude Code and Cursor.

Engineering skills apply across languages. Language skills apply to one language. Both live directly under `skills/`.

| Kind | Path |
| --- | --- |
| Engineering | `skills/<topic>/` |
| Language | `skills/<language>-<topic>/` |

## Skills

| Skill | Kind | Description |
| --- | --- | --- |
| `pull-request-code-review` | Engineering | Review a GitHub pull request or a GitLab merge request. |

## Install one skill

These commands are the same on macOS, Linux, and Windows WSL. Run them in a Unix shell. On Windows, that shell is WSL, and the install lands in the Linux home directory.

Replace `pull-request-code-review` with the skill name.

### npx skills

Requires Node.js 22.20 or later.

```bash
npx skills add zhongshixi/agent-skills --skill pull-request-code-review -a claude-code -a cursor -g
```

`-g` installs the skill for every project. Omit `-g` to install it into the current project only.

From a local clone:

```bash
npx skills add . --skill pull-request-code-review -a claude-code -a cursor -g
```

### Symlink

```bash
git clone https://github.com/zhongshixi/agent-skills.git
cd agent-skills
mkdir -p ~/.claude/skills ~/.cursor/skills
ln -sfn "$PWD/skills/pull-request-code-review" ~/.claude/skills/pull-request-code-review
ln -sfn "$PWD/skills/pull-request-code-review" ~/.cursor/skills/pull-request-code-review
```

| Host | Path |
| --- | --- |
| Claude Code | `~/.claude/skills/pull-request-code-review` |
| Cursor | `~/.cursor/skills/pull-request-code-review` |

## Create a skill

Add a directory and a `SKILL.md`:

```
skills/<skill-name>/
  SKILL.md
  references/       # optional detail, linked from SKILL.md
  assets/           # optional configs and templates
  evals/evals.json  # optional checks
```

The frontmatter `name` matches `<skill-name>`. Writing rules are in [CLAUDE.md](CLAUDE.md).

## License

[Apache-2.0](LICENSE).
