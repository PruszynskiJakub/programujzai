Współpraca z modelami AI przy tworzeniu kodu to sztuka balansowania między precyzją a swobodą. Kiedy zaczynamy pracę w trybie edytora, gdzie model wprowadza zmiany bezpośrednio do plików, musimy nauczyć się orkiestrować ten proces z wyczuciem i rozwagą.
  
## Zasilanie kontekstu - klucz do sukcesu

Pierwszym krokiem jest zawsze odpowiednie zasilenie kontekstu. Brzmi prosto, prawda? A jednak to właśnie tutaj wielu programistów popełnia fundamentalne błędy.

Na początku ery dostępnych LLM-ów istniała silna pokusa, by wrzucić do kontekstu cały kod źródłowy projektu. Wydawało się to logiczne - im więcej informacji, tym lepiej model zrozumie nasz projekt. Czy ten pomysł się sprawdził?

Niestety nie. Nawet modele z szerokim oknem kontekstowym, jak Gemini od Google, nie radzą sobie dobrze z nadmiarem informacji. Zbyt duży kontekst tworzy szum informacyjny, który rozprasza model i prowadzi do ogólnikowych, mało precyzyjnych odpowiedzi.

### Jak robić to efektywnie?

Wyobraź sobie, że instruujesz juniora w zespole. Czy zalałbyś go całą dokumentacją projektu na raz? Czy raczej przekazałbyś mu tylko te informacje, które są niezbędne do wykonania konkretnego zadania?

Odpowiedź jest oczywista - dodajemy do kontekstu minimalną ilość plików wymaganych do wykonania zadania. Nie za dużo, bo model się pogubi, ale też nie za mało, bo zabraknie mu kluczowych informacji.

> 💡 Jeżeli agent, którego używasz, ma możliwość dodawania plików read-only, korzystaj z tego. Ograniczy to skupienie edycji tylko na konkretnych plikach.

## Budowanie efektywnego promptu

Kolejnym krokiem jest stworzenie precyzyjnego promptu. Podobnie jak w przypadku kontekstu, tutaj również obowiązuje zasada minimalizmu.

Staraj się używać [[Słowa bogate znaczeniowo]] - czyli takich, które niosą ze sobą maksimum informacji przy minimalnej ilości tekstu. Zamiast długich opisów, używaj precyzyjnych terminów technicznych, nazw funkcji, klas czy metod.

Porównaj:

```
CREATE function fetch_news accepting number called limit and returning a list of `News`

vs

CREATE def fetch_news(limit: int) -> News
```

Druga wersja jest znacznie bardziej zwięzła, a jednocześnie precyzyjna. Model doskonale rozumie składnię języka programowania, więc nie musisz jej opisywać własnymi słowami.

## Poziomy szczegółowości promptu

Wybór odpowiedniego poziomu szczegółowości promptu zależy od złożoności zadania i wielkości kontekstu:

1. Niskopoziomowy - bardzo szczegółowy, precyzyjnie określający oczekiwania

2. Średniopoziomowy - balansujący między szczegółowością a ogólnością

3. Wysokopoziomowy - ogólny, zostawiający modelowi swobodę interpretacji

Pamiętaj o prostej zasadzie:

> Im większe zadanie, tym trzeba operować na mniejszym kontekście, z większym i bardziej szczegółowym promptem.

> Im mniejsze zadanie, tym możemy operować na większym kontekście, z mniejszym wysokopoziomowym promptem.

## Mentalność problem first

Czy to oznacza, że każdy może teraz programować bez znajomości języka? Absolutnie nie. Narzędzia AI są potężnymi asystentami, ale nie zastąpią głębokiego zrozumienia problemu.

"Mentalność problem first" jest kluczowa. Największy wzrost produktywności osiągniesz, gdy doskonale rozumiesz problem i potrafisz go rozwiązać nawet bez wsparcia AI. Model jest wtedy narzędziem przyspieszającym implementację, a nie zastępującym myślenie.

Kiedy sami nie rozumiemy problemu, próba naprowadzania AI na rozwiązanie staje się frustrująca. Klasyczne modelowanie iteracyjne, choć powolne, daje poczucie postępu i kończy się zwykle gruntownym refaktorem po osiągnięciu celu.

## Jakość kodu i rola recenzenta

Czy skupienie się na problemie, a nie na detalach implementacji, oznacza niższą jakość kodu? Niekoniecznie.

Tutaj wchodzi w grę [[Mentalność Recenzenta]]. Twoje umiejętności code review są teraz ważniejsze niż kiedykolwiek. AI pomoże ci szybko dostarczyć rozwiązanie, ale to ty musisz je zweryfikować, poprawić i dopracować.

Poświęć czas na refaktor. Sprawdź, czy kod jest czytelny, wydajny i zgodny z konwencjami projektu. AI może generować kod szybko, ale to ty odpowiadasz za jego jakość.

## 🔑 Kluczowe wnioski

- Minimalizm kontekstowy - dodawaj do kontekstu tylko niezbędne pliki

- Precyzyjne prompty - używaj bogatych znaczeniowo słów, wskazuj konkretne pliki i metody

- Problem first - najpierw zrozum problem, potem wykorzystaj AI do implementacji

- Mentalność recenzenta - zawsze weryfikuj i refaktoruj kod wygenerowany przez AI

- Balans - znajdź równowagę między szybkością dostarczania a jakością kodu

## Pułapki, których należy unikać

### Pułapki modeli

- Za słaby model - nie poradzi sobie z kompleksowymi zadaniami
  - **Konsekwencje**: Frustracja wynikająca z ciągłych poprawek, utrata czasu na iteracyjne doprecyzowywanie, spadek zaufania do narzędzi AI
  - **Kiedy występuje**: Przy próbach generowania złożonej architektury, implementacji skomplikowanych algorytmów czy integracji wielu systemów
  - **Jak unikać**: Dopasuj model do złożoności zadania, rozważ podział zadania na mniejsze części, które słabszy model może obsłużyć

- Zbyt potężny model - niepotrzebny narzut czasowy i kosztowy dla prostych zadań
  - **Konsekwencje**: Nieefektywne wykorzystanie zasobów, wyższe koszty operacyjne, dłuższy czas oczekiwania na odpowiedź
  - **Kiedy występuje**: Przy rutynowych zadaniach jak generowanie prostych funkcji, refaktoryzacja nazw zmiennych czy tworzenie podstawowych testów
  - **Jak unikać**: Wprowadź strategię doboru modeli w zależności od złożoności zadania, automatyzuj wybór odpowiedniego modelu

### Pułapki promptów

- Zbyt niskopoziomowe - skupiające się bardziej na "jak" niż na "co"
  - **Konsekwencje**: Ograniczenie kreatywności modelu, pominięcie potencjalnie lepszych rozwiązań, mikromanagement prowadzący do suboptymalizacji
  - **Kiedy występuje**: Gdy programista dyktuje każdy szczegół implementacji zamiast opisać problem i oczekiwany rezultat
  - **Jak unikać**: Skup się na opisie problemu i wymagań, pozwól modelowi zaproponować rozwiązanie, a następnie je zweryfikuj

- Zbyt wysokopoziomowe - zbyt ogólne, bez wystarczających wskazówek
  - **Konsekwencje**: Rozwiązania niedopasowane do specyfiki projektu, konieczność wielu iteracji, frustracja wynikająca z niezrozumienia intencji
  - **Kiedy występuje**: Przy zbyt ogólnych opisach typu "zrób mi system logowania" bez określenia technologii, wymagań bezpieczeństwa czy integracji
  - **Jak unikać**: Znajdź balans między ogólnym opisem problemu a konkretnymi wymaganiami, określ ograniczenia i preferencje technologiczne

### Pułapki kontekstu

- Za duży kontekst - powoduje szum informacyjny
  - **Konsekwencje**: Rozproszenie uwagi modelu, skupienie się na nieistotnych szczegółach, pomijanie kluczowych aspektów problemu
  - **Kiedy występuje**: Przy wrzucaniu całych repozytoriów do kontekstu, dodawaniu zbyt wielu plików niezwiązanych bezpośrednio z zadaniem
  - **Jak unikać**: Stosuj zasadę minimalnego kontekstu, dodawaj tylko te pliki, które są bezpośrednio związane z zadaniem, używaj narzędzi do filtrowania kontekstu

- Za mały kontekst - brak kluczowych informacji
  - **Konsekwencje**: Rozwiązania niespójne z resztą systemu, naruszenie istniejących konwencji, konieczność poprawek po integracji
  - **Kiedy występuje**: Przy izolowaniu problemu bez uwzględnienia szerszego kontekstu aplikacji, pomijaniu zależności między komponentami
  - **Jak unikać**: Analizuj zależności przed formułowaniem zadania, dodawaj do kontekstu pliki definiujące interfejsy i konwencje, upewnij się, że model rozumie architekturę systemu