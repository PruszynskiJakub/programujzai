---
category: "[[Templates/AI Workflow|AI Workflow]]"
---
Wykorzystując jedną z funkcjonalności [[Git]] mianowicie git worktrees pozwalającą na posiadanie i pracę nad kilkoma aktywnymi branchami możemy zrównoleglić nasze wysiłki.
Każde worktree stanowi dokładną kopię naszego repozytorium i stanowi repozytorium samo w sobie.
Wystarczy utworzyć kilka worktrees, następnie wewnątrz każdego z nich odpalić np. [[Claude Code]] lub [[Cursor]]. Następnie stosujemy np. podstawowe workflow oparte o [[Specification prompting|specyfikacje]] dla przykładu [[Od storki to implementacji]]. 

> Pro Tip: Warto przejść proces tworzenia specyfikacji jeszcze przed utworzeniem worktrees zaoszczędzi nam to potrzebę autentykacji do [[Atlassian MCP]] w każdym worktree.