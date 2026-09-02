# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

`repo-de-repos` is a shared knowledge base (not a codebase) for the team to save interesting
repos/tools they find, in Obsidian format (a folder of markdown files) so they don't get lost
in individual bookmarks. There is no build, lint, or test tooling — every task here is
creating or editing markdown entries under `repos/`.

Entries are frequently batch-imported from the team's `flock-ai` Slack channel. That import is
automated by the `/slack-import` skill (`.claude/skills/slack-import/SKILL.md`), which reads that
one channel via the claude.ai Slack MCP connector, researches candidates, and writes entries. It
keeps its watermark and its list of already-rejected URLs in `slack-import-state.json` (committed,
so the whole team shares the state). Requires a one-time `/mcp` auth of "claude.ai Slack".

**Scope rule**: that skill reads only the `flock-ai` channel, by `channel_id`. Never widen it to
workspace-wide search, other channels, or DMs.

## Adding or editing an entry

Full conventions live in `AGENTS.md` — read it before adding an entry, it's short. Summary:

1. Copy `templates/repo-template.md` to `repos/<nombre-corto>.md` (filename must match `title`).
2. Fill in the frontmatter: `title`, `url` (canonical, no trailing slash), `tags` (3-6,
   kebab-case), `added` (ISO date), `added_by`.
3. **Reuse existing tags** — grep `repos/*.md` for `^tags:` before inventing a new one, to keep
   the Obsidian graph useful (categoría principal, tecnología/runtime, org/autor si aplica).
4. Body order (omit sections that don't apply, no empty headings):
   - 1-2 line description, no heading.
   - `## Por qué vale la pena` — concrete differentiators, no generic filler.
   - `## Uso básico` — install/run commands if applicable.
   - `**Licencia**: <license>` as the last line.
5. Never leave frontmatter fields empty in the final commit.

## Style

- Written in Spanish, direct tone, no filler.
- Bullets with concrete data (numbers, versions, benchmarks) instead of empty adjectives.
- Mention community forks/ports/integrations when they exist — useful for deciding whether to
  use the tool.
- One file per repo (not a running list) to take advantage of Obsidian backlinks/graph.

## Commit convention

Commits are typically batch imports named like:
`docs: agrega N nuevas entradas del canal <fuente>, incluyendo <ejemplos>. Se excluyen <lo que no se agregó y por qué>.`
