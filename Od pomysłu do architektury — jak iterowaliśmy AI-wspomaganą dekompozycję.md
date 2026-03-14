---
permalink: iteracje-ai-dekompozycja
created: "2026-03-14"
categories: "[[Pages]]"
tags:
  - pages
---
*Opublikowane 2026-03-14*
# Od pomysłu do architektury — jak iterowaliśmy AI-wspomaganą dekompozycję
---

W [[Zrozumienie jak Proces, Flow i User Stories przeplatają się.]] opisałem kluczowe pojęcia oraz dekompozycję, na której opieramy nasz framework:

**Materiały → Procesy → Scenariusze → User Stories**

Dziś pójdę krok dalej — opowiem, jak zdecydowaliśmy się wspierać tę dekompozycję z pomocą AI. Ale nie będzie to opis gotowego rozwiązania podany na tacy. Będzie to historia iteracji, ślepych uliczek i momentów, w których musieliśmy wrócić do deski kreślarskiej.

## Punkt wyjścia — kontekst i założenia

Organizacja, z którą współpracuję, pracuje na wielu projektach jednocześnie, na zróżnicowanym stosie technologicznym. Zespoły dość często rotują — podobnie jak same projekty. Poziom wiedzy i umiejętności korzystania z AI wśród członków zespołów też jest różny.

Biorąc to pod uwagę, potrzebowaliśmy rozwiązania, które:

- jest agnostyczne względem projektu,
- jest agnostyczne względem narzędzia AI,
- pozwala w prosty sposób synchronizować nowe praktyki między wszystkimi zespołami,
- jest elastyczne i pozwala na proste rozszerzanie możliwości,
- pozwala na dzielenie toolingu wokół AI między zespołami.

To były wymagania „infrastrukturalne" — i dość szybko daliśmy sobie z nimi radę. Decyzje były oczywiste: system plików do organizacji i strukturyzacji, pliki Markdown przystępne zarówno dla AI, jak i dla człowieka, repozytorium Git do zarządzania wersjami i dzielenia zasobów.

## Prawdziwe wyzwania

Trudniejsza okazała się druga kategoria wymagań — ta dotycząca samego doświadczenia użytkownika i jakości pracy z narzędziem:

- Review rezultatów nie powinno zajmować więcej niż 10 minut.
- Narzędzie nie powinno wspierać generowania ton treści, której nikt nie przeczyta.
- Użytkownik musi mieć możliwość weryfikacji i korekty wyników.
- Agent powinien potrafić domyślać się rzeczy, które nie są jednoznacznie wyrażone w materiałach.
- Rozwiązanie musi zachowywać skuteczność wraz z czasem i wzrostem objętości danych.
- Użytkownik musi mieć możliwość kontrolowania autonomiczności agenta.

Szukanie prostego i skutecznego rozwiązania dla szerokiego grona odbiorców nie jest trywialne. Iteracji było kilka.

## Pierwsza iteracja — naiwna transformacja

Pierwotne podejście polegało na transformacji z jednego etapu na kolejny w ramach jednego, rozbudowanego procesu. Skille w tym wariancie były wieloetapowymi workflows — zaczynały od identyfikacji aktualnej wiedzy, przez stworzenie draftu, aż po samokrytykę z pomocą subagentów.

Kluczowym skillem było **skanowanie** — na etapie materiałów lub dalej — które z jednego lub kilku dokumentów generowało jeden lub więcej dokumentów reprezentujących kolejny etap dekompozycji. Na przykład: rezultatem skanowania materiałów z danego dnia były dokumenty opisujące zidentyfikowane procesy biznesowe.

Mimo że skuteczne merytorycznie, to podejście miało poważne wady. Agent pracował długo, a efekty — choć zadowalające jakościowo — były przytłaczające w swojej ilości. Kognitywnie wymagające było jednoczesne zrozumienie tego, co się zadziało, dlaczego, a następnie jeszcze ocena jakości samego rezultatu. Skill w ramach prompta wyświetlał najpierw sugerowaną dekompozycję w oknie czatu, co również stanowiło kiepski UX.

## Kolejne próby — granulacja i uproszczenia

Następne iteracje starały się adresować te bolączki: granulacja skilli, uproszczenie ich logiki, rezygnacja z niektórych etapów na rzecz szybkości. Zamiast transformacji wielu procesów naraz, skupiliśmy się na jednym. Innymi słowy — seria zmian z perspektywy Context Engineeringu.

Do skanowania dołączył nowy zestaw skilli skupionych wokół dekompozycji. Mając pojedynczy proces, wywoływaliśmy skill „decompose", który po etapie samokrytyki proponował listę scenariuszy.

Było lepiej, ale dalej żadne z podejść nie dawało takiego poczucia satysfakcji, jakiego szukałem. Brakowało czegoś fundamentalnego.

## Powrót do deski kreślarskiej

Wróciliśmy do Miro i Excalidraw i zadaliśmy sobie serię pytań kwestionujących niektóre z naszych pierwotnych pomysłów. Tym sposobem doszliśmy do kilku kluczowych obserwacji:

Surowe materiały chcemy przetwarzać tylko raz i ani razu więcej. Są to dane nieuporządkowane, często chaotyczne i niestrukturyzowane, zawierające sporo szumu. Na etapie przetwarzania surowych materiałów nie interesuje nas ich relacja z aktualnym stanem procesów, scenariuszy ani tym bardziej historyjek użytkownika. I wreszcie — w tym rozwiązaniu jest przestrzeń na zastosowanie jednej z praktyk deweloperskich popularnych w świecie AI, mianowicie Spec Driven Development, czyli podejścia, w którym najpierw tworzymy specyfikację zmian, a dopiero potem je wdrażamy.

Te spostrzeżenia okazały się brakującymi elementami układanki.

## Architektura finalna — scan, collide, consolidate

Każdy z etapów dekompozycji (Materiały / Procesy / Scenariusze) jest obsługiwany przez trzy dedykowane skille:

**Skanowanie** — identyfikacja kluczowych elementów dla danego etapu. W przypadku materiałów będą to pojęcia słownika oraz procesy, dla procesów — scenariusze, a dla scenariuszy — User Stories. Skupiamy się wyłącznie na zrozumieniu tego, co oferują nowe informacje, i nic więcej.

**Zderzenie** — porównanie odkryć z kroku pierwszego z aktualnym stanem wiedzy. Zidentyfikowane procesy zderzamy z już istniejącymi. Na tym etapie skupiamy się wyłącznie na zrozumieniu nowych informacji w kontekście naszego systemu.

**Konsolidacja** — powiązanie nowych informacji z aktualnym stanem systemu: utworzenie nowych procesów lub modyfikacja już istniejących.

Wynikiem tego trzystopniowego przetwarzania jest dokument stanowiący specyfikację — snapshot zmian systemu, które zostaną wprowadzone. I tu na scenę wchodzi kolejny skill: **implement**, który wprowadza wszystkie zmiany zdefiniowane wewnątrz specyfikacji. To właśnie jest moment, w którym Spec Driven Development zamyka pętlę — specyfikacja staje się kontraktem między fazą analizy a fazą implementacji.

## Co to daje

To rozwiązanie stanowi fundament, na którym możemy budować dalej. Jest elastyczne — pozwala na dołączanie nowych workflows, uruchamianie krytyków czy dodatkowych walidacji. Pozwala na łatwą analizę artefaktów pośrednich i ich modyfikację przez użytkownika w razie potrzeby.

Ale to, co uważam za najważniejsze: zachowuje użytkownika zaangażowanym. Pętle są krótkie i pozwalają na szybki feedback. Zamiast jednego wielkiego „wrzuć i czekaj" mamy serię małych, zrozumiałych kroków — każdy z nich daje poczucie kontroli i postępu.

Jest jeszcze jedna lekcja, być może najważniejsza: nie wolno mieszać procesu z tym, jak chcemy dochodzić do jego wartościowych artefaktów. Dekompozycja — od materiałów, przez procesy, po user stories — to nasz proces. Ale sposób, w jaki AI pomaga nam wydobywać z niego wartość (skanowanie, zderzanie, konsolidacja), to osobna warstwa. Wcześniejsze iteracje zawodziły właśnie dlatego, że te dwie rzeczy były ze sobą splecione — skille próbowały jednocześnie realizować logikę dekompozycji i produkować artefakty. Rozdzielenie ich było tym, co odkleiło całość.

To w zasadzie dwie kluczowe lekcje z tych iteracji: AI w kontekście organizacyjnym nie potrzebuje więcej autonomii — potrzebuje lepszych punktów styku z człowiekiem. A projektując te punkty styku, trzeba jasno oddzielić „co robimy" od „jak AI nam w tym pomaga".
