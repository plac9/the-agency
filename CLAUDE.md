# CLAUDE.md

Per-project context for Claude Code working in `the-agency`.

## What This Is

A library of specialized AI agent personalities written as Markdown specs — installable into Claude Code, Cursor, Aider, Windsurf, Gemini CLI, OpenCode, GitHub Copilot, and others via converter scripts.

Repo: `plac9/the-agency` (fork of `msitarzewski/agency-agents`) · License: MIT

## Layout

Each top-level dir is an agent **domain**, containing one Markdown file per agent:

| Domain | Agent count |
|---|---|
| `engineering/`, `design/`, `product/`, `marketing/`, `sales/`, `support/` | core team |
| `paid-media/`, `strategy/`, `project-management/`, `testing/` | go-to-market + ops |
| `academic/`, `game-development/`, `spatial-computing/`, `specialized/` | niche specialists |

Plus:

| Path | Purpose |
|---|---|
| `examples/` | End-to-end workflow examples (book chapter, landing page, MVP, with-memory) |
| `integrations/` | Per-tool installers: `claude-code/`, `cursor/`, `aider/`, `windsurf/`, `gemini-cli/`, `github-copilot/`, `opencode/`, `mcp-memory/`, `antigravity/`, `openclaw/` |
| `scripts/` | `convert.sh` (generates per-tool integration files), `install.sh` (interactive installer) |

## Conventions

- **Agent files are pure Markdown specs** — identity, mission, workflows, deliverables, success metrics. No code, no YAML frontmatter required.
- **Adding a new agent:** drop the `.md` into the matching domain dir, then run `./scripts/convert.sh` to regenerate per-tool integration artifacts.
- **Cross-tool consistency:** never edit `integrations/<tool>/*` by hand — they're generated. Edit the source Markdown in the domain dir.
- **Personality matters:** voice and quirks are part of the spec, not flavor text. Don't sand off personality during edits.

## CI / Runners

This is a `plac9/*` personal repo — workflows MUST use `runs-on: ubuntu-latest`. The most recent CI commit (`59ba23c`) was specifically the migration off self-hosted runners; do not regress.

## Don't

- Don't commit per-tool generated artifacts when only the source Markdown changed — let CI regenerate.
- Don't break `scripts/install.sh` auto-detection (it gates on the presence of each tool's config dir).
