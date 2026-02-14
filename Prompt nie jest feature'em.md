---
permalink: prompt-to-nie-feature
created: 2026-02-14
categories: "[[Pages]]"
tags:
  - pages
---
*Opublikowane 2026-02-14*
# Prompt nie jest feature'em
---
## Historia, która zmieniła nasz sposób pracy

Pracujemy nad aplikacją z podsystemem AI. Nic egzotycznego — agent przetwarza dane, zwraca odpowiedź w formacie markdown, frontend ją wyświetla. Jedna ze storek dotyczyła ulepszenia sposobu prezentowania wyników na frontendzie. Storka dojrzała, została doprecyzowana, miała w subtaskach scenariusze testowe opisujące jak powinien wyglądać finalny wynik. Klasyczny układ.

Developer skończył swoją część. Interfejs wyglądał dobrze. Podpięliśmy dane, odpaliliśmy scenariusze — i dwa z nich nie przeszły.

Reakcja była naturalna: szukamy buga we frontendzie. Sprawdzamy parsowanie markdowna, renderowanie tabel, obsługę edge case'ów. Nic. Frontend działał prawidłowo. Problem leżał głębiej — agent zwracał inny format niż oczekiwany. W jednym ze scenariuszy zamiast tabeli markdown generował listę punktowaną, w innym pomijał nagłówki sekcji, które frontend potrzebował do nawigacji.

Dobrze, to może prompt? Przecież prompt miał pokrycie w datasecie. Hipoteza formatowania była potwierdzona — kilkanaście przykładów w zbiorze testowym przechodziło poprawnie. Tylko że ten konkretny scenariusz, z tym konkretnym zestawem danych wejściowych, wypadał z wzorca.

I tu zaczęła się ciekawa rozmowa w zespole. Prompt, który nie działał, powstał tydzień wcześniej. Nie był częścią tej storki. Developer, który go napisał, pracował nad zupełnie innym zadaniem. Sam prompt był w fazie development — trwały nad nim prace w kontekście osobnego feature'a. A my testowaliśmy storkę frontendową, która w ogóle nie powinna tego prompta dotykać.

W normalnych okolicznościach pewnie zaktualizowalibyśmy prompt, domknęli scenariusze i zapomnieli o temacie. Ale sytuacja odsłoniła coś ważniejszego. Mieliśmy storkę frontendową blokowaną przez prompt, który żył w kontekście innej storki, nad którą pracował inny developer. Pytanie brzmiało: czyj to bug? Kto powinien go naprawić? I w ramach którego zadania?

To nie był problem techniczny. To był problem organizacyjny. Nasze podejście do zarządzania promptami nie pasowało do sposobu, w jaki faktycznie pracuje zespół.

---

## Problem: trzy podejścia i dlaczego dwa z nich się rozpadają

Po tej sytuacji usiedliśmy i przeanalizowaliśmy, jak w ogóle chcemy zarządzać promptami. Na stole pojawiły się trzy podejścia.

**Podejście pierwsze: jeden prompt, dwie etykiety.** W narzędziu do wersjonowania (Langfuse) trzymamy jeden prompt z labelem `production` na wersji stabilnej i `development` na wersji roboczej. Środowisko aplikacji decyduje, którą etykietę pobrać. Proste — do momentu, w którym dwóch developerów pracuje nad różnymi feature'ami dotykającymi tego samego prompta. Jeden ma wersję development w trakcie eksperymentu, drugi potrzebuje wprowadzić pilną zmianę. Nie da się mieć dwóch niezależnych wersji development na jednym prompcie. Pojawia się bloker: musisz czekać, aż kolega skończy swoją robotę i przesunie label, zanim zaczniesz swoją. A w międzyczasie storka frontendowa stoi, bo prompt jest "zajęty".

**Podejście drugie: prompt per środowisko.** Tworzymy osobne prompty — `assistant-prod`, `assistant-staging`, `assistant-dev`. Unikamy problemu z labelami, hot fixy są łatwe. Ale pojawiają się inne kłopoty. Synchronizacja między promptami staje się ręczna — trzeba pilnować, żeby zmiany z dev trafiły do prod w odpowiednim momencie. Przy trzech środowiskach i kilku promptach to szybko wymyka się z rąk. A przede wszystkim wciąż nie rozwiązuje głównego problemu: prompt jest przywiązany do storek i żyje w ich cyklu.

**Podejście trzecie: prompty jako osobny stream.** I tu dochodzimy do sedna. Prompt nie jest częścią feature'a. Prompt to infrastruktura, którą feature'y konsumują. Tak jak nie przypisujesz migracji bazy danych do storki frontendowej, tak nie powinno się przypisywać prompta do konkretnego zadania. Rozwój promptów powinien być niezależny od storek — mieć własny backlog, własne tempo, własny cykl walidacji.

---

## Workflow: pętla eksperymentów w pięciu krokach

Skoro prompty żyją niezależnie od storek, potrzebujemy procesu, który pozwoli nad nimi pracować w kontrolowany sposób. Nie wystarczy "zmień, sprawdź ręcznie, wrzuć na produkcję". Potrzebujemy pętli eksperymentalnej — takiej, która daje powtarzalne wyniki i chroni przed regresją.

Oto jak to wygląda w praktyce:

**Krok 1 — Hipoteza.** Zaczynam od konkretnego stwierdzenia, które mogę zweryfikować. Nie "poprawię prompt", ale: "dodanie few-shot examples poprawi formatowanie tabel markdown w 90% przypadków z datasetu". Hipoteza wyznacza metrykę sukcesu i zakres zmiany.

**Krok 2 — Nowa wersja prompta w Langfuse.** Nie tworzę nowego prompta — tworzę nową wersję istniejącego. Zachowuję pełną historię. Nowa wersja dostaje label roboczy, produkcyjna zostaje nienaruszona.

**Krok 3 — Ewaluacja offline.** Odpalam dataset przeciwko nowej wersji. Porównuję wyniki z wersją produkcyjną. Dla prostych kryteriów (format, obecność sekcji) używam asercji. Dla kryteriów trudnych do ujęcia w regex — na przykład "czy odpowiedź brzmi naturalnie" — wchodzi LLM-as-judge.

**Krok 4 — Analiza regresji.** To jest moment, o którym łatwo zapomnieć. Nie wystarczy, że nowy scenariusz przechodzi. Muszę sprawdzić, czy stare scenariusze nie zostały zepsute. Każda zmiana prompta może mieć efekty uboczne — model, który lepiej formatuje tabele, może gorzej radzić sobie z listami.

**Krok 5 — Promocja.** Jeśli metryki się zgadzają, przesuwam label `production` na nową wersję. To jest operacja niezależna od jakiejkolwiek storki. Prompt przeszedł swój własny pipeline walidacji.

W kodzie wygląda to tak:

```python
from langfuse import Langfuse

langfuse = Langfuse()

# Krok 2: Pobranie prompta — wersja produkcyjna i nowa
prompt_prod = langfuse.get_prompt("assistant", label="production")
prompt_new = langfuse.get_prompt("assistant", label="experiment-42")

# Krok 3: Ewaluacja offline na datasecie
dataset = langfuse.get_dataset("formatting-scenarios")

for item in dataset.items:
    # Uruchamiam agenta z nową wersją prompta
    trace = langfuse.trace(name="experiment-42")
    generation = trace.generation(
        name="assistant-call",
        input=item.input,
        model="gpt-4o",
        prompt=prompt_new,
    )

    output = run_agent(prompt_new.compile(), item.input)
    generation.end(output=output)

    # Linkuję trace z elementem datasetu
    item.link(
        trace,
        run_name="experiment-42",
        run_metadata={"hypothesis": "few-shot improves table formatting"}
    )

    # Krok 3+4: Ewaluacja — sprawdzam nowy case i regresję
    generation.score(name="format_valid", value=validate_format(output))
    generation.score(name="content_complete", value=validate_sections(output))
```

Po uruchomieniu eksperymentu Langfuse daje mi porównanie wyników między runami. Widzę, czy nowa wersja poprawia to, co chciałem poprawić — i czy nie psuje tego, co wcześniej działało. Dopiero wtedy podejmuję decyzję o promocji:

```python
# Krok 5: Promocja po pozytywnej ewaluacji
langfuse.prompts.update("assistant", version=prompt_new.version, labels=["production"])
```

Ta pętla nie jest skomplikowana. Ale zmienia jedną fundamentalną rzecz: decyzje o promptach przestają być intuicyjne i zaczynają być oparte na danych. A to zmienia sposób, w jaki cały zespół pracuje z AI.
