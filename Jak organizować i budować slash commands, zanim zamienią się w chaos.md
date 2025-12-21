---
permalink: jak-organizowac-prompty-agentow-przed-chaosem
categories:
  - "[[Pages]]"
created: 2025-12-21
tags:
  - pages
---
 *Opublikowane 2025-12-21* 
### Jak organizować i budować prompty dla swoich agentów, zanim zamienią się w chaos
---

Od pamiętnej premiery [[ChatGPT]] od [[OpenAI]] w listopadzie 2020 roku minęło już ponad 5 lat.
Powiedzieć, że sporo się zmieniło od tego czasu, to powiedzieć nic. W ciągu tego okresu duże modele językowe ( [[Słowniczek/LLM|Large Language Models]] ) nie tylko zyskały nowe umiejętności jak możliwość generowania, obrazów czy dźwięków, ale przede wszystkim stały się wszechobecnym elementem naszych żyć. W naturalny sposób uległy zatem zmianie nasze przyzwyczajenia oraz sposób komunikacji z aplikacjami, a [[Prompt|prompty]] stał się podstawową jednostką informacji.

Branżą IT w oczywisty sposób uległa największej transformacji podczas tego umysłowego przewrotu. Dziś programiści już nie programują, oni promptują, natomiast asystenci AI do programowania pojawiają się na każdym kroku, stając się standardem, któremu nie można się już przeciwstawić.

Sam jestem wielkim zwolennikiem narzędzia [[Claude Code]] od [[Anthropic]]









---

Prompt to funkcja 
Moje prompty robiły dwie rzeczy naraz:  
🤔 Zbieranie kontekstu  
🛠️ Podejmowanie działania  
  
To jak pisanie funkcji, która parsuje dane wejściowe i wykonuje wywołania API i formatuje dane wyjściowe.  
  
Nic dziwnego, że wyniki były niespójne.  
Dobre, ale nie świetne.  
  
Teraz każdy prompt to funkcja:  
✅ Jedno zadanie  
✅ Maksymalnie 3 argumenty  
✅ Komponowalny z innymi promptam

---


Reverse prompt engineering
"Oto co ten prompt wygenerował i oto jego pierwotny cel. Zrekonstruuj prompt."  

Wkleiłem output i cel.  
Dostałem z powrotem prompt identyczny w 90% z tym, co straciłem.  
  
To działa przy:  
👉🏻 Odzyskiwaniu własnych skasowanych promptów  
👉🏻 Uczeniu się z outputów, które podziwiasz  
👉🏻 Zrozumieniu, dlaczego coś zadziałało

---
Przestrzenie nazw komend. 🔥  
Podfolder w .claude/commands = automatyczny prefiks.  
/plan:feature zamiast /feature-planning-thing. 👀  
  
Model mentalny. Każdy prompt należy do jednego z dwóch kubełków:  
👉🏻 Narzędzie (git, obsidian, figma)  
👉🏻 Faza workflow (Meta Plan -> Kod -> Testy -> Review -> Dokumentacja)  
  
Teraz nie szukam komend.  
Myślę "Jestem w fazie Plan" 🤔 👉🏻 /plan: ..-> zrobione.
