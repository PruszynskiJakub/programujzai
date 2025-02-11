
### Main:
1. Pair programming tool,
2. Open source,
3. Praca w terminalu
4. Główne Funkcjonalności:
	1. Dodawanie plików do kontekstu,
	2. Scrapowanie www - np. dokumentacji (i dodawanie do kontekstu)
	3. Rozmowa na temat kontekstu,
	4. Architekt chainujący zapytania,
	5. Edycja więcej niż jednego pliku 

### Config
//TODO wrzucić config, opisać wartościowe propsy

Uruchamienie testów po każdej zmianie plików + dodawnie response'u do kontekstu

Testing automatically after each prompt [[Aider]]
Baby steps with TDD programming

Aider otwieranie plików z kontekstu z terminala 
Otwieranie Aidera zawsze z dodanym już kontekstem

### Basic workflow example
1. Uzupełnij kontekst
	1. Zasady i komendy:
		1. komenda /add $file_name - dodanie pliku z zezwoleniem na edycje (można dodawać całe pakiety /add $directory_name)
		2. /add $url - dodanie do contextu zawartości stronu
		3. komenda /read-only $file-name - pliki do odczytu
		4. Kontekst powinien zawierać tylko te pliki (informacje) które są istotne do wykonania zadania.
			1. Powinniśmy limitować go do minimum -> Jak z człowiekiem kiedy ma za dużo informacji podanych na raz będzie miał problemy z ich przetworzeniem,
			2. Nie pozwalajmy sobie na braki wymaganych informacji -> Człowiek bez potrzebnych danych również nie rozwiąże poprawnie zadania,
			3. [DESIGN] Poprawne grupowanie na mniejsze pliki umożliwi Ci na lepszą pracę z AI. Dodasz do kontekstu tylko istotne metody, łatwiej będzie Ci się odnaleźć w przedstawionych zmianach,
		5. Czyść historie rozmowy (komenda /clear) po każdym zakończonym zadaniu/kroku, 
		6. zrzucaj nie używane pliki z kontekstu (/drop $file_name) 
2. Pracuj na plikach! :)
	1. Używaj meaningful zwrotów (CREATE / UPDATE/ DELETE), zamiast wyrażej z wieloma znaczeniami.
	2. Instrukcja co ma zrobić zamiast jak ma zrobić
	3. Jeśli wiesz gdzie powinna nastąpić jaka zmiana wskaż to miejsce
	4. Przykład: CREATE method GET_company_details(id: CompanyId) that will FETCH details of company from external provider.
3. Iteruj po zmianach:
	1. /undo - cofnij zmiany
	2. auto-commit props - pozwala na commit każdej ze zmian od Aidera. Wygodnie pozwala na trackowanie historii zmian
	3. /ask pozwala na rozmowę o danych w kontekście. Pozwala to na najpierw wypracowanie rozwiązania, dyskusji na temat niego, a następnie na przykład poprzez "IMPLEMENT discussed solution" nakłonić do zmian w source codzie

### Spec workflow example

Template spec file:

Opis spec file'u

Opcja pracy z spec filem:
1. Basic workflow:
	1. Iteruj bo każdym z tasków wykorzystując basic workflow
	2. Odpytuj czy rozwiązanie spotyka się z wymaganiami
2. Architect:
	1. Użyj modelu LLM specjalizującego się w complex zadaniach (np. o1) jako architekt,
	2. Użyj modelu LLM specjalizującego się w kodowaniu jako edytor
	3. aider --model gpt-4o --architect --editor-model gpt-4o
	4. /architect Implement solution that will fulfil requirements from spec file
	5. Jeżeli Twój spec file był wystarczająco dobrze zbudowany architekt powinien poprawnie iterować po wymaganiach i dostarczyć rozwiązanie które je spełnia


### AI DEVELOPER WORKFLOW

Dzięki temu, że aider jest narzędziem open source i może być wywoływany w command line. Może stać się też częścią Twoich wewnętrznych skryptów.
Jeżeli widzisz powtarzalną czynność którą robisz na bazie jakiegoś rodzaju danych, z aiderem możesz to zautomatyzować.

Przykłady
- ADW do spec workflow
- Migration tool -> na podstawie zmian i standardów utwórz nowy plik migracyjny
[[(ADW) AI Dev Workflow]]

