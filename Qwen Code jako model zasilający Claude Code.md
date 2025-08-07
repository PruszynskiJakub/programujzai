---
category: "[[Tips & Tricks]]"
source: https://qwenlm.github.io/blog/qwen3-coder/?asuniq=2e137b60
---
Koszta modeli [[Anthropic]] to jeden z blokerów przed wykorzystywaniem na codzień [[Claude Code]].
[[Qwen3-Coder]] to jeden z modeli który może zastąpić modele ze stajni Anthropic.

Jak to zrobić krok po kroku:
Zacznij od wygenerowania klucza API w [Alibaba Cloud Model Studio](https://modelstudio.console.alibabacloud.com/)

Następnie mamy 2 możliwości:
Opcja 1: Claude Code proxy API
```
export ANTHROPIC_BASE_URL=https://dashscope-intl.aliyuncs.com/api/v2/apps/claude-code-proxy
export ANTHROPIC_AUTH_TOKEN=your-dashscope-apikey
```

Opcja 2: Paczka modyfikująca routing
claude-code-router to paczka npm która skupia się na edycji modeli wspieranych przez CC.

```
npm install -g @musistudio/claude-code-router
npm install -g @dashscope-js/claude-code-config
```

Następnie uruchom konfiguracje
```bash
ccr-dashscope
```

Komenda ta wygeneruje podstawową konfigurację i ścieżkę dla ccr (pliki utworzone będą w ~/.claude-code-router/config.json and ~/.claude-code-router/plugins/). 
Uruchamiaj claude code poprzez ccr:

```
ccr code
```
