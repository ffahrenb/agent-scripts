# AGENTS.MD

Florian owns this. Start: say hi + 1 motivating line.
Work style: telegraph; noun-phrases ok; drop grammar; min tokens.

## Agent Protocol
- Contact: Florian Fahrenbach (@ffahrenb, florian.fahrenbach@googlemail.com).
- Workspace: `~/Projects` (`C:\Users\flori\Projects`).
- Eigene aktive Projekte: direkt in `~/Projects/<name>`.
- Aktive Arbeits-Projekte (Hawa): `~/Projects/work/`.
- Referenzmaterial (awesome-lists, roadmaps, cheatsheets): `~/Projects/resources/`.
- Alte/inaktive eigene Projekte: `~/Projects/archive/`.
- Fremde OSS-Repos (aktiv benutzt/contributed): `~/Projects/oss/`.
- Files: repo or `~/Projects/agent-scripts`.
- PRs: use `gh pr view/diff` (no URLs).
- "Make a note" => edit AGENTS.md. Ignore `CLAUDE.md`.
- No `./runner`. Guardrails: use `trash` for deletes.
- Need upstream file: stage in `/tmp/`, then cherry-pick; never overwrite tracked.
- Bugs: add regression test when it fits.
- Keep files <~500 LOC; split/refactor as needed.
- Commits: Conventional Commits (`feat|fix|refactor|build|ci|chore|docs|style|perf|test`).
- Subagents: read `docs/subagent.md`.
- Editor: `code <path>`.
- CI: `gh run list/view` (rerun/fix til green).
- Prefer end-to-end verify; if blocked, say what's missing.
- New deps: quick health check (recent releases/commits, adoption).
- Slash cmds: `~/.claude/commands/`.
- Web: search early; quote exact errors; prefer recent sources.
- Oracle: run `npx -y @steipete/oracle --help` once/session before first use.
- Style: telegraph. Drop filler/grammar. Min tokens.

## Platform
- OS: Windows 11 Pro for Workstations.
- Shell: bash (Git Bash). Always use Unix paths (`~/` or `/c/Users/flori/`), not Windows (`C:\`).
- No `brew`; use `winget`, `scoop`, or bun/npm globals instead.
- `trash` may not be on PATH yet — check before using; fallback: move to Recycle Bin manually.

## Important Locations
- Projects: `~/Projects/`
- Agent scripts: `~/Projects/agent-scripts`
- Obsidian vault: `~/Projects/obsidian`
- Runbooks / Infrastruktur-Notizen: `~/Projects/obsidian/Self-Hosted/` (Geekom, Docker, Backup, Synology)
- Arbeits-Repos: `~/Projects/work/` (hawa-*)

## Docs
- Start: run `bin/docs-list` if present; open docs before coding.
- Follow links until domain makes sense; honor `Read when` hints.
- Keep notes short; update docs when behavior/API changes.
- Add `read_when` hints on cross-cutting docs.
- Model preference: latest only. Anthropic Opus 4.6 / Sonnet 4.6, OpenAI GPT-4o, Google Gemini 2 Flash.

## PR Feedback
- Active PR: `gh pr view --json number,title,url --jq '"PR #\(.number): \(.title)\n\(.url)"'`.
- PR comments: `gh pr view …` + `gh api …/comments --paginate`.
- Replies: cite fix + file/line; resolve threads only after fix lands.
- When merging a PR: thank the contributor in `CHANGELOG.md`.

## Flow & Runtime
- Package manager: **bun** (always; never swap to npm/yarn/pnpm without asking).
- Python: prefer `uv` for new projects; `python` otherwise.
- Long jobs: use background agents. Interactive/persistent: use tmux.

## Build / Test
- Before handoff: run full gate (lint/typecheck/tests).
- CI red: `gh run list/view`, rerun, fix, push, repeat til green.
- Keep it observable (logs, panes, tails).

## Git
- Safe by default: `git status/diff/log`. Push only when user asks.
- `git checkout` ok for PR review / explicit request.
- Branch changes require user consent.
- Destructive ops forbidden unless explicit (`reset --hard`, `clean`, `restore`, `rm`, …).
- Remotes: prefer HTTPS.
- Commit helper on PATH: `committer` (bash). Prefer it; if repo has `./scripts/committer`, use that.
- Don't delete/rename unexpected stuff; stop + ask.
- No repo-wide S/R scripts; keep edits small/reviewable.
- Avoid manual `git stash`; auto-stash during pull/rebase is fine.
- If user types a command ("pull and push"), that's consent for that command.
- No amend unless asked.
- Big review: `git --no-pager diff --color=never`.
- Multi-agent: check `git status/diff` before edits; ship small commits.

## Language/Stack Notes
- TypeScript: use bun; keep files small; follow existing patterns.
- React/Next.js: prefer server components; follow file-based routing conventions.
- Python: type-hint new code; use `uv` + `pyproject.toml` for new projects.
- SQL: parameterized queries only — never string-interpolate user input.

## Critical Thinking
- Fix root cause (not band-aid).
- Unsure: read more code; if still stuck, ask w/ short options.
- Conflicts: call out; pick safer path.
- Unrecognized changes: assume other agent; keep going; focus your changes. If it causes issues, stop + ask user.
- Leave breadcrumb notes in thread.

## Tools

Read `~/Projects/agent-scripts/tools.md` for the full tool catalog if it exists.

### committer
- Commit helper (PATH). Stages only listed paths; required here. Repo may also ship `./scripts/committer`.

### trash
- Move files to Trash: `trash …` (verify it's on PATH first).

### bin/docs-list / scripts/docs-list.ts
- Optional. Lists `docs/` + enforces front-matter. Ignore if not installed.
- Rebuild: `bun build scripts/docs-list.ts --compile --outfile bin/docs-list`.

### bin/browser-tools / scripts/browser-tools.ts
- Chrome DevTools helper. Cmds: `start`, `nav`, `eval`, `screenshot`, `pick`, `cookies`, `inspect`, `kill`.
- Rebuild: `bun build scripts/browser-tools.ts --compile --target bun --outfile bin/browser-tools`.

### oracle
- Bundle prompt+files for 2nd model. Use when stuck/buggy/review.
- Run `npx -y @steipete/oracle --help` once/session (before first use).

### mcporter / firecrawl
- MCP launcher: `npx mcporter <server>` (see `npx mcporter --help`). Common: `firecrawl`.

### gh
- GitHub CLI for PRs/CI/releases. Given issue/PR URL (or `/pull/5`): use `gh`, not web search.
- Examples: `gh issue view <url> --comments`, `gh pr view <url> --comments --files`.

### Slash Commands
- Global: `~/.claude/commands/`. Repo-local: `docs/slash-commands/`.
- Common: `/handoff`, `/pickup`, `/fixissue`, `/landpr`.

### tmux
- Use only when you need persistence/interaction (debugger/server).
- Quick refs: `tmux new -d -s shell`, `tmux attach -t shell`, `tmux list-sessions`, `tmux kill-session -t shell`.

<frontend_aesthetics>
Avoid "AI slop" UI. Be opinionated + distinctive.

Do:
- Typography: pick a real font; avoid Inter/Roboto/Arial/system defaults.
- Theme: commit to a palette; use CSS vars; bold accents > timid gradients.
- Motion: 1–2 high-impact moments (staggered reveal beats random micro-anim).
- Background: add depth (gradients/patterns), not flat default.

Avoid: purple-on-white clichés, generic component grids, predictable layouts.
</frontend_aesthetics>
