# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A Claude Code plugin **marketplace** — a registry that lets users discover and install plugins via `/plugin marketplace add ddaanet/claude-plugins`. Contains no runtime code; only metadata pointing to external plugin repos.

## Key File

`.claude-plugin/marketplace.json` — the marketplace manifest. Schema: https://code.claude.com/docs/en/plugins-reference

Each `plugins[]` entry needs `name` and `source` (GitHub object with `repo`). Optional fields: `description`, `version`, `author`, `repository`, `license`, `keywords`. `strict: false` makes the marketplace entry the full definition (default `true` defers to the plugin's own `plugin.json`).

## Validation

`claude plugin validate .` (CLI) or `/plugin validate .` (inside Claude Code)

## Conventions

- Git remote is named `origin`.
- Push: `git push origin main`
- Commit messages use emoji prefixes (e.g. `🎉`, `📝`, `🏷️`).
- Keep `README.md` and `marketplace.json` in sync — any plugin listed in one must appear in the other.

## Common Operations

- **Add a plugin:** add an entry to `plugins[]` in `marketplace.json` + a `##` section in `README.md` (before "License"), summarized from the plugin's own README.
- **Update a plugin:** edit the entry in `marketplace.json`, keep `README.md` in sync.

## Writing a README Section

- One `##` section per plugin, no summary table. The install command and prerequisites go inside the section; the top "Install" section carries only the marketplace command.
- Check what the plugin's README and `plugin.json` claim against its content — `skills/*/SKILL.md`, `hooks/hooks.json`, bootstrap scripts — and describe what the plugin does, not how it rates itself. Self-descriptions such as "lightweight" or "framework-agnostic" have been wrong, a README has misdescribed its own skill, and a manual install step turned out to be done by a SessionStart hook.
- Name mechanisms concretely (tmux `send-keys`, a SessionStart bootstrap) rather than paraphrasing them.
- Describe the published state (`origin/main`) when the local clone is ahead of it.
- Wording that is wrong at the source gets a brief in that repo's `inbox/`. `marketplace.json` descriptions keep matching the plugin's `plugin.json`, which wins under the default `strict: true`.

## Plugin Ecosystem

| Plugin | Repo | Local path |
|--------|------|------------|
| `ddaa` | `ddaanet/skills` | `../skills` |
| `edify` | `ddaanet/edify-plugin` | `../claudeutils` |

## Update Model

Third-party marketplaces do not auto-update. Users must run `/plugin marketplace update` to refresh. Plugin repos must **bump `version` in `plugin.json`** for updates to be detected — same version = skipped. Pinning via `ref`/`sha` in the source object is optional.
