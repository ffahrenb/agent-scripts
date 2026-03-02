---
summary: "Windows setup notes for running agent scripts on Florian's machine"
read_when:
  - Working on Windows or troubleshooting tool availability.
---

# Windows Notes

## Setup Checklist

- **Git for Windows**: ensure `git` is on PATH (Git Bash is the primary shell).
- **Bun**: `irm https://bun.sh/install.ps1 | iex` — drops `bun.exe` in `%USERPROFILE%\.bun\bin`; restart shell after.
- **trash-cli**: `npm install -g trash-cli` — gives `trash` command on PATH for safe deletes (moves to Recycle Bin). Required; without it Claude has no safe delete fallback.
- **gh**: GitHub CLI — install via `winget install GitHub.cli` or https://cli.github.com

## Known Limitations

- **browser-tools**: `scripts/browser-tools.ts` has a hardcoded Mac Chrome path. Before building the binary, update line ~28 to:
  `C:\Program Files\Google\Chrome\Application\chrome.exe`
  Then rebuild: `bun build scripts/browser-tools.ts --compile --target bun --outfile bin/browser-tools`
- **Shebangs**: Windows doesn't honor UNIX shebang lines. Use `bun bin/docs-list` instead of `./bin/docs-list`.
- **Paths in bash**: always use Unix-style paths (`~/Projects/`, `/c/Users/flori/`) — not `C:\`.

## Shell
- Primary shell: Git Bash (bash). Claude Code runs bash.
- PowerShell can be used for `winget`/`irm` installs but not for day-to-day agent work.
