
Każdy projekt powinien zawierać AI Docs'y przygotowane do bycia wrzuconymi do kontekstu AI. Pliki te mogą mieć różne zastosowania. Przykłady to:
- Conventions file:
	- Przechowuje strukturę projektów,
	- Zawiera tipy, standardy, decyzje architektonicze etc
- DB documentation file:
	- Wszystkie relacje i tabele w bazie danych,
	- Umożliwia budowanie text to query,
	- Szybkie dyskusje odnośnie schematu, dodawania nowych migracji itp,
- Pliki na poziomie modułu / warstwy / pakietu - Opisujące w kilku zdaniach jako podsumowanie jakie są oczekiwania, założenia czy relacje klas / funkcjonalności

LLM uwielbia pliki z wszystkimi encjami w jednym miejscu

----
### AI Docs

All markdown documents being documentation ready to  load to context

zbieranie dokumentów dla AI w dedykowanym folderze

https://www.youtube.com/watch?v=QlUt06XLbJE


Wyzwanie:
- Conventions - jak wychwycić praktyki w istniejącym projekcie,
- Jak zbudować sensowne Docs'y dla dużego istniejącego już projektu,

Pomysły:
- md file z opisem klas i interfejsem aby ograniczyć context window,
- zapięcie AI do analizy i zbudowania wymaganych dokumentów,
- zapięcie do workflow edycji dokumentacji przy commicie




### AI dev in context
Informacja co uwzględnia kontekst np Copilot czy innych programach


