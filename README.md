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
| [ddaa-handoff](https://github.com/ddaanet/skills) | Resume-summary handoff (EN) — end-of-session summary to continue in a new chat, delivered to Notion when available. Enable this OR the lightweight `handoff` plugin, not both | `ddaanet/skills` |
| [ddaa-passation](https://github.com/ddaanet/skills) | Passation résumé de session (FR) — résumé de fin de session pour continuer dans un nouveau chat, livré sur Notion quand c'est disponible. Activer celui-ci OU le plugin `handoff` léger, pas les deux | `ddaanet/skills` |
| [handoff](https://github.com/ddaanet/handoff) | Pre-/clear task snapshot for Claude Code: agent notes current task + open decisions, a PostToolUse hook composes them with auto-extracted last-N user prompts and files touched from the session JSONL | `ddaanet/handoff` |
| [gitmoji](https://github.com/ddaanet/gitmoji) | Commit-msg git hook that replaces conventional-commit prefixes (feat:, fix:, docs:, ...) with gitmoji emojis. Ships an installer command that stows the hook into the current git repo | `ddaanet/gitmoji` |
| [gitlore](https://github.com/ddaanet/gitlore) | Versioned, shared, git-backed memory for Claude Code | `ddaanet/gitlore` |
| [onekeys](https://github.com/ddaanet/onekeys) | UserPromptSubmit hook that expands single-character prompts into full instructions (c → Continue, h → /handoff:handoff). Mappings live in ~/.claude/onekeyers.txt | `ddaanet/onekeys` |
| [cwd-safety](https://github.com/ddaanet/cwd-safety) | Keeps the agent's Bash working directory at project root: a PreToolUse(Bash) hook blocks drift-inducing `cd` commands and commands run from a drifted cwd; a PostToolUse(Bash) hook warns after the working directory changes | `ddaanet/cwd-safety` |
| [candidature](https://github.com/ddaanet/candidature) | Candidature assistée : préparation, lettre de motivation, CV adapté, relecture, suivi des retours. Stockage Notion. Contenu français | `ddaanet/candidature` |
| [shell-scripting](https://github.com/ddaanet/shell-scripting) | Shell scripting gotchas skill plus automatic shellcheck feedback on edited shell files | `ddaanet/shell-scripting` |

Install a plugin:

```
/plugin install ddaa@ddaanet
```

## License

MIT
