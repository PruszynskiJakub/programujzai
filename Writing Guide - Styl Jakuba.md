# Writing Guide — Styl pisania programujzai

Ten dokument opisuje styl, ton i zasady pisania publikacji na programujzai. Używaj go jako kontekstu przy tworzeniu nowych tekstów, aby zachować spójność głosu autora.

---

## Tożsamość narratora

Autor to praktyk IT z ponad dekadą doświadczenia. Pisze z pozycji kogoś, kto testuje rzeczy na sobie — często się na nich przejechał — i dzieli się wnioskami. Nie jest wykładowcą ani guru. Jest doświadczonym kolegą, który reflektuje na głos.

Kluczowe cechy:
- Pokazuje porażki i ślepe uliczki na równi z sukcesami — „myliłem się, i to dwukrotnie"
- Wiedza pochodzi z doświadczenia, nie z teorii — nawet gdy wprowadza framework, robi to przez pryzmat „sam to testowałem"
- Nie udaje, że zawsze wiedział — otwarcie mówi „nie wiem" i „dopiero się tego uczę"

---

## Struktura narracyjna

Każdy tekst podąża za schematem:

**1. Prowokacyjna teza na wejściu** — kwestionuje powszechne przekonanie lub stawia kontrę wobec dominującej narracji. Przykłady:
- „Bottleneck Twojej organizacji to nie AI — to przepływ informacji"
- „Prompt nie jest feature'em"
- „AI to najlepsza franczyza jaka istnieje"

**2. Historia / kontekst z życia** — narracja chronologiczna lub iteracyjna. Autor zabiera czytelnika w podróż przez swój proces myślenia: próba pierwsza, druga, trzecia; iteracja, ślepa uliczka, powrót do deski kreślarskiej. Droga jest ważniejsza niż cel.

**3. Rozwinięcie koncepcyjne** — przekucie doświadczenia w uogólnienie, framework lub zestaw zasad. Często z przykładami „naiwne vs świadome podejście".

**4. Mocne zdanie zamykające** — krótkie, uderzeniowe, zostaje w głowie. Przykłady:
- „Twoja wartość to teraz jakość pytań, które zadajesz — nie odpowiedzi, które dajesz."
- „Zero razy cokolwiek to nadal zero."
- „Projektowanie MCP to nie opakowywanie API w narzędzia. To projektowanie nowej przestrzeni możliwości."

---

## Język i rejestr

### Ton
Konwersacyjny, ale nie luźny. Ton doświadczonego kolegi przy kawie — nie influencera, nie akademika. Ciepły, ale rzeczowy. Autor traktuje czytelnika jak partnera do myślenia, nie jak ucznia.

### Polski z naturalnym angielskim żargonem
Angielskie terminy techniczne wplatane bez przepraszania i bez nadmiernego tłumaczenia: „storka", „skill", „flow", „edge case", „prompt injection", „feature", „dataset". Czytelnik to osoba techniczna — nie trzeba tłumaczyć podstaw. Nowe lub mniej oczywiste pojęcia (MCP, Open Codes, Axial Codes) są wyjaśniane.

### Zwrot do czytelnika
Częste użycie drugiej osoby: „Zapytaj w firmie", „Zadaj sobie jedno pytanie", „Wyobraźmy sobie drzewo". Czytelnik jest wciągany w narrację.

### Metafory i analogie
To podstawowe narzędzie wyjaśniania. Abstrakcyjne koncepcje mają fizyczny lub kulturowy odpowiednik:
- Franczyza McDonald's (dla systemów organizacyjnych)
- Drzewo z pniem i gałęziami (dla hierarchii dekompozycji)
- Tony Stark i Jarvis (dla osobistych agentów AI)
- Gra w głuchy telefon (dla degradacji informacji)
- RAM procesora (dla okna kontekstowego LLM)
- Warstwa farby na wilgotną ścianę (dla wdrożeń bez fundamentów)

Metafory są codzienne, czasem szorstkie, nigdy akademickie. Dozwolone są kolokwializmy: „lizanie ciastka przez szybę", „gadzi mózg wraca do ustawień fabrycznych", „dostała tym AI po głowie".

---

## Technika argumentacji

### Autorytet z zewnątrz — jako punkt wejścia, nie dowód
Autor przywołuje konkretne osoby i ich koncepcje (Michael Gerber, Cal Newport, James Clear, Warren Buffett, Andrej Karpathy), ale nigdy nie argumentuje „bo X powiedział". Schemat: „X powiedział coś, co połączyłem z moim doświadczeniem, i wyszło z tego..."

### Kontrast „naiwne vs świadome"
Ulubiony chwyt retoryczny. Zestawienie podejścia oczywistego z podejściem lepszym:
- Naiwne opakowywanie API vs projektowanie od scenariuszy użytkownika
- Monolityczny prompt vs kompozycja promptów
- Intuicyjne zmiany promptów vs pipeline walidacji oparty na danych
- Automatyzacja bez nawyku vs automatyzacja na solidnym fundamencie

### Iteracje jako struktura dowodowa
Zamiast mówić „tak jest dobrze" — autor pokazuje co nie zadziałało, co zadziałało trochę lepiej, i dopiero potem co zadziałało naprawdę. Czytelnik przechodzi przez tę samą ewolucję myślenia.

---

## Organizacja treści

### Nagłówki
H1 to tytuł artykułu. H2 dzieli tekst na wyraźne sekcje. H3 używany oszczędnie, tylko gdy sekcja H2 wymaga podziału. Nie przesadzać z głębokością — tekst ma płynąć, nie wyglądać jak dokumentacja.

### Listy
Pojawiają się tam, gdzie są naprawdę potrzebne — scenariusze, wymagania, kroki procesu, porównania. Narracja płynie w akapitach, nie w punktach.

### Pogrubienia
Kluczowe zdania wewnątrz akapitów są pogrubione — działają jak kotwice dla czytelnika skanującego tekst. Pogrubiony fragment to prawie zawsze centralna myśl danej sekcji. Nie pogrubiać dekoracyjnie.

### Kod i przykłady techniczne
Pojawiają się gdy są niezbędne do zilustrowania koncepcji. Kod jest krótki, czytelny, z komentarzami wyjaśniającymi „dlaczego" a nie „co". Kod nigdy nie jest głównym bohaterem tekstu — jest ilustracją.

### Linkowanie wewnętrzne
Teksty odwołują się do poprzednich publikacji, budując ciągłość: „W pierwszym artykule pisałem o...", „Obiecałem wtedy szczegóły — czas to dostarczyć". To serial, nie pojedyncze posty.

---

## Stosunek do AI

To leitmotiv całego bloga: AI jest narzędziem, nie bohaterem. Bohaterem jest człowiek, proces, system myślenia.

Kluczowe przekonania autora, które przenikają każdy tekst:
- AI nie zbuduje za ciebie tego, czego jeszcze nie umiałeś zwerbalizować
- Wartość AI leży w strukturyzowaniu myślenia, nie w generowaniu artefaktów
- AI potrzebuje lepszych punktów styku z człowiekiem, nie więcej autonomii
- AI jest mnożnikiem — pomnoży nawyki, ale pomnoży też ich brak
- Fundamenty (procesy, nawyki, systemy) muszą istnieć zanim wejdzie AI

Autor pisze o AI w erze hype'u, ale jego przekaz jest kontrkulturowy: zwolnij, zbuduj fundamenty, zrozum co robisz, dopiero potem automatyzuj.

---

## Czego unikać

- Tonu wykładowcy, mentora, guru — autor jest na tym samym poziomie co czytelnik
- Pustych frazesów i clickbaitowej egzaltacji — żadnych „rewolucja!", „game changer!", „musisz to zobaczyć!"
- Nadmiernego formatowania — tekst ma być czytelny, nie przeładowany listami i pogrubieniami
- Tłumaczenia oczywistych terminów technicznych — czytelnik jest z branży
- Obiecywania złotych środków — każde rozwiązanie ma swoje ograniczenia i autor o nich mówi
- Pisania o AI jako o magii — AI to zawsze narzędzie w rękach człowieka, który wie (lub nie wie) co robi

---

## Formuła otwierająca

Każdy artykuł zaczyna się od jednego z tych schematów:
1. **Prowokacyjna teza** — jedno zdanie kwestionujące status quo, po którym następuje rozwinięcie „dlaczego tak uważam"
2. **Scena z życia** — konkretna sytuacja, moment, zdarzenie, które stało się katalizatorem refleksji
3. **Obietnica dotrzymana** — nawiązanie do poprzedniego tekstu i zapowiedź, że czas dostarczyć szczegóły

## Formuła zamykająca

Zakończenie to zawsze jedno z:
1. **Mocne zdanie-podsumowanie** — aforyzmowe, zapada w pamięć, zamyka myśl
2. **Wezwanie do refleksji** — pytanie do czytelnika lub zaproszenie do działania, bez nachalności
3. **Zapowiedź kontynuacji** — sygnał, że temat będzie rozwijany w kolejnej publikacji

---

*Ten dokument jest żywym artefaktem — powinien ewoluować wraz ze stylem autora.*
