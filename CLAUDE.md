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

- Git remote is named `github` (not `origin`).
- Push: `git push github main`
- Commit messages use emoji prefixes (e.g. `🎉`, `📝`, `🏷️`).
- Keep `README.md` and `marketplace.json` in sync — any plugin listed in one must appear in the other.

## Common Operations

- **Add a plugin:** add an entry to `plugins[]` in `marketplace.json` + a row to the table in `README.md`.
- **Update a plugin:** edit the entry in `marketplace.json`, keep `README.md` in sync.

## Plugin Ecosystem

| Plugin | Repo | Local path |
|--------|------|------------|
| `ddaa` | `ddaanet/skills` | `../skills` |
| `edify` | `ddaanet/edify-plugin` | `../claudeutils` |

## Update Model

Third-party marketplaces do not auto-update. Users must run `/plugin marketplace update` to refresh. Plugin repos must **bump `version` in `plugin.json`** for updates to be detected — same version = skipped. Pinning via `ref`/`sha` in the source object is optional.
