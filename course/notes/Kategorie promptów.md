---
tags:
  - prompt
  - todo
---



![[_resources/fcfa049a0dcc2378539de6db9e8926d0_MD5.jpeg]]
Here's an extended breakdown with examples:

#### Generujące
- **Opis**: Tworzą nową treść na podstawie wytycznych - od tekstów kreatywnych po kod, scenariusze i strategie
- **Przykład**: "Napisz 3 nagłówki reklamowe dla ekologicznej szczoteczki do zębów"

#### Kompresujące
- **Opis**: Redukują złożone informacje do esencji, zachowując kluczowe punkty i główne przesłanie
- **Przykład**: "Streść ten 20-stronicowy raport w 5 najważniejszych punktach"

#### Konwertujące
- **Opis**: Przekształcają treść między formatami, zachowując znaczenie (tekst↔kod, casual↔formal, język↔język)
- **Przykład**: "Zamień tę tabelę danych na format JSON"

#### Wyszukujące
- **Opis**: Analizują treść by znaleźć konkretne informacje, wzorce czy odpowiedzi na pytania
- **Przykład**: "Znajdź wszystkie daty spotkań wymienione w tym mailu"

#### Wykonujące
- **Opis**: Realizują określone zadania według instrukcji - obliczenia, formatowanie, sprawdzanie
- **Przykład**: "Posortuj tę listę produktów według ceny, malejąco"

#### Rozumujące
- **Opis**: Analizują sytuacje, dostarczają wnioski i rekomendacje oparte na kontekście i logice
- **Przykład**: "Jakie są potencjalne ryzyka wprowadzenia tej zmiany w procesie?"

----
Poniższe sześć kategorii dość trafnie oddaje główne sposoby, w jakie można wykorzystywać modele językowe (LLM) – każda grupa reprezentuje inny „tryb” działania bota w odniesieniu do treści i kontekstu. Oto kilka obserwacji i uwag na ich temat:

1. **Generujące**
    
    - _Charakterystyka_: W tej kategorii stawiamy przed modelem zadanie stworzenia zupełnie nowej treści: od tekstów kreatywnych (opowiadań, sloganów reklamowych) po kod czy gotowe rozwiązania.
    - _Zastosowanie_: Tworzenie artykułów, haseł marketingowych, scenariuszy, koncepcji kampanii czy nawet prototypów programistycznych.
    - _Uwagi_: Wymaga zwykle wyraźnych wskazówek dotyczących stylu, formy czy kontekstu, aby uniknąć „chaotycznych” wyników.
2. **Kompresujące**
    
    - _Charakterystyka_: Ich celem jest streszczenie, wyciągnięcie kluczowych informacji i redukcja objętości oryginalnego tekstu bez utraty sensu.
    - _Zastosowanie_: Szybkie zapoznanie się z treścią obszernych dokumentów, tworzenie esencji raportów czy notatek.
    - _Uwagi_: Ważne jest jasne określenie formy (np. liczba punktów, maksymalna długość) i poziomu szczegółowości. Przy zbyt ogólnikowych wytycznych streszczenie może być albo za długie, albo zbyt skrótowe.
3. **Konwertujące**
    
    - _Charakterystyka_: Konwersja danych czy tekstu z jednego formatu na inny (np. język, styl, format pliku). Model musi zachować sens oryginału, lecz dostosować formę.
    - _Zastosowanie_: Tłumaczenie językowe, zmiana stylu (np. formal → casual), konwertowanie zestawień do JSON/CSV/XML.
    - _Uwagi_: Ważne jest precyzyjne zdefiniowanie docelowego formatu oraz reguł (np. czy zachować oryginalną strukturę, czy zmienić nazwy pól w JSON itd.).
4. **Wyszukujące**
    
    - _Charakterystyka_: Skupione na wydobyciu konkretnych informacji z podanego tekstu czy zbioru danych. Model pełni rolę „analizatora” lub „detektora wzorców”.
    - _Zastosowanie_: Znajdowanie dat, nazwisk, kluczowych wskaźników, tworzenie odpowiedzi na bazie wielowątkowej korespondencji.
    - _Uwagi_: Precyzja zależy od jasności kryterium wyszukiwania. Jeśli pytanie jest wieloznaczne lub dane źródłowe są niekompletne, wynik może być niejednoznaczny.
5. **Wykonujące**
    
    - _Charakterystyka_: Konkretnie polega na wykonaniu zadania według instrukcji (np. obliczenia, sortowanie, formatowanie, walidacja).
    - _Zastosowanie_: Sortowanie list, dodawanie kolumn w danych, korekta tekstu wg zadanego schematu, tworzenie prostych podsumowań tabel.
    - _Uwagi_: Tutaj model często działa jak narzędzie automatyzujące powtarzalne czynności. Istotne jest, by instrukcje były sformułowane jasno i unikały dwuznaczności.
6. **Rozumujące**
    
    - _Charakterystyka_: Tutaj model wchodzi w rolę „doradcy” czy „analityka” – łączy informacje, interpretuje je i wyciąga wnioski oraz rekomendacje.
    - _Zastosowanie_: Analiza ryzyk, planowanie kroków strategicznych, tworzenie hipotez, diagnoza przyczyn problemów.
    - _Uwagi_: Przy rozumowaniu kluczowy jest kontekst i jakość dostarczonych informacji. Model może zaproponować trafną analizę jedynie w oparciu o to, co zostało mu przedstawione.

---

### Ogólne spostrzeżenia:

- **Przenikanie się kategorii**: W praktyce wiele promptów łączy w sobie elementy kilku kategorii. Na przykład polecenie „Przeanalizuj podane dane, wyciągnij najważniejsze punkty (kompresja), a następnie zaproponuj strategię wdrożenia (generowanie i rozumowanie)” angażuje co najmniej trzy z powyższych funkcji.
    
- **Stopień szczegółowości**: W każdej kategorii kluczowa jest precyzja promptu. Im lepiej sprecyzowane zadanie (np. dokładnie określone kryteria wyszukiwania, format końcowy czy ograniczenia liczby słów), tym bardziej użyteczna i zbliżona do oczekiwań będzie odpowiedź.
    
- **Kontrola stylu i tonu**: Nawet w kategoriach „sztywnych” (takich jak kompresja czy wykonanie polecenia) można zastosować wytyczne co do stylu językowego, aby wynik był spójny z założeniami (np. bardziej formalny, bardziej „ludzki” w tonie).
    
- **Znaczenie kontekstu**: Szczególnie w promptach rozumujących i generujących złożony kontent (np. długie raporty, wielowątkowe problemy), kluczową rolę odgrywa przekazanie wystarczającego kontekstu. Brak jasnych danych wejściowych sprawia, że model będzie „zgadywał” lub uzupełniał luki mniej precyzyjnymi odpowiedziami.
    
- **Zastosowanie biznesowe vs. kreatywne**: Podział na te sześć kategorii dobrze pokazuje, że LLM mogą pełnić różnorodne funkcje – od ściśle użytkowych (wykonujących, wyszukujących) po kreatywne (generujące) i wspierające proces decyzyjny (rozumujące).
    

Podsumowując, taka kategoryzacja ułatwia zrozumienie, „w jakim trybie” pracuje model i jakiego rodzaju rezultatów można oczekiwać. Jednocześnie w praktyce prompty często wymagają wielozadaniowego podejścia, łącząc kilka kategorii w jednym poleceniu.