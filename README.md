# claude-plugins

Claude Code plugin marketplace by [ddaanet](https://github.com/ddaanet).

## Install

```
/plugin marketplace add ddaanet/claude-plugins
```

## Plugins

| Plugin | Description | Repo |
|--------|-------------|------|
| [ddaa](https://github.com/ddaanet/skills) | Skills (EN) — brief, preflight, proof, bilingual skill creator, bookkeeping | `ddaanet/skills` |
| [ddaa-fr](https://github.com/ddaanet/skills) | Skills (FR) — brief, preflight, relecture, saisie comptable | `ddaanet/skills` |
| [handoff](https://github.com/ddaanet/handoff) | Pre-/clear task snapshot: agent notes current task, a hook composes them with auto-extracted user prompts and files touched | `ddaanet/handoff` |
| [gitmoji](https://github.com/ddaanet/gitmoji) | Commit-msg hook that rewrites conventional-commit prefixes (feat:, fix:, ...) into gitmoji emojis | `ddaanet/gitmoji` |
| [gitlore](https://github.com/ddaanet/gitlore) | Versioned, shared, git-backed memory — Claude Code's auto-memory in a git submodule, with semantic merge on divergence | `ddaanet/gitlore` |
| [onekeys](https://github.com/ddaanet/onekeys) | UserPromptSubmit hook that expands single-character prompts into full instructions (c → Continue, h → /handoff) | `ddaanet/onekeys` |
| [cwd-safety](https://github.com/ddaanet/cwd-safety) | Keeps the agent's Bash working directory at project root: blocks drift-inducing `cd` commands and warns when the cwd changes | `ddaanet/cwd-safety` |

Install a plugin:

```
/plugin install ddaa@ddaanet
```

## License

MIT
