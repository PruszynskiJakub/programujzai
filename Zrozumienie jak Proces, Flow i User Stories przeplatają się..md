---
permalink: proces-flow-user-stories
created: 2026-03-06
categories: "[[Pages]]"
tags:
  - pages
---
*Opublikowane 2026-03-06*
# Proces, Flow, User Story — trzy poziomy, które porządkują chaos
---

W [[Bottleneck Twojej organizacji to nie AI — to przepływ informacji]] pisałem o tym, że prawdziwe wąskie gardło organizacji to nie brak narzędzi AI, lecz jakość przepływu informacji. Obiecałem wtedy szczegóły — konkretny proces, narzędzia i pierwsze wnioski. Czas to dostarczyć.

Budując AI Project Brain i współpracując z Product Ownerami oraz Product Managerami jako naszymi pierwszymi użytkownikami, musiałem wgryźć się głębiej w trzy fundamentalne pojęcia: Proces biznesowy, Flow i User Story. Każdy je zna, każdy ich używa. Sam do niedawna byłem przekonany, że świetnie je rozumiem — budowanie produktu pokazało mi, że się myliłem.

## Trzy poziomy dekompozycji

Wyobraźmy sobie drzewo. Pień to cel — np. „użytkownik zakłada konto". Gałęzie to różne ścieżki, którymi może pójść. Korona to stany końcowe — sukces, błąd, porzucenie.

**Proces biznesowy** to całe to drzewo — ustrukturyzowana sekwencja aktywności podejmowanych przez aktora w celu osiągnięcia konkretnego celu. Rejestracja użytkownika, tworzenie kolekcji zdjęć, składanie zamówienia — każdy z tych procesów ma swoje rozgałęzienia, zależności i stany końcowe.

**Flow (scenariusz)** to pojedyncza ścieżka w tym drzewie. Nie całe drzewo — jedna gałąź od pnia do liścia. Rejestracja przez Google. Rejestracja przez email. Próba rejestracji, gdy konto z danym emailem już istnieje.

**User Story** to opis konkretnej funkcjonalności, która realizuje pełny scenariusz lub jego wycinek — z perspektywy użytkownika końcowego, z kryteriami akceptacyjnymi i zdefiniowanymi zachowaniami.

## Dlaczego ta hierarchia ma znaczenie

Nigdy wcześniej nie zastanawiałem się głęboko nad transformacją surowych wymagań od klienta na User Stories. Jednocześnie, dzięki doświadczeniu, podskórnie czułem jak dzielić storki i jak dostarczać w nich wartość — choć nigdy nie miałem pełnego obrazu. Te trzy poziomy go uzupełniają.

**Proces biznesowy naturalnie przekłada się na Epik.** Reprezentuje zamknięty kontekst, który nie powinien być mieszany w ramach jednej User Story. Procesy mają też między sobą zależności — dodawanie zdjęć do ulubionych (proces kolekcji) nie ma sensu, jeśli nie wyświetlamy zdjęć (proces galerii). Albo po dewelopersku: „nie zrobimy X, bo zależy od Y".

**Flow pozwala zawęzić dyskusję.** Zamiast rozmowy, w której każdy ekran obrastał kolejnymi pomysłami — „a tu możemy dodać like, a tu pobranie, a tu..." — skupiamy się na jednym procesie i jego konkretnych ścieżkach. Jeśli rozmawiamy o kolekcjach, to rozmawiamy o dodawaniu, zarządzaniu i usuwaniu elementów w kolekcjach. Nic więcej.

**Z scenariuszy powstają User Stories** — jedna lub wiele, zależnie od preferowanej granulacji. Osobiście wolę wręcz banalnie proste storki — na poziomie jednego przycisku na jednym ekranie. Im prostsze, tym mniej miejsca na niedomówienia, tym celniejsza wycena i tym szybsza satysfakcja dewelopera z dowiezienia czegoś konkretnego.

## Przykład: od procesu do storków

Weźmy proces rejestracji użytkownika.

**Scenariusze:**
Rejestracja przez Google. Rejestracja przez email. Próba rejestracji z emailem, który już istnieje w systemie.

**User Stories dla scenariusza „email już istnieje":**
Obsługa sytuacji, gdy konto należy do tego samego użytkownika — łączenie kont. Obsługa sytuacji, gdy konto należy do kogoś innego — komunikat i alternatywna ścieżka.

Każdy z tych storków ma jasny kontekst (proces rejestracji), jasną ścieżkę (scenariusz „email istnieje") i jasny zakres (jedna konkretna sytuacja). Nic się nie miesza, nic nie trzeba domyślać.

## Jak to wpływa na AI Project Brain

W pierwszym artykule pisałem o przepływie: **Informacja → AI Project Brain → Zespół → Implementacja**. Teraz mogę pokazać, co dzieje się wewnątrz tego „Brain".

Transformacja przebiega etapami:

**Materiały → Procesy → Scenariusze → User Stories**

Każde przejście między etapami to osobny krok — nie jedno wielkie „wrzuć dokument, dostaniesz gotowe storki". To celowe. Postawiliśmy kilka założeń projektowych:

Po pierwsze — artefakty powstające z transformacji AI muszą być możliwe do zrecenzowania w mniej niż 10 minut. Jeśli AI wygeneruje z transkrypcji spotkania 40 storków na raz, nikt ich rzetelnie nie przejrzy. Ale 5 procesów biznesowych? To da się zrecenzować, poprawić i zatwierdzić.

Po drugie — narzędzie musi być agnostyczne względem projektu i narzędzi AI. Nie budujemy kolejnego wrappera na GPT ani pluginu do Jiry. Budujemy framework transformacji.

Po trzecie — kontrola i zrozumienie ponad ilość. Każdy etap daje użytkownikowi możliwość zatrzymania się, przeanalizowania i skorygowania kierunku — na poziomie koncepcji, nie szczegółów implementacyjnych.

## Pierwsze wnioski

Dekompozycja działa. Gdy PM dostaje do recenzji procesy biznesowe zamiast surowych storków, dyskusja przenosi się na właściwy poziom — „czy ten proces w ogóle powinien istnieć?" zamiast „czy ten przycisk powinien być niebieski?". Dopiero po zatwierdzeniu procesów przechodzimy do scenariuszy, a potem do storków.

To podejście wymusza też coś, czego większość narzędzi AI nie robi — idempotentność transformacji. Jeśli poprawimy opis procesu i ponownie wygenerujemy scenariusze, powinniśmy dostać przewidywalnie lepsze wyniki, nie losowo inne.

Nadal jesteśmy na wczesnym etapie. Ale jedno jest już dla mnie jasne: wartość AI w kontekście organizacji nie leży w generowaniu artefaktów — leży w strukturyzowaniu myślenia o nich.

Branża IT w oczywisty sposób uległa największej transformacji podczas tego umysłowego przewrotu. Dziś programiści już nie tylko programują — oni promptują. Asystenci AI do programowania pojawiają się na każdym kroku, stając się standardem, którego nie można 