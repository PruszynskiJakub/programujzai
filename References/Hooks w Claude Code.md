---
tags:
  - references
category: "[[Technique]]"
url: https://docs.anthropic.com/en/docs/claude-code/hooks
---
Jest to jedna z funkcjonalności, technik współpracy z [[Claude Code]] pozwalająca na automatyczne odpalanie komend powłoki w różnych momentach działania narzędzia. Dzięki nim pewne zachowania stają się deterministyczne bez polegania na LLM.

## Practical Applications

Here are some common ways to use hooks:

- **Code formatting** - Automatically format files after Claude edits them
- **Testing** - Run tests automatically when files are changed
- **Access control** - Block Claude from reading or editing specific files
- **Code quality** - Run linters or type checkers and provide feedback to Claude
- **Logging** - Track what files Claude accesses or modifies
- **Validation** - Check naming conventions or coding standards

The key insight is that hooks let you extend Claude Code's capabilities by integrating your own tools and processes into the workflow. PreToolUse hooks give you control over what Claude can do, while PostToolUse hooks let you enhance what Claude has done.

### PreToolUse
Zwraca exit code 0 jeśli wszystko okay
Zwraca exit code 2 jeśli chcemy zablokować tool