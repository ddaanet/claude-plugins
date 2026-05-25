# claude-plugins

Claude Code plugin marketplace by [ddaanet](https://github.com/ddaanet).

## Install

```
/plugin marketplace add ddaanet/claude-plugins
```

## Plugins

| Plugin | Description | Repo |
|--------|-------------|------|
| [ddaa](https://github.com/ddaanet/skills) | Bilingual skills — briefing, handoff, preflight validation, structured proofreading, skill creation | `ddaanet/skills` |
| [edify](https://github.com/ddaanet/edify-plugin) | Opinionated agent framework for Claude Code | `ddaanet/edify-plugin` |
| [handoff](https://github.com/ddaanet/handoff) | Pre-/clear task snapshot: agent notes current task, a Stop hook composes them with auto-extracted user prompts and files touched | `ddaanet/handoff` |
| [gitmoji](https://github.com/ddaanet/gitmoji) | Commit-msg hook that rewrites conventional-commit prefixes (feat:, fix:, ...) into gitmoji emojis | `ddaanet/gitmoji` |
| [double-shot-latte](https://github.com/ddaanet/double-shot-latte) | Auto-continue stop hook: uses a Claude judge to decide if the agent should keep working instead of stopping prematurely | `ddaanet/double-shot-latte` |
| [gitlore](https://github.com/ddaanet/gitlore) | Versioned, shared, git-backed memory — Claude Code's auto-memory in a git submodule, with semantic merge on divergence | `ddaanet/gitlore` |

Install a plugin:

```
/plugin install ddaa@ddaanet
```

## License

MIT
