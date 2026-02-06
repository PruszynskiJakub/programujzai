Ta publikacja jest kontynuacją o tym jak zrozumieć ewaluację AI i wykorzystać je w praktyce.

Buduję aplikację konwersacyjnego agenta AI mającego dostęp do pokaźnego zbioru narzędzi.
Ze względu na istniejący już backend w języku Python zdecydowałem się na wykorzystanie kombinacji:
- Langchain - framework do zbudowania agenta oraz jego toolingu
- Langfuse - zarządzenie promptami, eksperymenty, ewaluacja

Langfuse to open-source'owe rozwiązanie do observability i ewaluacji aplikacji AI. Wybrałem je ze względu na możliwość self-hostingu oraz rozsądne ceny w wersji hostowanej. Ten artykuł to zbiór moich osobistych doświadczeń, wyciągniętych wniosków i otwartych pytań, które pojawiały mi się w głowie przed budowaniem pierwszych aplikacji AI.

**Kluczowy wniosek na start:** Langfuse UI pozwala tylko na "prompt experiments" — dla bardziej złożonych eksperymentów (np. testowanie agentów) niezbędne jest SDK.

## Dlaczego w ogóle ewaluacja?

Na pewnym etapie budowania aplikacji z AI będziemy chcieli wyjść poza strefę eksperymentowania, wprowadzania modyfikacji w promptach i narzędziach wyłącznie z pomocą naszej intuicji, będziemy chcieli odzyskać kontrolę.

## Pytania, na które szukałem odpowiedzi

Oto pytania, na które szukałem odpowiedzi — i na które chciałbym znać odpowiedzi zanim zacząłem pracę z Langfuse. Pogrupowałem je tematycznie:

**Proces ewaluacji i analiza**
1. Jak wygląda cały proces ewaluacji w Langfuse?
2. Jak przeprowadzić analizę Open Codes i Axial Codes w Langfuse?

**Datasety i eksperymenty**
3. Jak zacząć budować pierwszy dataset?
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

Zderzając się pierwszy raz tymi wszystkimi terminami możemy czuć się przytłoczeni ilością różnych dziwnie brzmiących pojęć i ich powiązań. Wypiszmy je sobie aby uporządkować wiedzę:

- **Score Config** - to definicja metryki i wartości jakie może przyjąć
- **Score** - to po prostu metryka, może być reprezentowana przez wartość liczbową, wartość Prawda/Fałsz lub stanowić kategorię z wartościami w postaci etykiet
- **Annotation Queue** - to kolejka wyselekcjonowanych ręcznie lub automatycznie traces, które wymagają manualnej analizy przez człowieka
- **Dataset** - to zbiór par input + expected output, które stanowią reprezentację danych jakie przyjmuje nasz agent lub jakaś jego składowa
- **Eksperyment** - to proces, rozpoczęty hipotezą, obejmujący weryfikację tej hipotezy na podstawie rzetelnych danych i zakończony decyzją oraz wnioskami dotyczącymi prawdziwości postawionej hipotezy

## Anatomia Langfuse

Podstawowe elementy observability w Langfuse to Trace, Span, Generation i Event. Dobrze ustrukturyzowany trace to podstawa do późniejszej analizy i ewaluacji.

### Środowiska i filtrowanie

Budując produkt wspieramy różne środowiska (dev, staging, prod). Aby łatwo filtrować traces:

**Rekomendowane podejście — zmienna środowiskowa:**
Ustawienie `LANGFUSE_TRACING_ENVIRONMENT` to najbardziej praktyczne rozwiązanie — proste filtrowanie po środowiskach, jednocześnie możliwość ewaluacji odpowiedzi ze wszystkich.

**Tagi dla granularnego filtrowania:**
Programistyczne tagowanie traces pozwala na dodatkowe wymiary wyszukiwania. Warto tagować np. czy trace pochodzi z eksperymentu lub testu — dzięki temu możemy je odfiltrować z normalnego ruchu.

**Podejście z wieloma projektami:**
Osobny projekt per środowisko — nie widzę w tym zalet, a jedynie dodatkową złożoność.

## Jak to się łączy: hipoteza → weryfikacja

Mając już wspólne zrozumienie możemy przedstawić jak te wszystkie rzeczy łączą się.
Z jednej strony mamy rzeczy, które pozwalają nam postawić hipotezę, z drugiej rzeczy które tą hipotezę pozwalają nam zbadać.

**Stawianie hipotez: Score Config → Score → Annotation Queue**

Aby zastosować podejście Open Codes i Axial Codes, które pozwalają nam nie tylko lepiej zrozumieć błędy zachodzące w aplikacji, ale również określić ich kategorię i skalę, potrzebujemy binarnej metryki (Score), którą potrzebujemy utworzyć poprzez Score Config, aby ta metryka finalnie była dla nas dostępna w Annotation Queue aka Human Annotation.

**Weryfikacja hipotez: Dataset → Eksperyment**

Gdy już postawiliśmy np. hipotezę o tym co stanowi źródło konkretnego błędu, jesteśmy w stanie zbudować zróżnicowany zestaw danych, który kończy się tym błędem, a następnie wprowadzić zmianę np. w naszym promptcie celem weryfikacji wyników.

Hipotezy mogą obejmować niemal wszystko, nie tylko zaobserwowane błędy. Przykładowe inne hipotezy to:
- niewrażliwość aplikacji na prompt injection
- przyznawanie się do niewiedzy gdy agent nie ma dostatecznej wiedzy
- umiejętność wybrania odpowiedniej trajektorii narzędzi gdy zadanie jest skomplikowane i wieloetapowe
- umiejętność zbudowania odpowiedniego zapytania do narzędzia

## Ewaluacja manualna w Langfuse

### Score Config

**Rekomendacja: metryki binarne (Pass/Fail) zamiast skali Likerta (1-10).** Łatwiejsze do interpretacji i mniej subiektywne.

### Annotation Queues

**Uwaga na ograniczenia planów:**
- Hobby: tylko 1 kolejka
- Core: 3 kolejki

W realnym projekcie może to być problematyczne.

### Workflow ewaluacji

1. **Selekcja traces** — dodaj interesujące traces do Annotation Queue
2. **Manualna ewaluacja** — dla każdego elementu wybierz Pass lub Fail
3. **Przy Fail** — dodaj komentarz z pierwszą zaobserwowaną nieprawidłowością
4. **Eksport traces z Fail** i kategoryzacja na podstawie komentarzy (Axial Codes)

### Problem z komentarzami

Komentarze do traces są tragicznie wyświetlane — trzeba na nie najechać, co utrudnia szybki przegląd.

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
- **Feedback → User:** powiązanie oceny z konkretnym użytkownikiem
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

## Otwarte pytania

1. Jak tworzyć datasety skutecznie?
2. Reference-free vs reference-based evaluation — kiedy które?
3. Jaki label powinien być używany przez aplikację do zaciągania odpowiedniego prompta?
4. Jak najlepiej testować złożone flow wieloagentowe?

---

![[Attachments/AI Evals Research -  Collected/2e622fd009ba4ce84c771b15fdb1272d_MD5.jpeg]]
