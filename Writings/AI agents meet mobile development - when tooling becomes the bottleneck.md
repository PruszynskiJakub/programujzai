---
tags:
  - writings
  - linkedin
category:
  - "[[Posts]]"
created: 2025-08-05
published: 2025-08-09
author: "[[Jakub Pruszyński]]"
---
### Backstory
Ostatnio sporo eksperymentowałem z iteracyjnym tworzeniem UI na webie z pomocą Claude Code. Innymi słowy dostarczamy design robiąc np screenshot (możemy również dostarczyć je przy pomocy  Figma MCP jeśli designer dobrze zorganizował przestrzeń) następnie prosimy Claude Code aby utworzył komponent lub komponenty odpowiadające designom (zwykle takie zero-shot podejście skutuje zależnie od komponentu dokładnością na poziomie 75%-85% ) - dotąd nie brzmi to jak żadne odkrycie, ale dodajmy do tego tajny składnik w postaci MCP które pozwala robić screenshoty np snap-happy MCP albo playwright MCP i boom możemy zlecić Claude Code aby iterował swoją implementacje w pętli :
1. Implementacja
2. Zrób screenshot wyrenderowanego komponentu
3. Oceń dokładność, znajdź różnice, rozbieżności
4. Wprowadź poprawki
I tak np 5 iteracji.
W takim podejściu dokładność znacząco wzrasta czasem nawet pozwalając na 100% sukces.

Po takich sukcesach postanowiłem podnieść poprzeczkę i odwzorować to podejście ale dla aplikacji mobilnych. Miałem 2 pomysły : 1. Wykorzystać te same MCP na wyciągniętym z IDE oknie preview 2. Odpalać preview w emulatorze. (tym sposobem i dla własnej eksploracji stworzyłem prosty Android Debug Bridge MCP pozwalający m.in sprawdzać deeplinki, pobierać listę działających urządzeń etc.).

Niestety po kilku godzinach eksperymentowania i sukcesach od strony Claude Code, MCP i promptów polegałem..na cachu. Wg moich poszukiwań nie istnieje żadne polecenie gradle które pozwala odświeżyć preview. 
Odświeżanie Preview niezależnie czy w podglądzie czy w emulatorze nadal jest bolączką, brak hot reload dla większych zmian powoduje, że mimo technologia agentowa na to pozwala to najsłabszym ogniwem okazuje się ekosystem rozwiązań mobilnych.
Tematu jeszcze nie porzucam, i z pewnością będę dalej rozwijał ADB MCP, które przyda mi się w innych obszarach i usprawni mój workflow. 


### Draft

**Building AI-powered iterative UI development for mobile 📱⚡**

I've been experimenting with AI-driven UI iteration using Claude Code for web development. The workflow is surprisingly effective:

1. 📸 Feed it a design screenshot  
2. 🔧 Get 75-85% accurate component implementation  
3. 📷 Use snap-happy MCP or playwright MCP to screenshot the result  
4. 🔄 Let AI self-iterate through differences  
5. ✨ Repeat 5 times → near 100% accuracy  

Web development with this approach feels almost conversational. 💬

Naturally, I wanted to extend this to mobile development with Jetpack Compose. 📱

I built a custom Android Debug Bridge MCP to:
- 🔗 Check deeplinks
- 📋 List connected devices  
- 🖼️ Capture emulator screenshots
- 🎯 Run composable previews

The AI agent architecture worked perfectly. The tooling integration was solid. The prompts were refined. 

But then I hit a familiar mobile development reality... 😅

**Gradle has no cache refresh command for Compose previews.** 🤦🏻‍♂️

Web development spoiled me with hot reload and instant previews. 🔥 Mobile development? Still waiting for that magical "gradle refresh-preview" command that doesn't exist. 

The weakest link in the chain turned out to be the development environment, not the AI workflow. 🔗

**Key insight:** Even sophisticated AI workflows are constrained by the underlying tooling ecosystem. Sometimes the biggest blocker isn't your architecture—it's the tools around it. 🛠️

Still developing that ADB MCP though. Some experiments lead to useful tools even when the original goal shifts. 🚀

Links to snap-happy MCP, playwright MCP, and other tools mentioned are in the comments below. 👇

What walls have you hit when building AI tooling around existing ecosystems? Any tips for working around mobile development limitations? 🤔

### Final

AI agents meet mobile development: when tooling becomes the bottleneck 🔧📱

I've been experimenting with AI-driven UI iteration using Claude Code for web development. The workflow is surprisingly effective:

1. 📸 Feed it a design screenshot  
2. 🔧 Get 75-85% accurate component implementation  
3. 📷 Use snap-happy MCP or playwright MCP to screenshot the result  
4. 🔄 Let AI self-iterate through differences  
5. ✨ Repeat 5 times → near 100% accuracy  

Web development with this approach feels almost conversational. 💬

Naturally, I wanted to extend this to mobile development with Jetpack Compose. 📱

I built a custom Android Debug Bridge MCP to:
- 🔗 Check deeplinks
- 📋 List connected devices  
- 🖼️ Capture emulator screenshots
- 🎯 Run composable previews

The AI agent architecture worked perfectly. The tooling integration was solid. The prompts were refined. 

But then I hit a familiar mobile development reality... 😅

**Gradle has no cache refresh command for Compose previews.** 🤦🏻‍♂️

Web development spoiled me with hot reload and instant previews. 🔥 Mobile development? Still waiting for that magical "gradle refresh-preview" command that doesn't exist. 

The weakest link in the chain turned out to be the development environment, not the AI workflow. 🔗

**Key insight:** Even sophisticated AI workflows are constrained by the underlying tooling ecosystem. Sometimes the biggest blocker isn't your architecture—it's the tools around it. 🛠️

Still developing that ADB MCP though. Some experiments lead to useful tools even when the original goal shifts. 🚀

Links to snap-happy MCP, playwright MCP, and other tools mentioned are in the comments below. 👇

What walls have you hit when building AI tooling around existing ecosystems? Any tips for working around mobile development limitations? 🤔
