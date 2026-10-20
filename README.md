# agent-skills

Personal skills and other configuration for AI coding agents.

## Skills

| Skill | Purpose |
|---|---|
| [clarity](skills/clarity/SKILL.md) | Write and edit text so the reader gets the point from the first words. |

## Install

Each skill is installed by copying its folder into the agent's skills folder. For Claude Code, that is `~/.claude/skills/`:

```powershell
Copy-Item -Recurse skills/clarity $HOME/.claude/skills/
```
