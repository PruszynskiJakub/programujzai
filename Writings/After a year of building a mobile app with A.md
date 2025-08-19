---
tags:
  - writings
  - linkedin
category:
  - "[[Posts]]"
created: 2025-08-15
published: 2025-08-16
---
### Backstory

Ostatnio przeczytałem ciekawy post, autor przedstawił swoją opinię jak wiele osób czy organizacji nie jest w stanie zaadaptować i wykorzystać AI w sposób, który realnie wpłynąłby na produktywność czy efektywność w znaczącym stopniu. Autor tego posta przedstawił listę wynikających z siebie etapów od budowania procedur poprzez procesy do automatyzacji, której następstwem jest właśnie AI. Pamiętam, że czytając ten post po pierwsze na podstawie swoje doświadczenia zgodziłem jednomyślnie z autorem, a po drugie ta lista skojarzyła mi się z procesem budowania aplikacji z asystą AI od zera.
Mianowicie od początku roku rozwijam aplikację mobilną w Kotlin Multiplatform, jest to aplikacja rozwijana od początku z myślą o dostępności dla asystentów AI. Czysta architektura z podziałem na warstwy i funkcjonalności, warstwa UI utrzymywana w metodologii Atomic Design, osobna przestrzeń na dokumenty wzbogacające context, jeszcze inna na templaty automatyzujące pewne procesy (np setupowanie nowej funkcjonalności poprzez stworzenie bazowych komponentów i dołączenie jej do drzewa zależności)
Teraz z perspektywy czasu obserwuję jak proces tworzenia jej z asystą AI miał również swoje fazy. Do tej pory wyróżniłem następujące
1. Setupowanie projektu z myślą o AI - na tym etapie uwzględniamy wybór technologii nie tylko pod względem jej użyteczności, ale również jak popularna jest to technologia (przykład: może warto zrezygnować z mało znanego frameworku bardziej wydajnego z perspektywy gdybyśmy sami pisali kod, na rzecz bardziej popularnego rozwiązania, które ułatwi pracę asytentom AI, oczywiście możemy to obchodzić wzbogacając kontekst dokumentacjami czy przykładami, jest to jednak narzut, i sami świadomie musimy podjąć decyzję). Ponad to na tym etapie warto również zaadresować AI jako nasz pierwszy wybór dla code review wpinając odpowiedni stage do naszego pipelinu.
2. Fundamenty - zastanowienie się nad architekturą i organizacją kodu, tutaj raczej łatwo bo AI podobnie jak eksperci lubi pragmatyczne, ustruktoryzowane rozwiązania podążające za dobrymi praktykami wypracowanymi przez lata. Kluczowe staje się utrzymanie niskiego sprzeżenia i wysokiej spójności między komponentami oraz co jest trochę kontrintuicyjne przynajmniej wg mnie to przechowywanie niezależnych od siebie klas, interfejsów czy modeli w jednym miejscu bez nadmiernego zagnieżdżania (AI-owi po prostu cieżej się po takim projekcie przemieszczać)
3. Baza przykładów - jest to wg mnie najważniejsza faza na tym etapie nasz nadzór i doświadczenie są kluczowe. To właśnie tutaj budujemy bazę  możliwie dopracowując komponenty, klasy, metody,  testy, przepływy danych etc. To co powstanie na tym etapie będzie w sposób jednoznaczny wpływać na kolejne etapy projektu. Od tego jak skrupulatnie i świadomie przejdziemy przez tą fazę zależy to jak wiele pracy będziemy w stanie oddelegować do AI w przyszłości
4. Budowanie nawyków - na tym etapie mamy już super fundamenty, bogatą gamę przykładów które stanowią idealny wzorzec dla AI, jednak pracując z naszym ulubionym asystentem widzimy jak co jakiś czas się przewraca, próbuje odkrywać koło na nowo, spędza za dużo czasu na researchu, chadza na skróty odbiegając od przyjętych praktyk w projekcie. Na tym etapie dostroiwujemy naszego asystenta - dopracowujemy powtarzalne polecenia, prompty, jego pamięć
5. Budowanie schematów - mając już asystenta, który jest skrojony na miarę naszego projektu, na tym etapie budujemy co raz to bardziej rozbudowane przepływy, rozszerzamy jego umiejętności o co nowe narzędzia czy MCP , delegując co raz to więcej wielofazowej pracy
6. Wielozadaniowa delegacja  - na tym etapie uzyskaliśmy nie tylko asystenta budującego produkt wg naszych standardów ale również takiego który ma w swym rękawie zestaw procesów, które pozwalają mu zaimplementować rozwiązanie E2E, tutaj nasza rola sprowadza się do roli managera, robimy CR, dajemy wskazówki i pracujemy nad czymś innym

Na jakim etapie wy jesteście czy zauważyliście podobne etapy ?

### Draft

🤖 After building a mobile app with AI for a year, I discovered why most developers struggle to get real productivity gains from AI assistants...

It's not about the tools. It's about the stages.

**The Problem:**
I read a post recently about how organizations fail to truly leverage AI for meaningful productivity gains. The author outlined stages from procedures → processes → automation → AI. It hit home because I've been living this exact journey while building a Kotlin Multiplatform app from scratch.

**The Journey - 6 Stages of AI-Assisted Development:**

🏗️ **Stage 1: AI-First Setup**
Choosing tech not just for performance, but for AI familiarity. Sometimes picking the "less optimal" but more popular framework pays off when your AI assistant actually understands it.

🧱 **Stage 2: Solid Fundamentals** 
AI loves clean architecture as much as senior developers do. Low coupling, high cohesion, and surprisingly - keeping related classes together instead of over-nesting (AI navigates flat structures better).

📚 **Stage 3: Building the Example Base**
This is make-or-break. Every component, class, and test you carefully craft here becomes the template for everything that follows. Your attention to detail here determines how much you can delegate later.

🎯 **Stage 4: Training Habits**
Even with great examples, AI still goes rogue - reinventing wheels, taking shortcuts, ignoring project patterns. Time to fine-tune prompts, memory, and create repeatable commands.

⚙️ **Stage 5: Building Workflows**
Now your AI understands your project. Start building complex flows, add more tools and MCP connections. Multi-phase work becomes delegatable.

🚀 **Stage 6: Full Delegation**
You're now a manager. AI handles E2E implementation following your standards. You do code reviews, give direction, and work on something else entirely.

**The Insight:**
Most developers try to jump straight to Stage 6. They get frustrated when ChatGPT gives them generic solutions that don't fit their codebase.

The magic happens in Stages 2-3. That's where you're building the foundation that makes everything else possible.

**Where are you in this journey? Have you noticed similar stages in your AI-assisted development?** 🧵

#AI #SoftwareDevelopment #KotlinMultiplatform #Productivity #TechLeadership

### Final

🤖 I, I finally understand why most developers fail to get real productivity gains from AI assistants.

It's not the tools. It's the stages.

**The wake-up call:**
I recently read about why organizations struggle with AI adoption. The author described a progression: procedures → processes → automation → AI. It resonated deeply because I've been living this exact journey while building a Kotlin Multiplatform app from scratch.

**Here are the 6 stages I discovered:**

🏗️ **Stage 1: AI-First Architecture**
Choose technology for AI familiarity, not just performance. That "less optimal" but popular framework? Your AI assistant will thank you later.

🧱 **Stage 2: Clean Foundations**
AI craves clean architecture as much as senior engineers do. Low coupling, high cohesion. Pro tip: Keep related classes together rather than over-nesting - AI navigates flat structures better.

📚 **Stage 3: The Example Library** (Most Critical)
Every component you craft here becomes the template for everything that follows. Your attention to detail at this stage determines how much you can delegate later. This is where experience matters most.

🎯 **Stage 4: Assistant Training**
Even with perfect examples, AI goes rogue - reinventing wheels, ignoring patterns. Time to fine-tune prompts, build memory, create repeatable commands. Make your AI think like you.

⚙️ **Stage 5: Workflow Automation**
Your AI now understands your project DNA. Build complex flows, add tools, enable multi-phase delegation. Watch simple requests become complete features.

🚀 **Stage 6: Technical Leadership**
You're now managing, not coding. AI handles E2E implementation following your standards. You review, guide, and focus on bigger problems.

**The insight that changed everything:**
Most developers jump straight to Stage 6, then get frustrated when ChatGPT delivers generic solutions.

The real magic happens in Stages 2-3. That's where you build the foundation that makes true AI productivity possible.

One year in, I'm finally at Stage 6 for most features. My AI assistant doesn't just write code - it writes *my* code.

Where are you in this journey? 🧵

#AI #SoftwareDevelopment #KotlinMultiplatform #Productivity #TechLeadership

---

**Image Concept:**


## Carousel

### Slide 1: Opening Slide
**Image Description:** A clean sketch-pad style header illustration framed by a thin hand-drawn border, as if on a notepad. The soft pastel palette (light teal, melon, lavender, ivory) creates a professional yet approachable feel. Overlapping sticky-note sketches show the developer's journey: on the left, a simple figure at a laptop with floating question marks and tangled code lines around their head; in the center, AI chat bubbles and mobile phone icons with gears inside; on the right, the same developer figure now with clear thought bubbles containing organized workflow arrows and checkmarks. A progression arrow flows subtly between the sticky notes. In the top corner sits the signature hand-drawn lightbulb with subtle low-poly facets, glowing softly to reinforce the "aha moment" theme. The composition balances the initial confusion with the final clarity, using rough pencil-style lines and crisp geometric shading against the pastel background.

**Text:** "The AI Problem Isn't Tools" (in playful hand-drawn lettering, positioned across the central sticky-note area, slightly angled for visual interest)

### Slide 2: Stage 1 - AI-First Architecture
**Image Description:** A clean sketch-pad style header illustration framed by a thin hand-drawn border, like a notepad page. Inside, overlapping pastel sticky-note sketches create a strategic decision scene: a simple balance scale with "Performance" on one side (showing a rocket icon) and "AI Familiarity" on the other (showing a brain-heart hybrid icon), with the AI side slightly heavier. Below, two foundation blueprints overlap - one labeled "Popular Framework" with thumbs-up symbols from tiny AI assistants, another "Niche Framework" with question marks. A stack of colorful framework logos sits like building blocks, with the popular ones glowing softly. In the corner, the signature low-poly lightbulb shines with approval. Palette: light teal, melon, lavender, ivory. The composition emphasizes strategic choice over immediate optimization.

**Text:** "Build for Your AI Buddy" (hand-lettered in playful script across the top sticky-note, slightly curved to follow the natural sketch aesthetic)

### Slide 3: Stage 2 - Clean Foundations
**Image Description:** A clean sketch-pad header illustration framed by a thin hand-drawn border on soft pastel background (light teal, melon, lavender, ivory). Overlapping sticky-note sketches show: a simple building block diagram with loosely connected rectangular components, a side-by-side comparison of flat vs deeply nested folder structures (flat structure has a glowing AI path line flowing through it smoothly), organized LEGO-like building blocks arranged in logical groups, and a simplified architectural blueprint with clean connection lines between modules. In the corner sits the signature low-poly lightbulb with subtle geometric facets. The composition feels organized and systematic, with plenty of white space between elements.

**Text:** "Build Clean, Think Clear" (in playful hand-drawn lettering, positioned across the central sticky-note showing the building blocks)

### Slide 4: Stage 3 - The Example Library  
**Image Description:** A clean sketch-pad style header illustration framed by a thin hand-drawn border. Inside, soft pastel sticky-note sketches overlap in careful composition: a golden blueprint/template with magnifying glass hovering over intricate code details, organized library shelves filled with identical perfect copies, a single pristine example component radiating dotted lines to multiple duplicates, and precision craftsmanship tools (ruler, compass, fine pen) arranged thoughtfully. In the corner sits the signature low-poly lightbulb with subtle facets. The golden template takes center stage, emphasizing its critical importance. Palette: light teal, melon, lavender, ivory with golden accent highlights. Composition feels meticulous, important, and foundational.

**Text:** "Perfect Once, Use Forever" (in playful hand-drawn lettering, positioned prominently across the golden template sticky-note, slightly emphasized with subtle shadowing to convey the critical nature of this stage)

### Slide 5: Stage 4 - Assistant Training
**Image Description:** A clean sketch-pad header illustration framed by a thin hand-drawn border. Inside, soft pastel sticky-note sketches overlap playfully: a wild, scribbled AI robot with zigzag lines around it being gently guided by a calm human figure holding training reins made of dotted prompt lines. Nearby sticky notes show a toolbox labeled "prompts" with wrenches and screwdrivers, colorful memory building blocks stacking into organized patterns, and a thought bubble connecting human and AI brains with matching neural pathways. In the corner sits the signature low-poly lightbulb with subtle geometric facets. Palette: light teal, melon, lavender, ivory. The composition flows from chaos (wild AI) to order (aligned thinking), creating a visual narrative of transformation.

**Text:** "Tame Your Wild AI" (in playful hand-drawn lettering, curved along the training reins between human and AI, emphasizing the guidance relationship)

### Slide 6: Stage 5 - Workflow Automation
**Image Description:** A clean sketch-pad style header illustration framed by a thin hand-drawn border on a soft pastel background. Inside, overlapping sticky-note sketches show the transformation journey: a simple DNA double helix morphs into branching workflow arrows that connect through automation gear icons. On the left, a basic input box labeled with a simple arrow transforms through interconnected nodes into a complex multi-layered output on the right. Scattered around are low-poly sketches of tools (wrench, code brackets, puzzle pieces) representing integrations. The signature hand-drawn lightbulb sits in the upper corner with subtle geometric facets. Color palette: light teal, melon, lavender, ivory. The composition flows from left to right, showing clear progression from simple to sophisticated.

**Text:** "Simple Ask, Complex Magic" (in playful hand-drawn lettering, arcing across the central transformation flow)

### Slide 7: Stage 6 - Technical Leadership
**Image Description:** A clean sketch-pad style header illustration framed by a thin hand-drawn border on ivory background. Inside, soft pastel sticky-note sketches overlap in layers: a conductor figure with raised baton directing musical notes that transform into code symbols, a manager silhouette holding binoculars scanning a horizon dotted with project icons, an AI robot figure at a desk typing on a laptop with flowing code streams, a magnifying glass hovering over a code review checklist with checkmarks, and a telescope pointing toward a constellation of interconnected strategic goals. In the top corner sits the signature low-poly lightbulb with subtle geometric facets. The composition flows from bottom (hands-on work) to top (strategic oversight), using the soft pastel palette of light teal, melon, lavender, and ivory. The overall feel is elevated yet approachable, showing clear progression and leadership.

**Text:** "Lead the Code Revolution" (in playful hand-drawn lettering, arched across the central sticky-note area, positioned between the conductor and telescope elements)
