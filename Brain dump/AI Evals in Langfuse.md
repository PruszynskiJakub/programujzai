# AI Evals in Langfuse - Moje doświadczenia i wnioski

## Wstęp

Langfuse to open-source'owe rozwiązanie do observability i ewaluacji aplikacji AI. Wybrałem je ze względu na możliwość self-hostingu oraz rozsądne ceny w wersji hostowanej. Ten artykuł to zbiór moich osobistych doświadczeń, wyciągniętych wniosków i otwartych pytań po pracy z platformą.

**Kluczowy wniosek na start:** Langfuse UI pozwala tylko na "prompt experiments" - dla bardziej złożonych eksperymentów (np. testowanie agentów) niezbędne jest SDK.

---

## Anatomia Langfuse

Podstawowe elementy observability: Trace, Span, Generation, Event. Dobrze ustrukturyzowany trace to podstawa do późniejszej analizy i ewaluacji.

### Środowiska i filtrowanie

Budując produkt wspieramy różne środowiska (dev, staging, prod). Aby łatwo filtrować traces:

**Rekomendowane podejście - zmienna środowiskowa:**
Ustawienie `LANGFUSE_TRACING_ENVIRONMENT` to najbardziej praktyczne rozwiązanie - proste filtrowanie po środowiskach, jednocześnie możliwość ewaluacji odpowiedzi ze wszystkich.

**Tagi dla granularnego filtrowania:**
Programistyczne tagowanie traces pozwala na dodatkowe wymiary wyszukiwania. Warto tagować np. czy trace pochodzi z eksperymentu lub testu - dzięki temu możemy je odfiltrować z normalnego ruchu.

**Podejście z wieloma projektami:**
Osobny projekt per środowisko - nie widzę w tym zalet, a jedynie dodatkową złożoność.

---

## Typy promptów: Text vs Chat

Langfuse wspiera dwa typy promptów (typ jest nieedytowalny po utworzeniu):

### Text
Prompt zawierający treść z placeholderami. Nie przyjmuje historii konwersacji - zastosowanie w ewaluacjach mocno ograniczone dla aplikacji chatowych.

**Kiedy używać:** Wersjonowany prompt bez potrzeby ewaluacji konwersacji, np. podsumowanie artykułu gdzie placeholder przyjmuje treść.

### Chat
Prompt z treścią, placeholderami i możliwością przekazania konwersacji.

**Kiedy używać:** Testowanie prompta systemowego będącego częścią konwersacji.

**Problem:** Langfuse w placeholderze konwersacji przyjmuje wyłącznie format `{"role": "...", "content": "string"}`. Langchain używa innego formatu ("type" zamiast "role", "human" zamiast "user"). Przez to:
- Wiadomości z Langchain nie są kompatybilne
- Bardziej złożone wiadomości (np. z plikami) nie są obsługiwane
- Efektywne testowanie przez UI jest praktycznie niemożliwe, chyba że prompt jest self-contained

### Moja decyzja

**Używam wyłącznie promptów typu "Text" jako system prompty. Eksperymenty prowadzę wyłącznie przez kod.**

Dzięki temu:
1. Sam decyduję czy ewaluuję pojedynczy prompt czy całego agenta z prawdziwymi narzędziami
2. Format nie ma znaczenia - pełna dowolność

---

## Moja hipoteza: 3 wymiary eksperymentów

Doszedłem do wniosku, że eksperymenty AI można opisać w trzech wymiarach:

### 1. Głębokość (Depth)
Na jakim poziomie eksperymentujemy:
- Główny agent - gdy zależy nam na jakości finalnej odpowiedzi
- Subagent - izolowane testowanie części systemu
- Łańcuch promptów - sekwencja wywołań
- Pojedynczy prompt - atomowa jednostka

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

---

## Co powinny obejmować eksperymenty

Zidentyfikowałem kluczowe scenariusze testowe:

1. **Ton wypowiedzi** - czy agent zachowuje spójny głos
2. **Próby prompt injection** - bezpieczeństwo
3. **Różna złożoność zadań:**
   - Jednoetapowe: "Wyślij maila"
   - Wieloetapowe: "Wyślij maila i dodaj przypomnienie do kalendarza"
4. **Reakcja na błędy** - graceful handling
5. **Niemożliwość wykonania zadania** - co agent robi gdy nie może pomóc
6. **Nieprzewidziane zapytania** - edge cases
7. **Działanie pojedynczych narzędzi** - np. jak działa generator query dla Serper w izolacji vs w całym flow

---

## Integracja Langchain ↔ Langfuse

### Co działa out-of-the-box
Podstawowe trace'owanie wywołań LLM.

### Pułapki i problemy

**Formaty placeholderów są różne:**
- Langfuse: `{{placeholder}}`
- Langchain: `{placeholder}`

**Powiązanie promptów z narzędziami:**
Udało mi się powiązać prompt z głównym agentem, ale nie z promptami używanymi w narzędziach. To denerwujące gdy chcę zobaczyć w Langfuse jaki prompt został użyty do generacji.

**Trace ID:**
Nie można przekazać bezpośrednio UUID jako trace ID - trzeba usunąć znaki "-".

**Wyświetlanie wiadomości:**
- Na liście traces - format Langchain wyświetla się słabo
- Na szczegółach pojedynczego trace - działa poprawnie
- Langfuse wyświetla ładnie tylko JSON z polami `role` i `content`

**Definicje narzędzi:**
Langfuse nie pozwala trzymać definicji narzędzi - testowanie przez UI wymaga duplikowania konfiguracji.

---

## Datasety i eksperymenty przez kod

### Kluczowy wniosek
Eksperymenty generują traces widoczne na liście **tylko gdy datasety są przechowywane na platformie Langfuse**. W przeciwnym razie otrzymujemy tylko "experiment run" bez pełnej widoczności.

### Moje podejście
Buduję datasety przez platformę Langfuse, ale nie wykorzystuję ich do ewaluacji przez UI - robię to przez kod. Daje mi to pełną dowolność.

### Gdzie umieszczać eksperymenty w kodzie?
Dla mnie eksperymenty przypominają migracje bazodanowe - migrujemy między jednym promptem a drugim, dbając o spójność i jednoznaczne usprawnienie.

---

## Ewaluacja manualna w Langfuse

### Score Config
**Rekomendacja: metryki binarne (Pass/Fail) zamiast skali Likerta (1-10)**
- Łatwiejsze do interpretacji
- Mniej subiektywne

### Annotation Queues
**Uwaga na ograniczenia planów:**
- Hobby: tylko 1 kolejka
- Core: 3 kolejki

W realnym projekcie może to być problematyczne.

### Workflow
1. Selekcja traces - dodaj do Annotation Queue
2. Manualna ewaluacja - Pass/Fail
3. Przy Fail - dodaj komentarz z pierwszą zaobserwowaną nieprawidłowością
4. Eksport traces z Fail i kategoryzacja na podstawie komentarzy

### Problem z komentarzami
Komentarze do traces są tragicznie wyświetlane - trzeba na nie najechać, co utrudnia szybki przegląd.

![[Attachments/AI Evals in Langfuse/ed32b45a3362d439aa5cff17e4e817a7_MD5.jpeg]]

---

## Powiązania i kontekst

Kluczowe jest prawidłowe łączenie danych:
- **Feedback → User:** powiązanie oceny z konkretnym użytkownikiem
- **Trace ID → Message:** powiązanie trace z konkretną wiadomością w aplikacji
- **Session ID → Conversation:** powiązanie sesji z konkretną konwersacją
- **Environment variable → Trace env:** spójność środowiska aplikacji z Langfuse

---

## Otwarte pytania

1. Jak tworzyć datasety skutecznie?
2. Reference-free vs reference-based evaluation - kiedy które?
3. Jaki label powinien być używany przez aplikację do zaciągania odpowiedniego prompta?
4. Jak najlepiej testować złożone flow wieloagentowe?

---

## Podsumowanie

Zabawa z promptami przez UI (eksperymenty, playground) jest dla mnie mało wartościowa ze względu na ograniczenia formatu. **Moje podejście:** datasety na platformie, eksperymenty w kodzie, prompty typu Text jako system prompty.

Langfuse jest dobrym narzędziem, ale wymaga świadomości jego ograniczeń - szczególnie w integracji z Langchain i przy bardziej złożonych scenariuszach agentowych.

---

![[Attachments/AI Evals Research -  Collected/2e622fd009ba4ce84c771b15fdb1272d_MD5.jpeg]]

----







**1. Wstęp - kontekst**

- Krótkie nawiązanie do poprzedniego artykułu (link)
- Co daje Langfuse vs inne opcje (dlaczego akurat Langfuse?)

Langfuse jest rozwiązaniem open source pozwalającym na self hosting oraz w wypadku hostowania przez twórców ceny nie są wygórowane.

**2. Anatomia Langfuse** (szybkie podstawy)

- Trace, Span, Generation, Event - co jest czym
- Jak wygląda dobrze ustrukturyzowany trace





Budując pełnoprawne produkty zapewne będzie wspierać różne środowiska - deweloperskie, produkcyjne, testowe.
Tym samym w takim układzie będzie nam zależeć aby w łatwy sposób móc wyszukiwać. 
 Robimy to przez pole env (rekomendowany) - polegający na ustawieniu zmiennej środowiskowej `LANGFUSE_TRACING_ENVIRONMENT`, jest to rozwiązanie najbardziej praktyczne i elastyczne, bo mamy zarazem prosty sposób filtrowania po środowiskach, jednocześnie mogąc ewaluować odpowiedzi na wszystkich

Jeżeli potrzebujemy również utworzyć filtry po których możemy jeszcze bardziej zgranulować wyszukiwanie wówczas dostępne mamy tagi, które możemy programistycznie zaprogramować.

Podejście z wieloma projektami - innymi słowy mamy środowisko per projekt w Langfuse, nie ma wg mnie żadnych zalet, a jedynie dostarcza złożoności.

Sam Langfuse wspiera również Prompt Management.
Są dwa typu promptów wg Langfuse:
1. Text - prompt zawierający treść oraz placeholdery w ramach treści, nie przyjmuje on natomiast żadnej historii konwersacji więc zostosowanie go dalej w ewaluacjach jest mocno ograniczone zwłaszcza dla aplikacji chatowych, bo masz wpływ i możesz ewaluować wyłącznie względem placeholderów
2. Chat - prompt zawierający treść oraz placeholdery oraz przyjmujący konwersację lub jej placeholder. Dla tego typu możemy - przekazać również wiadomości, możesz ewaluować względem placeholderów w treści oraz samej konwersacji

To jaki typ wybierzemy jest nieedytowalne.
A zależy od tego chociażby jak będziemy w stanie odpalać eksperymenty.

Innymi słowy:
1. Wybieraj typ "Text" w wypadku gdy -  Potrzebujesz wersjonowany prompt, którego nie potrzebujesz ewaluować w inny sposób niż przez placeholdery np podsumowanie artykuły gdzie w ramach treści prompt poprzez placeholder przekażesz treść artykułu
2. Wybieraj typ "Chat" w wypadku gdy zależy Ci na przetestowania prompta systemowego, który jest cześcią konwersacji, daje on większą elastykę ale również tworzenie jest trochę bardziej upierdliwe, zwłaszcza, gdy Langfuse w ramach placeholdera konwersacji przyjmuje wyłącznie format {"role": "...", "content": "string"}  co znów wprowadza kolejne ograniczenia, bo wiadomości z Langchain przez to że mają inny format, albo bardziej złożonych wiadomości z plikami nie obsłużymy

Podsumowując wg mnie zabawa z  promptami przez UI czy to przez eksperymenty czy przez playground, jest mało wartościowa albo kompletnie  bezwartościowa biorąc pod uwagę ograniczenia w postaci formatu więc i platground i budowanie datesets pod to nie ma sensu.

Osobiście mimo wszystko preferuje wykorzystanie promptów typu "Text" mimo i używanie ich wyłącznie jako system prompty. Same eksperymenty, czy testowanie różnych wersji robię wyłącznie przez kod. 

Czyli buduje datasety przez platformę, niewykorzystuje ich do ewaluacji przez UI, ale przez kod. Wówczas mam dowolność :
1. To ja decyduje czy ewaluuje pojedynczy prompt czy całego agenta z dostępem do prawdziwych narzędzi
2. Format nie ma tutaj znaczenia


Warto spiąć tag prompta ze środowiskiem celem eksperymentów

Gdzie w kodzie umieszczać eksperymenty ? 
Dla mnie brzmią one dla mnie trochę jak migracje w ramach bazki.
Tutaj migrujemy pomiędzy jednym promptem i drugim i zależy nam utrzymaniu spójności z jednoznaczym usprawnieniem.

Eksperymentować możemy z
1. ustawieniami modeli - temperatura, top-p, 
2. promptem
3. ustawieniami narzędzi
4. dodaniem nowego narzędzia - 
5. usunięciem narzędzia
6. dodaniem kolejnej warstwy AI, podzapytanie

Z poziomu, czyli jak zmiana wpływa na :
1. całego agenta - gdy zależy nam na jakości finalnej odpowiedzi
2. wykorzystanie pojedynczego narzędzia - agent z jednym toolem który chcemy usprawnić
3. trajektorią narzędzi

Poprzez: 
1. pojedyncze zapytania
2. zapytanie od środka konwersacji 


**3. Integracja Langchain ↔ Langfuse** (tu jest unikalna wartość!)

- Co działa out-of-the-box
- **Pułapki:** format placeholderów, słabe wyświetlanie na liście, różnice w strukturze
- Przykłady kodu z obejściami

Placeholdery w Langfuse mają format {{placeholder}}.
Placeholdery w Langchain mają natomiast {placeholders}.


Nie udało mi się powiązać prompta z tool używanym przez agenta.
Nie przekażemy bezpośrednio uuid jako trace id trzeba zmodyfikować usuwając znaki "-".


Nie można trzymać definicji narzędzi więc jakiekolwiek próby testowania przez UI mają dodatkowy narzut w postaci duplikowania narzędzi itd.


Eksperymenty powodują wygenerowanie traces, które znów warto byłoby dodatkowy wyróżnić w jakiś sposób - działa wyłącznie gdy datasets są trzymane u nich. 


Co chcemy aby obejmowały testy:
1. Konkretny ton wypowiedzi
2. Reakcje na nieprzewidziane zapytania
3. Zadania jedno i wieloetapowe "Wyślij maila", "Wyślij maila i wrzuć przypomnienie do kalendarza"
4. Niemożliwość wykonania zadania
5. Próby prompt injection
6. Działanie pojedynczych narzedzi gdy one bazują na LLM np. jak działa generator serper query w odosobnieniu oraz jak działa całość od wygenerowania zapytań do pozyskania wyników


**4. Workflow ewaluacji w praktyce**

- Score Config (dlaczego binarny > Likert)
- Annotation Queues (z uwagą o limitach Hobby/Core)
- Eksport i analiza

**5. Datasety i eksperymenty**

- Datasety przez UI vs w kodzie
- Prompt experiments vs testowanie całych agentów

Datasety w zależnie od naszej intencji mogą pomóc na w ewaluacji pojedynczych promptów

**6. Praktyczne wskazówki**

- Jak formatować input żeby ładnie się wyświetlał (JSON z `role` i `content`)
- Tagowanie i filtrowanie traces




Jak tworzyć datasets skutecznie ???
Reference free vs reference based evaluation


Jaki label powinien wykorzystać apka do zaciągania odpowiedniego prompt.


----
Rodzaje obserwacji w Langfuse
Prompty chat vs text
Jak testować prompty  a jak testować złożone flow lub agenta ?
Datasety do testowania przez UI i w kodzie
Tworzenie Score Configu
Tworzenie Annotation Queue do ręcznej analizy
	   - *Uwaga:* Langfuse w wersji Hobby pozwala tylko na jedną kolejkę
	   - w wersji Core są to już 3 
Langfuse wyświetla na liście traces ładnie tylko JSON z polami `role` i `content` -

Spinanie Langchain z Langfuse, co działa co nie działa
	 format od Langchain jest słabo wyświetlany, na widoku szczegółów już jest dobrze
	 format dla placeholderów jest różny

Expected output jest też wskazówką dla nas czego oczekujemy od takiej odpowiedzi
	 

Komentarze do traces są tragicznie wyświetlane, trzeba na nie najechać 
[[Attachments/AI Evals in Langfuse/ed32b45a3362d439aa5cff17e4e817a7_MD5.jpeg|Open: Screenshot 2026-02-03 at 22.05.07.png]]
![[Attachments/AI Evals in Langfuse/ed32b45a3362d439aa5cff17e4e817a7_MD5.jpeg]]
### Trace - definicja

### Workflow w Langfuse

![[Attachments/AI Evals Research -  Collected/2e622fd009ba4ce84c771b15fdb1272d_MD5.jpeg]]

1. **Selekcja traces** - dodaj interesujące traces do "Annotation Queue"

2. **Konfiguracja Score Config:**
   - Potrzebujesz binarnego score config Pass-Fail
   - W miarę możliwości stawiaj na metryki binarne - łatwe do interpretacji i mniej subiektywne niż skala Likerta (1-10) czy wartości rzeczywiste (0-1)

![[Attachments/AI Evals Research -  Collected/bc7912a323a09d8d66e0983feb2a8ca5_MD5.jpeg]]

3. **Utwórz Annotation Queue:**
   - Wymagana nazwa (np. "Open Codes") oraz score config


4. **Manualna ewaluacja:**
   - Dla każdego elementu wybierz Pass lub Fail
   - Przy Fail - dodaj komentarz z pierwszą zaobserwowaną nieprawidłowością

5. **Eksport i kategoryzacja:**
   - Eksportuj traces z wynikiem Fail
   - Na podstawie komentarzy zbuduj Axial Codes

### Uwagi praktyczne

- 
- Eksperymenty przez UI to prompt eksperymenty
- Datasety możemy wykorzytywać w kodzie jak i na UI
- Prompty typu chat pozwalają przekazywać historię konwersacji