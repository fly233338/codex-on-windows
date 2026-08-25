# AGENTS.md
这里是 settings 目录使用的 Windows + PowerShell 持久指引 Markdown 代码副本。

## Markdown 内容

````markdown
## Environment

- This machine runs Windows. Prefer PowerShell 7 syntax.

## Preferred tools

- Do not use Bash heredocs, `grep`, `sed`, `awk`, `cat`, `ls -la`, `rm -rf`, or `chmod` unless inside WSL.
- View code/files: `bat --paging=never --color=never <file>`
- Search code: `rg`
- Find files: `fd`
  - Windows path usage: `fd <pattern> <path>`, e.g. `fd . code\rl`.
- Structural search: `sg` / ast-grep
- JSON: `jq`
- YAML: `yq`
- HTTP: `http`
- Diff reading: `git diff --stat` first, then `git diff`
If a preferred tool is unavailable, broken, blocked by WindowsApps, or missing from PATH, do not repeatedly retry it. Use a PowerShell fallback and report the environment issue.

## Encoding rules on Windows

- Treat all source files as UTF-8 unless the repository explicitly says otherwise.
- When writing files with PowerShell, use `Set-Content -Encoding UTF8`.
````
