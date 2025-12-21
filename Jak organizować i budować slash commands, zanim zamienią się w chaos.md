---
permalink: jak-organizowac-prompty-agentow-przed-chaosem
categories:
  - "[[Pages]]"
created: 2025-12-21
tags:
  - pages
---
 *Opublikowane 2025-12-21* 
### Jak organizować i budować prompty dla swoich agentów, zanim zamienią się w chaos
---

Od pamiętnej premiery [[ChatGPT]] od [[OpenAI]] w listopadzie 2020 roku minęło już ponad 5 lat.
Powiedzieć, że sporo się zmieniło od tego czasu, to powiedzieć nic. W ciągu tego okresu duże modele językowe ( [[Słowniczek/LLM|Large Language Models]] ) nie tylko zyskały nowe umiejętności jak możliwość generowania obrazów czy dźwięków, ale przede wszystkim stały się wszechobecnym elementem naszych żyć. W naturalny sposób uległy zatem zmianie nasze przyzwyczajenia oraz sposób komunikacji z aplikacjami, a [[Prompt|prompty]] stał się podstawową jednostką informacji.

Branżą IT w oczywisty sposób uległa największej transformacji podczas tego umysłowego przewrotu. Dziś programiści już nie programują, oni promptują, natomiast asystenci AI do programowania pojawiają się na każdym kroku, stając się standardem, któremu nie można się zaprzeczyć.

Sam jestem wielkim zwolennikiem narzędzia [[Claude Code]] od [[Anthropic]], w sumie z dwóch względów: 
1. Uwielbiam rodzinę modeli [[Claude]] za ich styl i jakość generowanych odpowiedzi mimo, że nie są one niskobudżetowe
2. Historycznie pracowałem przy aplikacjach mobilnych i potrzebowałem agenta dostępnego jednocześnie w Xcode i Android Studio stąd padło na AI w terminalu.

Każdego z tych narzędzi łączy przynajmniej jedno - promptowanie oraz jakiś mechanizm reużywalności promptów. W [[Claude Code]] nazywa się to *slash commands*, w [[Cursor]] natomiast *rules*. Te mechanizmy stanowią fundamentalne rozwiązanie pozwalające w powtarzalny i skuteczny sposób budować złożone systemy. Wraz z rozwojem tych systemów zyskujemy dźwignię delegowania co i raz większych zadań z rosnącą skutecznością.

Z mojego doświadczenia i eksperymentów w budowaniu takiego systemu świetnie sprawdzają się dwa proste modele myślowe 
1. Prompt to funkcja - upraszczającego myślenie o tym jak budować prompty
2. Narzędzia i procesy - upraszczającego myślenie jak prompty organizować

#### Prompt to funkcja
Z obserwacji widzę, że sporo deweloperów, ma dość chaotyczne podejście do promptów. Nie budują one dopasowanej układanki gdzie każdy puzzel ma swoje jasno określone miejsce i cel. Przypomina to raczej kleksy z tuszu na białej kartce, takie które wykorzystują psychologie pytając ze świdrującymi oczyma "Co widzisz na tym obrazku?".

Według mnie zbudowanie takiej układanki jest naturalne jeśli tylko spojrzymy w sposób abstrakcyjny i ścisły na prompt właśnie jako funkcje, czyli fragmenty kodu zapisane w języku naturalnym, które przyjmują pewne parametry oraz wynikowo zwracają jakiś rezultat.

Patrząc tak na to w ten sposób, naturalnym się staje, że prompty powinny:
- [ ] mieć tylko jedną odpowiedzialność i wywiązywać się z niej rzetelnie
- [ ] powinny przyjmować maksymalnie 3 argumenty dla zachowania skupienia
- [ ] powinny być komponowalne z innymi promptami, aby móc budować w sposób przejrzysty złożoność

Aby to podejście działo oczywiście konieczna jest możliwość wywoływania  promptów z innych promptów. W Claude Code tym mechanizmem jest wbudowane narzędzie *SlashCommand* wywołujące inny prompt aka slash command.
##### Przykład:
Załóżmy, że chcemy przygotować N alternatywnych podejść do jakieś implementacji. 

Możemy opisać to wszystko w ramach jednego prompta.

lub

W ramach dwóch promptów
1. jednego odpowiedzialnego za odpalanie N analiz i raportowanie
2. drugiego odpowiedzialnego za pojedyncza analizę.  
  
Drugie podejście wg mnie daje kompozycyjność, jakość i możliwość skupienia się na tym aby każdy prompt miał jasny cel. 

#### Narzędzia i procesy
W momencie gdy mamy już zbudowaną obszerną kolekcje naszych promptów wówczas niedogodnością staje się odwoływanie do nich poprzez coraz dziwniejsze, nie wpadające w pamięć nazwy. Mnie to właśnie napotkało i  postanowiłem sobie wówczas jakoś to zorganizować. Organizacją, którą przyjąłem składa się na załóżenia:

Każdy prompt jest dla mnie 
	1. *Narzędziem* (np. git, obsidian, figma) 
	2. *Procesem* składających się z fazy: 
		1. Meta promptingu
		2. Planowania
		3. Kodzenia
		4. Testowania
		5. Recenzowania
		6. Dokumentowania

Na podstawie powyższego i wykorzystując przestrzenie nazw w Claude Code (alternatywnie można tworzyć suffixy) przeniosłem wszystkie swoje prompty do odpowiednich podfolderów.
Teraz nie muszę zastanawiać się pod jaką wymyślną nazwą coś ukryłem, pytam siebie natomiast w jakiej fazie budowania jestem lub z jakiego narzędzia chcę właśnie skorzystać.