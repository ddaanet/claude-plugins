# claude-plugins

Claude Code plugin marketplace by [ddaanet](https://github.com/ddaanet).

## Install

Add the marketplace once, then install plugins individually — each section
below gives the command and any extra setup.

```
/plugin marketplace add ddaanet/claude-plugins
```

Third-party marketplaces do not auto-update: run `/plugin marketplace update`
to pick up new plugin versions.

## ddaa, ddaa-fr, ddaa-handoff, ddaa-passation

[ddaanet/skills](https://github.com/ddaanet/skills) — bilingual
[Agent Skills](https://agentskills.io) for claude.ai and Claude Code, shipped
as four plugins. Each skill is a native rewrite in its target language, not a
mechanical translation, so that instructions match the language of the
conversation.

- **brief** (ddaa, ddaa-fr) — Mission document for Claude Code
- **preflight** (ddaa, ddaa-fr) — Pre-release validation
- **proof / relecture** (ddaa, ddaa-fr) — Structured item-by-item proofreading
- **bilingual-skill-creator** (ddaa) — Create a skill in two languages
- **bookkeeping / saisie-comptable** (ddaa, ddaa-fr) — Bank statements into a double-entry CSV ledger
- **handoff / passation** (ddaa-handoff, ddaa-passation) — Session wrap-up to continue in a new chat

`handoff` / `passation` live in their own plugins so each project decides
separately. They are most useful in hybrid projects where Claude Code
cooperates with claude.ai. For code-only work, the `autodrive-handoff`
plugin — a local task snapshot rather than a full session summary — covers
the same ground.

English:

```
/plugin install ddaa@ddaanet
/plugin install ddaa-handoff@ddaanet
```

Français :

```
/plugin install ddaa-fr@ddaanet
/plugin install ddaa-passation@ddaanet
```

Install one language per project, not both. Enable `ddaa-handoff` /
`ddaa-passation` OR the `autodrive-handoff` plugin, not both.

## autodrive-handoff

[ddaanet/autodrive-handoff](https://github.com/ddaanet/autodrive-handoff) — a
task frame that survives a `/clear` or `/compact`. Before the reset, the agent
writes the task in hand to `TASK.md` and the open decisions and remaining
todos to `TODO.md`, in the project root; `SessionStart` hooks inject them
back, verbatim, into the next session. Before a `/compact` only `TODO.md` is
written, since the compaction summary carries the task.

- `/autodrive-handoff:handoff` — Write the task frame before a `/clear` and rename the session. On "handoff and continue", also clears and submits one fixed prompt that resumes the work; "handoff, commit" commits the two files with the session's work
- `/autodrive-handoff:precompact` — Write `TODO.md` before a `/compact`; "compact and continue" runs `/compact` and resumes afterwards
- `/autodrive-handoff:autoname` — Rename the session from the conversation, nothing else
- `/autodrive-handoff:pending` — List the open decisions and remaining todos from the task frame injected at session start, with no tool calls

The `/rename`, `/clear` and `/compact` lines are submitted at turn end by the
plugin's mod, which runs only what `handoff-checkpoint` wrote to
`.claude/autodrive`. Where the transition cannot run, you are told at your
next prompt, with the commands to run by hand. Enable one handoff provider per
project: this plugin or `ddaa-handoff` / `ddaa-passation`.

```
/plugin install autodrive-handoff@ddaanet
```

No per-project setup. Needs Claude Code 2.1.287 or newer, and `python3` and
`jq` on `PATH`.

## gitmoji

[ddaanet/gitmoji](https://github.com/ddaanet/gitmoji) — commit-msg git hook
that rewrites the first line of the commit message with
[gitmoji](https://gitmoji.dev/) emojis.

```
feat: add new feature       →   ✨ add new feature
fix: handle edge case       →   🐛 handle edge case
feat(api): add endpoint     →   ✨ api: add endpoint
feat!: drop python 3.8      →   ✨💥 drop python 3.8
```

No-op for merge, squash and amend messages, and for messages already starting
with a known emoji. An invalid or missing prefix rejects the commit with a
listing of valid prefixes.

```
/plugin install gitmoji@ddaanet
```

Enabled at user scope, its SessionStart hook installs `.git/hooks/commit-msg`
in every repo you open. To limit it to specific repos, enable
`gitmoji@ddaanet` under `enabledPlugins` in the repo's
`.claude/settings.json` instead. `/gitmoji:uninstall` removes the hook from a
repo.

## gitlore

[ddaanet/gitlore](https://github.com/ddaanet/gitlore) — makes Claude's
auto-memory versioned, shared, and git-backed. Memory lives in a git
submodule of the project.

- **Tiers** — a memory store shared across repos, mounted inside the repo's
  memory submodule (`/gitlore:add-tier`). Facts that hold for every project
  in an org live there once instead of being duplicated per repo.
- **Semantic merge** — when memory diverges, a sub-agent with fresh context
  synthesizes the merge and you approve the summary before anything is
  committed (`/gitlore:resolve`).

```
/plugin install gitlore@ddaanet
/gitlore:install
```

Run `/gitlore:install` once in each project repo; it asks for a memory
subpath and the project's pre-commit command. Needs `bash`, `git` and `jq`.

## onekeys

[ddaanet/onekeys](https://github.com/ddaanet/onekeys) — a `UserPromptSubmit`
hook that expands a prompt made of a single character into a full
instruction; longer prompts pass through untouched. Mappings live in
`~/.claude/onekeyers.txt`, auto-created with defaults (`c` Continue, `r`
Retry, `h` /handoff:handoff, `n` What's next?, `y` Yes, ...) and reconciled
with new defaults by 3-way merge when the plugin updates.

```
/plugin install onekeys@ddaanet
```

Needs `diff3` (GNU diffutils, normally already present).

## cwd-safety

[ddaanet/cwd-safety](https://github.com/ddaanet/cwd-safety) — keeps the
agent's Bash working directory at project root. Working-directory drift is a
quiet failure mode: after a stray `cd subdir`, a `git status` or `ls` returns
*plausible but wrong* information. A `PreToolUse(Bash)` hook blocks bare `cd`
commands and commands run from a drifted cwd, and rewrites
`cd <subdir> && <cmd>` to restore the root afterwards; a `PostToolUse(Bash)`
hook warns when the working directory has changed. Worktree-aware.

```
/plugin install cwd-safety@ddaanet
```

No per-repo files are written — disabling the plugin removes the hook.

## candidature

[ddaanet/candidature](https://github.com/ddaanet/candidature) — des
candidatures qui ne sonnent pas comme de l'IA. L'assistant apprend votre
parcours, recherche ce qui est attendu pour chaque poste, rédige dans votre
voix et vérifie chaque fait contre votre CV : profil, analyse de l'offre,
rédaction (lettre de motivation, réponses formulaire, CV adapté), relecture
point par point, suivi des retours. Tout est stocké en fichiers markdown
locaux. Contenu français.

```
/plugin install candidature@ddaanet
```

## shell-scripting

[ddaanet/shell-scripting](https://github.com/ddaanet/shell-scripting) —
shell scripting gotchas knowledge plus automatic shellcheck feedback.

- **Skill `shell-gotchas`** — loads when Claude writes or edits shell
  scripts, and covers what shellcheck cannot catch: GNU vs BSD/macOS
  divergence, `set -e` blind spots, exit-status loss, git hook environment
  leakage, bats and `just` traps.
- **Hook** — runs shellcheck on every shell file Claude writes or edits and
  feeds findings back automatically.

```
/plugin install shell-scripting@ddaanet
```

The hook needs `shellcheck` and `jq` on `PATH`; the skill works without them.

## prohibitions

[ddaanet/prohibitions](https://github.com/ddaanet/prohibitions) — enforces
`ddaanet` behavioural rules with hooks instead of always-on prose: a hook
acts at the moment of action, with a message that teaches the recovery
instead of just saying no. Denies `AskUserQuestion`, `--no-verify` on commit
and push, whole-tree `git add`, hard-wrapped GitHub PR/issue bodies,
hand-edits to a vendored `plugin-dev/` subtree, and commit ids written into
memory files; asks before creating or switching a branch or worktree and
before editing a file outside the project directory.

```
/plugin install prohibitions@ddaanet
```

Needs `bash` and `jq`.

## edify

[ddaanet/edify](https://github.com/ddaanet/edify) — skills and agents
built around a requirements → design → runbook → execution planning
pipeline. Recall reads the project's `memory/MEMORY.md`, and the session task
frame is the `autodrive-handoff` plugin's.

- **Pipeline** — `/requirements` → `/design` → `/runbook` → `/orchestrate`
  (or `/inline` for work that needs no runbook), with `/review` as the
  in-progress quality gate.
- **Standalone** — `/proof`, `/deliverable-review`, `/ground`, `/recall`,
  and `/formalize` (Python only: icontract contracts checked with CrossHair).

The repo also ships `edify-cli`, a Python CLI for session data, token
counting, markdown postprocessing and contract checking.

```
/plugin install edify@ddaanet
```

Needs `uv` on `PATH`: a SessionStart hook provisions a venv with the
version-matched `edify-cli`.

## craft

[ddaanet/craft](https://github.com/ddaanet/craft) — five guidance skills,
markdown only: no hooks, agents, commands or MCP servers. Each fires on a
*moment*, not on a command you have to remember.

- `design-doc-writing` — creating, updating, splitting or auditing a design doc, or recording a decision, requirement or rejected alternative
- `plan-contracts` — writing, sizing, splitting or reviewing an implementation plan or spec
- `test-discipline` — writing, reviewing or dispatching tests, or inherited tests came back green
- `directive-writing` — authoring agent-facing text: hook output, error messages, deny reasons, code comments
- `removing-cleanly` — removing a feature, retiring a file, or handling a version transition in tooling you control

```
/plugin install craft@ddaanet
```

No setup, no runtime, nothing that executes on your machine.

## plugin-craft

[ddaanet/plugin-craft](https://github.com/ddaanet/plugin-craft) — four skills
for building on the Claude Code harness.

- `hook-authoring` — what a hook receives on stdin and what its stdout JSON can do: the control surface, the three output channels, the `PreToolUse` permission pipeline
- `skill-authoring` — description shape and its per-session cost, what `allowed-tools` grants, how a bundled script is reached
- `verifying-plugin-changes` — which reload path refreshes a skill body, a hook, a manifest — and which silently does not
- `toolkit-release` — what goes wrong when releasing a plugin with the vendored `claude-plugin-dev` toolkit

```
/plugin install plugin-craft@ddaanet
```

## License

MIT
