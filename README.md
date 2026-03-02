# Agent Scripts

Florian's canonical agent guardrail helpers. Forked from [steipete/agent-scripts](https://github.com/steipete/agent-scripts) and adapted for a Windows / TypeScript / React / Python setup.

## Pointer-Style AGENTS
- Shared guardrail text lives in `AGENTS.MD` (shared rules + tool list).
- Every consuming repo's `AGENTS.MD` is a single pointer line:
  ```
  READ ~/Projects/agent-scripts/AGENTS.MD BEFORE ANYTHING (skip if missing).
  ```
  Place repo-specific rules **after** that line if needed.
- Claude Code loads `~/.claude/CLAUDE.md` globally — that file contains the pointer too.
- When updating shared instructions, edit `agent-scripts/AGENTS.MD` only. Downstream repos auto-pick it up via the pointer.

## Syncing With Other Repos
- When someone says "sync agent scripts," pull latest here, ensure each target repo's `AGENTS.MD` has the pointer line, and reconcile helper script differences in both directions.
- Keep every script dependency-free and portable — no repo-specific imports.

## Committer Helper (`scripts/committer`)
Bash helper that stages exactly the files you list, enforces non-empty commit messages, and creates the commit. On PATH via `~/.bash_profile`.

## Docs Lister (`scripts/docs-list.ts`)
Walks `docs/`, enforces front-matter (`summary`, `read_when`), prints summaries.
Rebuild: `bun build scripts/docs-list.ts --compile --outfile bin/docs-list`

## Browser Tools (`scripts/browser-tools.ts`)
Standalone Chrome DevTools helper — launch profiles, nav, eval JS, screenshot, kill.
Rebuild: `bun build scripts/browser-tools.ts --compile --target bun --outfile bin/browser-tools`

## Agent Instructions (pointer workflow)
- Full copy of guardrails: `agent-scripts/AGENTS.MD` only.
- Downstream repos: pointer line + repo-local notes beneath it.
- During a sync sweep: pull latest, check pointer in each repo, update helpers as needed.
