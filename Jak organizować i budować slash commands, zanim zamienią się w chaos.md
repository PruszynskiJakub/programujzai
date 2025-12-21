---
permalink: jak-organizowac-prompty-agentow-przed-chaosem
categories:
  - "[[Pages]]"
created: 2025-12-21
tags:
  - pages
---
# Jak organizować i budować prompty dla swoich agentów, zanim zamienią się w chaos

Od pamiętnej premiery [[ChatGPT]] od [[OpenAI]] w listopadzie 2022 roku minęły już ponad dwa lata. Powiedzieć, że sporo się zmieniło od tego czasu, to powiedzieć nic. W ciągu tego okresu duże modele językowe ([[Słowniczek/LLM|LLM]]) nie tylko zyskały nowe umiejętności, jak możliwość generowania obrazów czy dźwięków, ale przede wszystkim stały się wszechobecnym elementem naszego życia. W naturalny sposób zmieniły się zatem nasze przyzwyczajenia oraz sposób komunikacji z aplikacjami, a prompt stał się podstawową jednostką informacji.

Branża IT w oczywisty sposób uległa największej transformacji podczas tego umysłowego przewrotu. Dziś programiści już nie tylko programują — oni promptują. Asystenci AI do programowania pojawiają się na każdym kroku, stając się standardem, którego nie można ignorować.

Sam jestem wielkim zwolennikiem narzędzia [[Claude Code]] od [[Anthropic]], w sumie z dwóch względów:

1. Uwielbiam rodzinę modeli Claude za ich styl i jakość generowanych odpowiedzi, mimo że nie są one niskobudżetowe.
2. Historycznie pracowałem przy aplikacjach mobilnych i potrzebowałem agenta dostępnego jednocześnie w Xcode i Android Studio — stąd padło na AI w terminalu.

Każde z tych narzędzi łączy przynajmniej jedno — promptowanie oraz jakiś mechanizm reużywalności promptów. W Claude Code nazywa się to _slash commands_, w Cursor natomiast _rules_. Te mechanizmy stanowią fundamentalne rozwiązanie pozwalające w powtarzalny i skuteczny sposób budować złożone systemy. Wraz z rozwojem tych systemów zyskujemy dźwignię do delegowania coraz większych zadań z rosnącą skutecznością.

Z mojego doświadczenia i eksperymentów w budowaniu takiego systemu świetnie sprawdzają się dwa proste modele myślowe:

1. **Prompt to funkcja** — upraszcza myślenie o tym, jak budować prompty
2. **Narzędzia i procesy** — upraszcza myślenie o tym, jak prompty organizować

---

## Prompt to funkcja

Z obserwacji widzę, że sporo deweloperów ma dość chaotyczne podejście do promptów. Nie budują dopasowanej układanki, gdzie każdy puzzel ma jasno określone miejsce i cel. Przypomina to raczej kleksy z tuszu na białej kartce — takie, które wykorzystuje psychologia, pytając ze świdrującymi oczami: „Co widzisz na tym obrazku?".

Według mnie zbudowanie takiej układanki jest naturalne, jeśli tylko spojrzymy w sposób abstrakcyjny i ścisły na prompt właśnie jako funkcję — czyli fragment kodu zapisany w języku naturalnym, który przyjmuje pewne parametry i wynikowo zwraca jakiś rezultat.

Patrząc na to w ten sposób, naturalne staje się, że prompty powinny:

- mieć tylko jedną odpowiedzialność i wywiązywać się z niej rzetelnie,
- przyjmować maksymalnie 3 argumenty dla zachowania skupienia,
- być komponowalne z innymi promptami, aby móc budować złożoność w sposób przejrzysty.

Aby to podejście działało, konieczna jest oczywiście możliwość wywoływania promptów z innych promptów. W Claude Code tym mechanizmem jest wbudowane narzędzie _SlashCommand_, wywołujące inny prompt (czyli slash command).

### Przykład w praktyce

Załóżmy, że chcemy przygotować N alternatywnych podejść do jakiejś implementacji.

**Podejście 1: Monolityczny prompt**

Możemy opisać to wszystko w ramach jednego rozbudowanego prompta, który sam generuje wiele wariantów i je porównuje. Problem? Prompt robi zbyt wiele naraz, trudno go debugować i modyfikować.

**Podejście 2: Kompozycja promptów**

Tworzymy dwa osobne prompty:

- `/analyze-single` — odpowiedzialny za przeprowadzenie pojedynczej analizy podejścia
- `/analyze-variants` — odpowiedzialny za N-krotne wywołanie `/analyze-single` i zebranie wyników w raport

Drugie podejście daje kompozycyjność, wyższą jakość i możliwość skupienia się na tym, aby każdy prompt miał jasny, pojedynczy cel. Jeśli analiza nie działa poprawnie, wiem dokładnie, który prompt naprawić.

---

## Narzędzia i procesy

W momencie gdy mamy już zbudowaną obszerną kolekcję promptów, niedogodnością staje się odwoływanie do nich poprzez coraz dziwniejsze nazwy, które nie wpadają w pamięć. Mnie to właśnie spotkało i postanowiłem sobie to jakoś zorganizować.

Organizacja, którą przyjąłem, opiera się na dwóch wymiarach. Każdy prompt klasyfikuję jako:

**1. Narzędzie** — z czym pracuję?

Przykłady: `git`, `obsidian`, `figma`, `xcode`, `docker`

**2. Proces** — w jakiej fazie jestem?

|Faza|Opis|
|---|---|
|Meta-prompting|Tworzenie i ulepszanie samych promptów|
|Planowanie|Analiza wymagań, architektura rozwiązania|
|Kodowanie|Właściwa implementacja|
|Testowanie|Weryfikacja poprawności|
|Recenzowanie|Code review, refaktoring|
|Dokumentowanie|README, komentarze, changelog|

Na podstawie powyższego, wykorzystując przestrzenie nazw w Claude Code (alternatywnie można tworzyć sufiksy), przeniosłem wszystkie swoje prompty do odpowiednich podfolderów:

```
.claude/commands/
├── git/
│   ├── plan-commit.md
│   ├── review-pr.md
│   └── generate-changelog.md
├── code/
│   ├── implement-feature.md
│   ├── refactor-module.md
│   └── write-tests.md
└── docs/
    ├── generate-readme.md
    └── document-api.md
```

Teraz nie muszę się zastanawiać, pod jaką wymyślną nazwą coś ukryłem. Pytam siebie natomiast: w jakiej fazie budowania jestem lub z jakiego narzędzia chcę właśnie skorzystać?

---

## Podsumowanie

Organizacja promptów to inwestycja, która zwraca się szybko. Dwa modele myślowe, które sprawdzają się w praktyce:

1. **Prompt to funkcja** — traktuj prompty jak kod: jedna odpowiedzialność, ograniczona liczba parametrów, możliwość kompozycji.
    
2. **Narzędzia × Procesy** — organizuj prompty w dwuwymiarowej siatce, żeby zawsze wiedzieć, gdzie szukać.
    

Zacznij od małego — wybierz jeden powtarzalny workflow, który wykonujesz regularnie, i zamień go w kompozycję 2-3 promptów. Zobaczysz różnicę.