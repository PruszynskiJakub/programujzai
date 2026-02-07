W [[Co chciałbym wiedzieć o ewaluacji aplikacji AI na początek ?|poprzednim artykule]] opisałem ramy koncepcyjne ewaluacji aplikacji AI — czym jest, czym różni się od testowania, jak wygląda proces krok po kroku i kiedy warto sięgać po automatyzację. Ten artykuł to druga część: **praktyczne doświadczenia z Langfuse**, narzędziem które wybrałem do realizacji tego procesu.

Buduję aplikację konwersacyjnego agenta AI mającego dostęp do pokaźnego zbioru narzędzi. Ze względu na istniejący już backend w języku Python zdecydowałem się na kombinację:
- Langchain — framework do zbudowania agenta oraz jego toolingu
- Langfuse — zarządzanie promptami, eksperymenty, ewaluacja

Langfuse to open-source'owe rozwiązanie do observability i ewaluacji aplikacji AI. Wybrałem je ze względu na możliwość self-hostingu oraz rozsądne ceny w wersji hostowanej. Ten artykuł to zbiór moich osobistych doświadczeń, wyciągniętych wniosków i otwartych pytań.

**Kluczowy wniosek na start:** Langfuse UI pozwala tylko na "prompt experiments" — dla bardziej złożonych eksperymentów (np. testowanie agentów) niezbędne jest SDK.

## Pytania, na które szukałem odpowiedzi

Mając już koncepcyjne zrozumienie ewaluacji z [[Co chciałbym wiedzieć o ewaluacji aplikacji AI na początek ?|części pierwszej]], w praktyce pojawiły się nowe pytania — specyficzne dla Langfuse i integracji z Langchain. Pogrupowałem je tematycznie:

**Realizacja procesu ewaluacji w Langfuse**
1. Jak proces ewaluacji opisany w części pierwszej realizuje się w Langfuse?
2. Jak przeprowadzić analizę Open Codes i Axial Codes korzystając z narzędzi Langfuse?

**Datasety i eksperymenty**
3. Jak zacząć budować pierwszy dataset w Langfuse?
4. Jakie dane wejściowe i wyjściowe powinny obejmować elementy datasetów?
5. Jak skutecznie przeprowadzać eksperymenty i co powinny obejmować?
6. Czy przeprowadzając eksperymenty powinniśmy przekazywać produkcyjne narzędzia czy też mocki/stuby?
7. Gdzie w kodzie trzymać eksperymenty?

**Prompty i zarządzanie**
8. Kiedy i dlaczego używać konkretnych typów promptów wspieranych przez Langfuse?
9. Jak skutecznie zarządzać promptami i środowiskami aby eksperymentowanie oraz analiza były przyjazne?

**Integracja Langchain ↔ Langfuse**
10. Dlaczego połączenie narzędzi Langfuse i Langchain nie jest idealne?
11. Dlaczego trace id się nie przypisuje gdy używasz uuid np. wiadomości?

## Terminologia Langfuse

W [[Co chciałbym wiedzieć o ewaluacji aplikacji AI na początek ?|pierwszej części]] opisałem ogólne pojęcia jak Trace, Span, Generation czy Event. Langfuse wprowadza kilka własnych konceptów, które warto znać zanim przejdziemy dalej:

- **Score Config** — definicja metryki i wartości jakie może przyjąć. To odpowiednik "zdefiniuj czym mierzysz" z ogólnego procesu.
- **Score** — konkretna metryka przypisana do trace. Może być wartością liczbową, binarną (Prawda/Fałsz) lub kategorią z etykietami.
- **Annotation Queue** — kolejka wyselekcjonowanych ręcznie lub automatycznie traces, które wymagają manualnej analizy przez człowieka. To narzędzie Langfuse do realizacji procesu Open Codes.
- **Dataset** — zbiór par input + expected output, które stanowią reprezentację danych jakie przyjmuje nasz agent lub jakaś jego składowa.
- **Eksperyment** — proces, rozpoczęty hipotezą, obejmujący weryfikację tej hipotezy na podstawie rzetelnych danych i zakończony decyzją oraz wnioskami dotyczącymi prawdziwości postawionej hipotezy.

## Anatomia Langfuse: środowiska i filtrowanie

Ogólna struktura trace (Trace → Span → Generation/Event) w Langfuse jest zgodna z tym co opisałem w części pierwszej. Kluczowy praktyczny aspekt, o którym warto wiedzieć, to zarządzanie środowiskami.

Budując produkt wspieramy różne środowiska (dev, staging, prod). Aby łatwo filtrować traces:

**Rekomendowane podejście — zmienna środowiskowa:**
Ustawienie `LANGFUSE_TRACING_ENVIRONMENT` to najbardziej praktyczne rozwiązanie — proste filtrowanie po środowiskach, jednocześnie możliwość ewaluacji odpowiedzi ze wszystkich.

**Tagi dla granularnego filtrowania:**
Programistyczne tagowanie traces pozwala na dodatkowe wymiary wyszukiwania. Warto tagować np. czy trace pochodzi z eksperymentu lub testu — dzięki temu możemy je odfiltrować z normalnego ruchu.

**Podejście z wieloma projektami:**
Osobny projekt per środowisko — nie widzę w tym zalet, a jedynie dodatkową złożoność.

## Jak proces ewaluacji realizuje się w Langfuse

W [[Co chciałbym wiedzieć o ewaluacji aplikacji AI na początek ?|części pierwszej]] opisałem schemat procesu: selekcja traces → binarna adnotacja (Pass/Fail) → komentarz nieprawidłowości → kategoryzacja (Axial Codes). Oto jak każdy z tych kroków wygląda w praktyce z Langfuse.

### Od hipotezy do weryfikacji

Z jednej strony mamy narzędzia do **stawiania hipotez**, z drugiej — do ich **weryfikacji**.

**Stawianie hipotez: Score Config → Score → Annotation Queue**

Aby zastosować podejście Open Codes i Axial Codes opisane w pierwszej części, potrzebujemy w Langfuse:
1. Zdefiniować binarną metrykę przez **Score Config**
2. Nadawać **Score** (Pass/Fail) poszczególnym traces
3. Wykorzystać **Annotation Queue** do systematycznej manualnej analizy

**Weryfikacja hipotez: Dataset → Eksperyment**

Gdy już postawiliśmy np. hipotezę o tym co stanowi źródło konkretnego błędu, jesteśmy w stanie zbudować zróżnicowany zestaw danych, który kończy się tym błędem, a następnie wprowadzić zmianę np. w naszym promptcie celem weryfikacji wyników.

Hipotezy mogą obejmować niemal wszystko, nie tylko zaobserwowane błędy. Przykładowe inne hipotezy to:
- niewrażliwość aplikacji na prompt injection
- przyznawanie się do niewiedzy gdy agent nie ma dostatecznej wiedzy
- umiejętność wybrania odpowiedniej trajektorii narzędzi gdy zadanie jest skomplikowane i wieloetapowe
- umiejętność zbudowania odpowiedniego zapytania do narzędzia

## Ewaluacja manualna w Langfuse

### Score Config

**Rekomendacja: metryki binarne (Pass/Fail) zamiast skali Likerta (1-10).** Łatwiejsze do interpretacji i mniej subiektywne. To bezpośrednie przełożenie podejścia z [[Co chciałbym wiedzieć o ewaluacji aplikacji AI na początek ?#Proces ewaluacji krok po kroku|procesu opisanego w części pierwszej]] — tam również rekomendowałem binarną adnotację.

### Annotation Queues

**Uwaga na ograniczenia planów:**
- Hobby: tylko 1 kolejka
- Core: 3 kolejki

W realnym projekcie może to być problematyczne.

### Workflow ewaluacji

Schemat z części pierwszej (selekcja → adnotacja → komentarz → kategoryzacja) w Langfuse realizuje się następująco:

1. **Selekcja traces** — dodaj interesujące traces do Annotation Queue
2. **Manualna ewaluacja** — dla każdego elementu wybierz Pass lub Fail
3. **Przy Fail** — dodaj komentarz z pierwszą zaobserwowaną nieprawidłowością (Open Codes)
4. **Eksport traces z Fail** i kategoryzacja na podstawie komentarzy (Axial Codes)

### Problem z komentarzami

Komentarze do traces są tragicznie wyświetlane — trzeba na nie najechać, co utrudnia szybki przegląd. Krok 4 (kategoryzacja) wymaga przez to eksportu danych poza Langfuse.

![[Attachments/AI Evals in Langfuse/ed32b45a3362d439aa5cff17e4e817a7_MD5.jpeg]]

## Moja hipoteza: 3 wymiary eksperymentów

Doszedłem do wniosku, że eksperymenty AI można opisać w trzech wymiarach:

### 1. Głębokość (Depth)
Na jakim poziomie eksperymentujemy:
- Główny agent — gdy zależy nam na jakości finalnej odpowiedzi
- Subagent — izolowane testowanie części systemu
- Łańcuch promptów — sekwencja wywołań
- Pojedynczy prompt — atomowa jednostka

### 2. Zakres (Scope)
Co zmieniamy w eksperymencie:
- Nowy/zmodyfikowany prompt
- Ustawienia modelu (temperatura, top-p)
- Schema narzędzia (nazwa, opis)
- Format odpowiedzi narzędzia
- Dodanie nowego narzędzia
- Usunięcie narzędzia
- Dodanie nowej warstwy AI (np. klasyfikacja intencji przed głównym agentem)

### 3. Typ zapytania (Query type)
Jak testujemy:
- Pojedyncze zapytanie
- Wiele zapytań
- Zapytanie od środka konwersacji

**Datasety powinny reprezentować niezbędny zestaw informacji do uruchomienia eksperymentu w zależności od tych 3 wymiarów.**

## Co powinny obejmować eksperymenty

Zidentyfikowałem kluczowe scenariusze testowe:

1. **Ton wypowiedzi** — czy agent zachowuje spójny głos
2. **Próby prompt injection** — bezpieczeństwo
3. **Różna złożoność zadań:**
   - Jednoetapowe: "Wyślij maila"
   - Wieloetapowe: "Wyślij maila i dodaj przypomnienie do kalendarza"
4. **Reakcja na błędy** — graceful handling
5. **Niemożliwość wykonania zadania** — co agent robi gdy nie może pomóc
6. **Nieprzewidziane zapytania** — edge cases
7. **Działanie pojedynczych narzędzi** — np. jak działa generator query dla Serper w izolacji vs w całym flow

## Datasety i eksperymenty przez kod

### Kluczowy wniosek

Eksperymenty generują traces widoczne na liście **tylko gdy datasety są przechowywane na platformie Langfuse**. W przeciwnym razie otrzymujemy tylko "experiment run" bez pełnej widoczności.

### Moje podejście

Buduję datasety przez platformę Langfuse, ale nie wykorzystuję ich do ewaluacji przez UI — robię to przez kod. Daje mi to pełną dowolność:
1. To ja decyduję czy ewaluuję pojedynczy prompt czy całego agenta z dostępem do prawdziwych narzędzi
2. Format nie ma znaczenia

Expected output w datasecie to również wskazówka dla nas samych — czego oczekujemy od odpowiedzi agenta.

### Gdzie umieszczać eksperymenty w kodzie?

O samych eksperymentach i ich umiejscowieniu w kodzie, lubię myśleć natomiast poprzez analogie do migracji baz danych i umieszczać je na podobnym poziomie. Sam nie wiem do końca dlaczego, po prostu koncepcyjnie są one dla mnie czymś bliźniaczym, czymś co stanowi jakiś kluczowy poboczny element całej układanki. Tutaj migrujemy pomiędzy jednym promptem a drugim i zależy nam na utrzymaniu spójności z jednoznacznym usprawnieniem.

## Typy promptów w Langfuse: tekstowe vs chatowe

Langfuse wspiera dwa typy promptów (typ jest nieedytowalny po utworzeniu):

**Text** — prompt zawierający treść z placeholderami. Nie przyjmuje historii konwersacji — zastosowanie w ewaluacjach mocno ograniczone dla aplikacji chatowych.
Kiedy używać: wersjonowany prompt bez potrzeby ewaluacji konwersacji, np. podsumowanie artykułu gdzie placeholder przyjmuje treść.

**Chat** — prompt z treścią, placeholderami i możliwością przekazania konwersacji.
Kiedy używać: testowanie prompta systemowego będącego częścią konwersacji.

**Problem:** Langfuse w placeholderze konwersacji przyjmuje wyłącznie format `{"role": "...", "content": "string"}`. Langchain używa innego formatu ("type" zamiast "role", "human" zamiast "user"). Przez to:
- Wiadomości z Langchain nie są kompatybilne
- Bardziej złożone wiadomości (np. z plikami) nie są obsługiwane
- Efektywne testowanie przez UI jest praktycznie niemożliwe, chyba że prompt jest self-contained

### Moja decyzja

**Używam wyłącznie promptów typu "Text" jako system prompty. Eksperymenty prowadzę wyłącznie przez kod.**

Ma to tą niepodważalną zaletę, że to ja decyduje o tym czy ewaluuje pojedynczy prompt czy całego agenta z narzędziami i co równie istotne dzielę format i metody z kodem produkcyjnym.

Podsumowując, zabawa z promptami przez UI — czy to przez eksperymenty czy przez playground — jest mało wartościowa biorąc pod uwagę ograniczenia formatu, więc i playground i budowanie datasetów pod to nie ma sensu.

## Zarządzanie promptami i środowiskami

Warto spiąć tag prompta ze środowiskiem celem eksperymentów. Dzięki `LANGFUSE_TRACING_ENVIRONMENT` mamy jasny podział na środowiska, a tagi pozwalają na dodatkowe filtrowanie — np. odróżnienie traces z eksperymentów od normalnego ruchu produkcyjnego.

Moje podejście:
- Prompty trzymam w Langfuse jako "Text" system prompty — wersjonowane i zarządzane przez platformę
- Eksperymenty oznaczam odpowiednimi tagami, dzięki czemu nie mieszają się z produkcyjnymi traces
- Kod eksperymentów trzymam na tym samym poziomie co migracje — jako kluczowy, ale poboczny element projektu
- Środowiska rozróżniam wyłącznie przez zmienną środowiskową, nie przez osobne projekty

## Powiązania i kontekst

Kluczowe jest prawidłowe łączenie danych:
- **Feedback → User:** powiązanie oceny z konkretną wiadomością
- **Trace ID → Message:** powiązanie trace z konkretną wiadomością w aplikacji
- **Session ID → Conversation:** powiązanie sesji z konkretną konwersacją
- **Environment variable → Trace env:** spójność środowiska aplikacji z Langfuse

## Problemy integracji Langchain ↔ Langfuse

Mimo, że Langfuse chwali się integracją z Langchain to nadal jest sporo nieścisłości i niedoróbek wg mnie, które powodują, że ten duet nie jest idealny.
To te na które sam natrafiłem:

1. **Nieprzyjazne wyświetlanie input/output na liście traces** — Langchain ma swój specyficzny format inny niż wyrosły samoistnie standard role + content. Na szczęście na szczegółach trace dane są wyświetlane w przyjaznej formie. Langfuse wyświetla ładnie tylko JSON z polami `role` i `content`.
2. **Nieoczywista konfiguracja CallbackHandlera** — konfiguracja dla "automatycznego" logowania do Langfuse oparta o instancję CallbackHandlera nie pozwala z automatu na zmiany identyfikatora sesji czy użytkownika, tym samym trzeba stosować obejścia w postaci wykorzystania innych metod m.in `propagate_attributes`. Ponadto, nie rozgryzłem jeszcze jak sprawić aby narzędzia prawidłowo wiązało się z prompt z Langfuse gdy korzystamy z LLM na poziomie tooli.
3. **Różne formaty placeholderów** — Langfuse bazuje na `{{placeholder}}`, Langchain natomiast na `{placeholder}`.
4. **Trace ID nie akceptuje UUID z myślnikami** — nie można przekazać bezpośrednio UUID jako trace ID — trzeba usunąć znaki "-". Jeśli tego nie zrobimy, trace ID po prostu się nie przypisze.
5. **Brak możliwości trzymania definicji narzędzi** — Langfuse nie pozwala przechowywać definicji narzędzi, co sprawia że jakiekolwiek próby testowania przez UI mają dodatkowy narzut w postaci duplikowania konfiguracji narzędzi.

## W stronę automatyzacji

W [[Co chciałbym wiedzieć o ewaluacji aplikacji AI na początek ?#Kiedy automatyzować ewaluację|pierwszej części]] wyróżniłem dwa typy błędów: **Missing Instructions** (braki w prompcie) i **Model Limitations** (wrodzone ograniczenia modelu). Te drugie wskazałem jako idealnych kandydatów do automatycznej ewaluacji.

Po kilku iteracjach manualnej analizy widzę, że podział ten sprawdza się w praktyce. Większość moich wczesnych Fail-i to Missing Instructions — rzeczy, które rozwiązuję prostą zmianą promptu. Automatyczny ewaluator w tym momencie byłby przedwczesny.

Otwarte pytania, z którymi będę się mierzyć w kolejnym etapie:
1. **Reference-free vs reference-based evaluation** — kiedy które podejście? Reference-based wymaga expected output w datasecie, co przy złożonych agentach jest trudne do zdefiniowania. Reference-free (LLM as Judge bez wzorcowej odpowiedzi) jest elastyczniejszy, ale potencjalnie mniej precyzyjny.
2. **Jak tworzyć datasety skutecznie?** — Manualne tworzenie jest czasochłonne, syntetyczne generowanie wymaga dobrej znajomości edge case'ów. Szukam balansu.
3. **Jaki label powinien być używany przez aplikację do zaciągania odpowiedniego prompta?** — Konwencje nazewnictwa mają znaczenie przy wersjonowaniu.
4. **Jak najlepiej testować złożone flow wieloagentowe?** — Moje 3 wymiary eksperymentów pomagają to ustrukturyzować, ale w praktyce izolacja subagentów nie jest trywialna.

Gdy dojrzeje moje zrozumienie tych tematów, opiszę je w kolejnej części.

---

![[Attachments/AI Evals Research -  Collected/2e622fd009ba4ce84c771b15fdb1272d_MD5.jpeg]]
