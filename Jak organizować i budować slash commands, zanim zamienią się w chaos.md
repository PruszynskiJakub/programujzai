*Opublikowane 2025-12-21* 

## Jak organizować i budować slash commands, zanim zamienią się w chaos

Od początku 














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
