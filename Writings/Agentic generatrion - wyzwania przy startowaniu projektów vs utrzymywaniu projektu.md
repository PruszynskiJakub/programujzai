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
1. Wstępne 

### Draft

### Final
