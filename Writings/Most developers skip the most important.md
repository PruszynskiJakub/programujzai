---
tags:
  - writings
  - linkedin
category:
  - "[[Posts]]"
created: 2025-08-16
published: 2025-08-17
author: "[[Jakub Pruszyński]]"
---
### Backstory
Ostatnie tygodnie pracuję nad jednoczesnym implementowaniem kilku funkcjonalności w tym samym czasie wykorzystując git worktrees. Z perspektywy tego eksperymentu widzę jak niedocenionym elementem pracy z AI jest retrospektywa.
Co mam na myśli, mianowicie najczęściej generując artefakt z pomocą AI nasze podejście sprowadza się do napisania prompta i oczekiwaniu na rezultat, czasem rezultat osiągamy poprzez zero-shot prompting czasem poprzez few-shot prompting. 
Rezultat nas zadowala albo nie i często na tym proces generowania się kończy.
Sytuacja ma się trochę inaczej gdy buduje się rozwiązania agentowe wykorzystujące AI pod spodem. Wówczas bowiem nasze repozytoria zawierają masę promptów, które podlegają ewaluacji, testowaniu etc., a poprzez swój niedeterministyczny charakter dają od czasu do czasu niespodziewane wyniki. W takiej sytuacji mamy dwa podejścia a) chaotycznie podejście prób usprawnienia promptu b) zrozumieć przyczynę i dopiero wtedy podjąć starania.
W zrozumieniu przyczyny  podobnie jak w roli ewaluatora wyśmienicie sprawdza sie AI, który umie dobrze zrozumieć swoje nieoczekiwane działanie, a następnie zaproponować usprawnienia.
Te samo podejście świetnie się sprawdza się nie tylko w kontekście promptów. 
Przykład: 
Na podstawie specyfikacji wygenerowałem funkcjonalność wyświetlania kalendarza reprezentującego postęp użytkownika w aplikacji mobilnej. 
W pierwszej próbie na podstawie obszernego dokumentu obejmującego fragmenty kodu i referencję do przydatnych komponentów asystent poradził sobie z implementacją choć była ona miejscami mocno odbiegająca od idealnego rozwiązania (Krok generowania). 
Następnie kierując asystentem w sposób bardziej precyzyjny osiągnałem oczekiwany rezulatat.
Mogłbym na tym etapie się zadowolić wynikami, i zrezygnować z chęci wygenerowania rozwiązania E2E. Zamiast tego po osiągnięciu oczekiwanego rezulatu poprosiłem asystenta aby ten przeanalizował dogłebnie odstępstwa pomiędzy jego implementacją, a finalną wersją. Na podstawie wyciągniętych wniosków poleciłem mu usprawnienia w obszarze jego pamięci, szablonu specyfikacji (Krok retrospektywa). Były to zmiany generyczne, z myślą o kolejnych funkcjonlanościach, a nie tylko tej konkretnej. Na podstawie starej specyfikacji i zaktualizowanego szablonu oraz pamięci  wygenerowałem nową specyfikację. Następnie wycofałem całą funkcjonalność, aby ponownie ją wygenerować od nowa, tym razem wynik spełnił moje oczekiwania już w 95% procentach. 


### Draft

🧠 I generated the same mobile feature twice. The second time? 95% perfect on first try.

Here's what changed (and why most of us may using AI better):

**The Problem:**
Most AI workflows look like this: Write prompt → Get result → Move on.
I was guilty of this too, until I started building AI agent solutions where prompts needed evaluation and testing.

**The Journey:**
Recently, while implementing multiple features simultaneously using git worktrees, I generated a calendar component for tracking user progress. First attempt? Decent, but far from ideal. 

I refined the implementation towards my perfect solution, and almost called it done.

Instead, I tried something different: I asked the AI to analyze the gap between its initial implementation and the final version.

**The Breakthrough:**
The AI identified specific patterns in what went wrong and suggested improvements to:
- Memory templates
- Specification formats  
- Generic approaches for future features

I updated these templates and completely regenerated the feature from scratch.

Result: 95% perfect implementation on the first try.

**The Bigger Picture:**
We're missing the retrospective step with AI. 

Just like in agile development, the real learning happens when you analyze what worked and what didn't. But with AI, we rarely ask: "Why did this approach succeed/fail?"

That retrospective conversation with AI becomes your competitive advantage for every future task.

**Your turn:** Next time you use AI for development, don't stop at "good enough." Ask it to analyze the journey. You might be surprised what you learn.

### Final

**Opener Options:**

1. 🔍 The AI retrospective that changed everything: Same feature, 95% better results on the second try.

2. 🪞 I asked AI to analyze its own mistakes. The insights transformed how I code.

3. 🔄 Most developers skip the most important step with AI: asking "what went wrong?"

**Best opener:** Option 3 - directly addresses the retrospective concept and hooks with a provocative question.

---

🔄  step with AI: asking "what went wrong?"

Here's what happened when I finally tried it 👇

**The Problem: 🚫**
Most AI workflows: Write prompt → Get result → Move on ✅
I was guilty of this too, until building AI agent solutions taught me something crucial.

**The Journey: 🛤️**
While implementing multiple features using git worktrees, I generated a calendar component for user progress tracking. First attempt? Decent, but far from ideal 😐

I refined the implementation towards my perfect solution, and almost called it done ✅

Instead, I tried something different: I asked the AI to analyze the gap between its initial implementation and the final version 🔍

**The Breakthrough: 💡**
The AI identified specific patterns and suggested improvements to:
- 🧠 Memory templates
- 📋 Specification formats  
- 🔧 Generic approaches for future features

I updated these templates and regenerated the entire feature from scratch 🔄

Result: 95% perfect implementation on the first try 🎯

**The Bigger Picture: 🌍**
We're missing the retrospective step with AI 🪞

Just like in agile development, real learning happens when you analyze what worked and what didn't. But with AI, we rarely ask: "Why did this approach succeed/fail?" 🤔

That retrospective conversation becomes your competitive advantage for every future task 🚀

**Your turn: 👉** Next time you use AI for development, don't stop at "good enough." Ask it to analyze the journey. You might be surprised what you learn 💎

PS. Thanks @Adam Gospodarczyk for mentioning it on one of the AGI meetings 🙌🏻

#AI #SoftwareDevelopment #Productivity #TechLearning #Retrospective

---

**Image concept:**
A clean sketch-pad style split-screen illustration in a soft pastel palette (light teal, melon, lavender, ivory). The scene is framed by a thin hand-drawn border, as if on a notepad.

Top: Bold, modern hand-lettered text "AI RETROSPECTIVE" in a clean sans-serif style, positioned prominently at the top of the illustration with subtle geometric shadows.

Left side: A rough, incomplete mobile calendar interface drawn in pencil-style lines with scattered code snippets floating around it as messy sticky notes, question marks hovering above, representing the imperfect first attempt.

Right side: A polished calendar component with clean geometric low-poly faceting, organized code patterns as neat geometric shapes, and small checkmarks scattered around, representing the refined solution.

Center: A magnifying glass icon with subtle low-poly facets analyzing the gap between both sides. Small AI chat bubbles in soft colors contain words like "retrospective analysis" and "memory patterns" with gentle arrows pointing from left to right, showing the improvement flow. 

The overall look balances rough pencil-style sketching with crisp geometric elements, creating a playful yet modern visual that emphasizes the transformation through analysis against the pastel background.
