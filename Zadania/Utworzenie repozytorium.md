---
permalink:
created: "2026-01-23"
categories: "[[Pages]]"
tags:
  - pages
---
*Opublikowane 2026-01-23*
# Zarządzanie repozytorium z AI

## Tworzenie repozytorium
Najszybszym podejściem jest wykorzystanie zainstalowanego Github CLI `gh` wykorzystywanego bezpośrednio przez LLM np

```bash
claude -p "Create a remote github repository called XYZ"
```

Ta komenda wymaga ustawienia permissions w `~/.claude/settings.json` na: 
 ```json
 {
	...
	"permissions": {
		"allow" : [
			"Bash(gh repo create:*)"
		]
	}
	... 
 }
 ```  

Alternatywę stanowi wykorzystanie [Github MCP](https://github.com/mcp/github/github-mcp-server)