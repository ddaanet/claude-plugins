# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A Claude Code plugin **marketplace** — a registry that lets users discover and install plugins via `/plugin marketplace add ddaanet/claude-plugins`. Contains no runtime code; only metadata pointing to external plugin repos.

## Key File

`.claude-plugin/marketplace.json` — the marketplace manifest. Schema reference: https://code.claude.com/docs/en/plugins-reference

### Manifest Structure

- `name`: marketplace identifier (`ddaanet`), used in `/plugin install <plugin>@ddaanet`
- `owner`: maintainer info (name, optional email)
- `metadata.description`: brief marketplace description
- `plugins[]`: array of plugin entries, each with:
  - `name` (required): plugin identifier, used in install commands
  - `source` (required): object with `source: "github"` and `repo: "owner/repo"` (can also use `ref`/`sha` to pin)
  - Optional: `description`, `version`, `author`, `repository`, `license`, `keywords`, `category`

All plugins in this marketplace use GitHub sources (`"source": "github"`). The actual plugin code lives in the referenced repos, not here.

### Strict Mode

Default is `strict: true` — the plugin's own `plugin.json` is authoritative; marketplace entries only supplement. Set `strict: false` on an entry to make the marketplace definition the entire plugin definition (no `plugin.json` needed in the target repo).

## Validation

```
claude plugin validate .
```

Or inside Claude Code: `/plugin validate .`

## Conventions

- Git remote is named `github` (not `origin`).
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
