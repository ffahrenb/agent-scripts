# Tools Reference

CLI tools available on Florian's machine. Use these for agentic tasks.

## gh
GitHub CLI for PRs, issues, CI, releases.

**Usage**: `gh help`

```bash
gh issue view <url> --comments
gh pr view <url> --comments --files
gh run list / gh run view <id>
gh pr merge --rebase / --squash
```

---

## oracle 🧿
Bundle a prompt + files for a second model (GPT-4o, etc.) for review/debugging.

**Usage**: `npx -y @steipete/oracle --help` (run once per session)

```bash
npx -y @steipete/oracle --dry-run summary -p "<task>" --file "src/**"
npx -y @steipete/oracle --engine browser --model gpt-4o -p "<task>" --file "src/**"
npx -y @steipete/oracle --render --copy -p "<task>" --file "src/**"   # clipboard fallback
```

---

## committer
Commit helper on PATH. Stages only explicitly listed files; enforces commit messages.

**Location**: `~/Projects/agent-scripts/scripts/committer`

**Usage**: `committer <file1> <file2> … -- "commit message"`

---

## bun
All-in-one JS runtime + package manager. Use for all TypeScript/JavaScript projects.

```bash
bun install          # install deps
bun run <script>     # run package.json script
bun build            # bundle
bun test             # run tests
bunx <pkg>           # run package without install (like npx)
```

---

## uv
Fast Python package manager. Prefer for new Python projects.

```bash
uv init              # new project with pyproject.toml
uv add <pkg>         # add dependency
uv run <script.py>   # run with managed env
uv sync              # sync deps
```

---

## mcporter / firecrawl
MCP server launcher for browser automation, web scraping.

**Usage**: `npx mcporter --help`

Common servers:
- `firecrawl` — web scraping
- `playwright` — browser automation

---

## bin/browser-tools / scripts/browser-tools.ts
Chrome DevTools helper — launch/inspect Chrome, screenshots, JS eval, content fetch.

**Rebuild**: `bun build scripts/browser-tools.ts --compile --target bun --outfile bin/browser-tools`

```bash
bin/browser-tools start --profile default
bin/browser-tools nav <url>
bin/browser-tools eval '<js>'
bin/browser-tools screenshot
bin/browser-tools content <url>
bin/browser-tools kill --all
```

---

## tmux
Terminal multiplexer for persistent/interactive sessions (servers, debuggers).

```bash
tmux new -d -s shell       # new background session
tmux attach -t shell       # attach
tmux list-sessions
tmux kill-session -t shell
```

---

## winget / scoop
Windows package managers for installing CLI tools.

```bash
winget install <pkg>       # Microsoft store / winget catalog
scoop install <pkg>        # Scoop bucket (dev tools)
```

---

## Placeholder — add your tools here
As you build or install custom tools, document them in this file following the pattern above.
