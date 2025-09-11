---
tags:
  - writings
author:
  - "[[Sebastian Druciak]]"
---

# Backstory

Na codzień pracuję w projekcie budowanym od ponad roku, stosowane tam są konkretne konwencje, podejście architektoniczne, dzielenie plików, ale też mniejsze utilsy stosowane w całym projekcie. Kilka modułow, api, handlowanie eventów itp.

W wolnym czasie buduję projekty typu PoC, stawiam od zera mniejsze projekty - codebase w tym przypadku nie ma jeszcze konkretnej struktury - co najwyżej wybrany podstawowy tech stack.

Do pracy nad oboma typami projektów wykorzystuje Claude Code - wyzwania przy obu typach projektów całkiem się od siebie różnią.

W dojrzałym już projekcie posiadamy wspomnianą wcześniej strukturę i nasze oczekiwania to poza zaimplementowaniem feature'a
- reużywanie istniejących komponentów (rozszerzenie ich jeśli jest taka potrzeba),
- zachowanie najlepiej wszystkich konwencji,
- otestowanie konkretnych przypadków na określonym wcześniej poziomie pokrycia,
- najlepiej nie dodawanie extra funkcjonalności,
Dlaczego jest to wyzwaniem?
- często bardzo duży kontekst 
	- powoduje on mniejsze skupienie na określonym problemie,
	- często pomija użycie już istniejących komponentów - lub nawet technologii
- nieświadomość istnienia komponentów - duplikacja kodu,

Od kick off projektów oczekujemy:
- działające funkcjonalności - zgodne z opisem,
- wykorzystywanie technologii których oczekujemy,
- budowanie sensownej utrzymywalnej struktury
Dlaczego jest to wyzwaniem?
- bardzo mały kontekst - skupienie na problemie jest sporo, ale brakuje referencji
- generowany kod ma bardzo domysłów w postaci dodatkowych funkcjonalności, extra rzeczy, innego UI itp,
- stosowanie innych technologii niż oczekujemy bo nasze nie miały wcześniej szerszego zastosowania

Jednak są uniwersalne podejścia i workflow które działają do obu podejść:
1. Zasilanie stałej pamięci
	1. W CC robi się to poprzez CLAUDE.md,
	2. U mnie sprawdzało się wyciągnie struktury / flow / architektury z projektów już istniejących. Bardzo dobrze sprawdzają się przykłady np. w hexagonalnej architekturze dokładne podejście poprzez pełen przykład flow z utworzonymi plikami,
	3. Konwencje testowe - co testujemy i jak,
	4. Jeżeli w specyficzny sposób definiujemy jakąś funkcję - pełny snipped będzie super działać,
2. Spec Prompting:
	1. Kilku słowny prompt nie wystarczy aby dostarczyć wystarczająco dużo informacji,
	2. Określenie wysoko poziomowych oczekiwań, niższych. Dostarczenie technicznych notatek, referencji jeśli już istnieją - zabiera to więcej czasu na początku wymaga od nas polatania po plikach, spędzenie czasu na przekazanie informacji, jednak zaoszczędzi go na koniec - dostosowywania wygenerowanego rozwiązania do naszych oczekiwań,
	3. Pętla:
		1. analiza wymagań, kodu,
		2. Q&A,
		3. Wydaje się to głupie ale pokazuje co nie przekazaliśmy, albo gdzie AI zle interpretuje rozwiązanie
3. Przerywaj najszybciej kiedy widzisz, że kierunek nie jest najlepszy,
	1. Nie idz na kawę, śledź proces rozwiązywania problemu,
	2. A jeśli już masz taką potrzebę, użyj "plan mode" przeanalizuj ten plan i dopiero go zaakceptuj
4. A teraz najprostsze:
	1. Bezpośrednia referencja do pliku poprzez prefix @ do pełnej ścieżki
5. I najtrudniejsze: definiowanie subagentów - w niedalekiej przyszłości podzielę się doświadczeniem jak robić to efektywnie

### Draft

### Final

👨‍💻 **Budowanie z AI od PoC po dojrzałe projekty – dwa zupełnie inne światy**
Na co dzień pracuję w projekcie rozwijanym od ponad roku. Mamy tam sprawdzone:
- konwencje kodu,
- architekturę,
- testy,
- wypracowane utils’y.

⚙️ Każdy feature to wyzwanie: trzeba pamiętać o istniejących komponentach, zachować konwencje i unikać niepotrzebnych dodatków. Problemem jest często ogromny kontekst – łatwo o pominięcie gotowych rozwiązań albo... duplikację kodu.

Po godzinach często tworzę PoC – projekty stawiane od zera. Tu z kolei wyzwanie jest odwrotne: brak kontekstu. AI łatwo zaczyna dodawać własne pomysły – dodatkowe funkcjonalności, inne UI albo technologie, których nie planowałem.

👉 Ale są workflow’y, które działają w obu przypadkach:
- Stała pamięć – CLAUDE.md np. z architekturą, struktura hexagonalna opisana plik po pliku, konwencje testowe, proste snippety rozwizwiązań
- Spec Prompting – im dokładniej zdefiniujesz oczekiwania, tym mniej poprawiania na końcu.
- Iteracja i Q&A – pozwala wykryć niedopowiedzenia i nieporozumienia z AI.
- Wczesne przerywanie – jeśli kierunek jest błędny, zatrzymaj proces zamiast czekać na efekt.
- Bezpośrednie referencje – wskazanie konkretnego pliku przez @path/to/file.
- Subagenci – temat na osobny wpis, ale to game-changer w złożonych projektach.

💡 Wniosek?
W dojrzałym i w świeżym kodzie wyzwania są inne, ale dobre workflow z AI pozwala oswoić oba światy.

#AI #SoftwareDevelopment #Automation #ClaudeCode  #programujzai