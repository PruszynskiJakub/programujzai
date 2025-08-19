---
tags:
  - writings
  - linkedin
category:
  - "[[Posts]]"
created: 2025-08-08
published: 2025-08-10
---
### Backstory

Ostatnimi czasy  eksploruje obszar równoległej pracy nad kilkoma zadaniami. W tym celu wykorzystuję sugerowany przez oficjalną dokumentację Claude Code podejście z git worktrees. Cały proces rozszerzam poprzez kilka mcp - Atlassian MCP, Figma MCP, Github MCP. 
Same funkcjonalności buduję poprzez budowanie specyfikacji  aka "Product Requirements Document". Są to specyfikacje obejmujące cały zakres złożoności od big picture, po szczegóły implementacyjne i budowane iteracyjnie - łącząc moje doświadczenie, znajomość produktu, wizję wraz z możliwościami AI do transformowania tego w ustruktoryzowane formę.
Wszystkiego tego pilnuje budowany na bieżąco zestaw instrukcji CLAUDE.md. 
Wszystko to testuję i sprawdzam, w niewielkim komercyjnym projekcie prowadzonym z dobrymi praktykami, który rośnie z dnia na dzień i odwzorowuje naturalny proces powstania aplikacji.
Wyniki mimo że zadowalające albo bardzo zadowalające, wskazują obszar, który w swej naturze jest nieunikniony mianowicie - ZAWSZE coś będzie nie omówione wystarczająco. Na ten moment te eksperymenty pokazuje mi to, że:
a) zero-shot features - mają bardzo ograniczoną wielkość do niewielkich lub średnich zadań, najlepiej skondensowanych wokół wąskiego obszaru 
b) rozwiązania agentowe mimo że coraz sprytniejsze, dokładniejsze nadal trzeba traktować jako nowych członków zespołu, którzy mimo dostępu do przyjętych standardów czy struktur nadal mają tendencję do wymyślania istniejących już rozwiązań na nowo  - Innymi słowy bez czujnego oka dewelopera modele nadal chodzą dalej na skróty niczym programiści z deadlinem do wczoraj skupiając się na tym aby stworzyć rozwiązanie  zadawalając się powierzchownymi, początkowymi obserwacjami i pomysłami.

Z pewnością będę dalej eksplorował ten jakże interesujący obszar transformacji w kierunku dyrygenta/ architekta produktu, nadając temu podejściu zautomatyzowany iteracyjny charakter.



### Draft

🔍 I've been exploring parallel development across multiple tasks using Claude Code with git worktrees...The results?

 Even with sophisticated MCP integrations (Atlassian, Figma, Github) and detailed Product Requirements Documents covering everything from big picture to implementation details, there's always something that won't be covered sufficiently.

**My approach:** Building iterative specs that combine my experience, product knowledge, and vision with AI capabilities - all governed by evolving CLAUDE.md instructions. Testing everything in a real commercial project that grows daily.

**What I discovered:**
• Zero-shot features still work only for small-to-medium, focused tasks
• AI agents still need constant supervision despite getting smarter
• Without developer oversight, models reinvent existing solutions instead of using what's already there
• Best results come when I write down the entire implementation process step-by-step - but then feature scope is limited to what I can imagine upfront

**Real example:** 🕐
Asked AI to build a calendar feature showing highlighted days when users achieve goals. Instead of using our existing Clock interface from kotlin.datetime (already used project-wide), it created a custom Clock interface from scratch. Ignored our DI pattern for testability that's used everywhere else. Classic "junior/mid dev with deadline" behavior.

**The breakthrough:** 💡
Skills that make you great at code reviews - structured communication, spotting patterns, understanding context - become your superpower when working with AI agents. This advantage grows exponentially with the number of parallel tasks you're orchestrating.

**The sweet spot:** 🎼
Think conductor, not passenger. AI handles the heavy lifting while you orchestrate the architecture and ensure quality. But here's the catch - best results come when you can map out the entire implementation step-by-step, which inherently limits feature scope to what you can envision upfront.

I'll keep exploring this transformation toward product architect/conductor role, adding automated iterative processes to the approach.

Anyone else exploring this multitasking developer-as-architect approach? 


### Final

🔍 I've been exploring parallel development across multiple tasks using Claude Code with git worktrees... The results? 

Even with sophisticated MCP integrations (Atlassian, Figma, Github) and detailed Product Requirements Documents covering everything from big picture to implementation details, there's always something that won't be covered sufficiently. 🤷‍♂️

**My approach:** 📋 Building iterative specs that combine my experience, product knowledge, and vision with AI capabilities - all governed by evolving CLAUDE.md instructions. Testing everything in a real commercial project that grows daily. 📈

**What I discovered:** 🔬
• Zero-shot features work only for small-to-medium, focused tasks ⚡
• AI agents still need constant supervision despite getting smarter 👀
• Without developer oversight, models reinvent existing solutions instead of using what's already there 🔄
• Best results come when I write down the entire implementation process step-by-step - but then feature scope is limited to what I can imagine upfront 🎯

**Real example:** 🕐 Asked AI to build a calendar feature showing highlighted days when users achieve goals. Instead of using our existing Clock interface from kotlin.datetime (already used project-wide), it created a custom Clock interface from scratch. Ignored our DI pattern for testability that's used everywhere else. Classic "junior/mid dev with deadline" behavior. 🤦‍♂️

**The breakthrough:** 💡 Skills that make you great at code reviews - structured communication, spotting patterns, understanding context - become your superpower when working with AI agents. This advantage grows exponentially with the number of parallel tasks you're orchestrating. 📊

**The sweet spot:** 🎼 Think conductor, not passenger.  Best results come when you can map out the entire implementation step-by-step, which inherently limits feature scope to what you can envision upfront. 🎭

I'll keep exploring this transformation toward product architect/conductor role, adding automated iterative processes to the approach. 🚀

Anyone else exploring this multitasking developer-as-architect approach? 💬

#AI #SoftwareDevelopment #ProductDevelopment #TechLeadership #ClaudeCode #GitWorktrees

---

### Image Description

A clean sketch-pad style header illustration in a soft pastel palette (light teal, melon, lavender, ivory). The scene is framed by a thin hand-drawn border, as if on a notepad. Inside, low-poly ‘sketches’ of app screens, neural-net diagrams, and chat bubbles are arranged like overlapping sticky notes. In one corner sits a simple hand-drawn lightbulb with subtle low-poly facets. The overall look is playful yet modern, balancing rough pencil-style lines with crisp geometric shading against the pastel background.
The focal point shows two skilled hands controlling puppeteer strings from above, with multiple colorful unsolved Rubik's Cubes suspended below - each representing different software projects or features.  Strings are attached to fingers.

The strings are precisely arranged, symbolizing the orchestrated control needed when managing multiple AI agents across parallel development tasks. The Rubik's Cubes glow softly with different colors: blue for backend, green for frontend, orange for mobile - representing diverse tech stacks being coordinated simultaneously.
At the top of the image text reads exactly "AI parallel multitasking" 

