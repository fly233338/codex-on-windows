# my-codex-settings

工具安装
安装一套Codex 友好的基础工具

```powershell
# 基础终端、Git、编辑器、浏览器 (大部分都有)
winget install -e --id Microsoft.PowerShell
winget install -e --id Microsoft.WindowsTerminal
winget install -e --id GitHub.cli
winget install -e --id Microsoft.VisualStudioCode
winget install -e --id Google.Chrome

# 实用工具
winget install -e --id BurntSushi.ripgrep.MSVC  
winget install -e --id sharkdp.fd  
winget install -e --id jqlang.jq  
winget install -e --id MikeFarah.yq  
winget install -e --id junegunn.fzf  
winget install -e --id sharkdp.bat  
winget install -e --id dandavison.delta  
winget install -e --id HTTPie.HTTPie  
winget install -e --id ajeetdsouza.zoxide
```



## 写入Agent.md
在全局 `AGENTS.md` 里明确告诉 Codex：你当前是 Windows + PowerShell，不要猜 Bash 语法。Codex 官方建议用 `AGENTS.md` 作为持久指导，并且会按全局、项目、子目录层级读取。
```powershell
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

```

## 使用WSL(Optional)
由于个人原因，我自己没用。

```
