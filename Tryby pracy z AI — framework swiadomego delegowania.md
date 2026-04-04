# Tryby pracy z AI: framework świadomego delegowania

Chaotyczne, złożone, skomplikowane, proste. Które z tych słów opisuje sposób, w jaki dziś pracujesz z AI? I czy to Twój świadomy wybór, czy po prostu nawyk?

Różnica między "pracuję z jednym oknem czatu" a "zadania dzieją się w tle bez mojego udziału" to nie kwestia lepszego narzędzia. To kwestia dojrzałości systemu, któremu ufasz.

## Jedna oś

Każdy system pracy z AI, niezależnie od narzędzi, stacku czy organizacji, ma jeden wspólny wymiar: **tryb pracy**. Są cztery, ułożone na osi rosnącej autonomii.

Synchroniczna: pracujesz z jedną instancją AI w czasie rzeczywistym. Ty prowadzisz, AI asystuje. 

Równoległa: kilka instancji jednocześnie, kilka terminali, git worktrees. Ty koordynujesz. Dyrygent, nie pianista. 

Asynchroniczna: zlecasz zadanie i wracasz po wynik. Jules, Claude Code Web, Cursor Agents. Przychodzi PR, robisz review, mergujesz albo odrzucasz. 

W tle: praca dzieje się bez Twojego udziału. Cron, Webhook, `/loop`, `/dispatch`. Ty dowiadujesz się o efektach, nie o procesie.

Każdy tryb to inny poziom zaufania do narzędzia, do procesu, do siebie. **Im dalej w prawo potrafisz świadomie przesunąć swoją pracę, tym skuteczniejszy jesteś.** Ty i Twoja organizacja. Słowo "świadomie" jest tu kluczowe. Przesunięcie w prawo bez zrozumienia kosztu to nie odwaga. To niedbałość.

Naturalną konsekwencją tego stwierdzenia jest pytanie: kiedy i z czym mogę pracować w poszczególnych trybach? To trudniejsze pytanie niż wygląda. Zacznijmy od prostej analogii, która częściowo na nie odpowiada.

## Skojarzenie z Cynefin

Te cztery słowa, którymi zaczęliśmy, to nie przypadek. To domeny Cynefin, modelu który opisuje jak podejmujemy decyzje w zależności od tego, jak dobrze rozumiemy sytuację. Spotkałem się z nim po raz pierwszy na szkoleniu SCRUM-owym i to właśnie jego pamiętam z tych warsztatów najmocniej.

Proste (Clear): wiesz co robić, robisz. Skomplikowane (Complicated): nie wiesz od razu, ale ekspert znajdzie rozwiązanie. Złożone (Complex): nikt nie wie z góry, musisz próbować i obserwować. Chaotyczne (Chaotic): najpierw gaś pożar, potem myśl.

Naturalne skojarzenie narzuca się natychmiast:
Proste → W tle.
Skomplikowane → Asynchroniczna.
Złożone → Równoległa.
Chaotyczne → Synchroniczna.

I to skojarzenie jest... użyteczne. Ale nieprecyzyjne. Kiedy zacząłem je testować na własnej pracy, szybko się rozleciało.

## Gdzie analogia się sypie

Wyobraź sobie sytuację. Produkcja leży, logi są niezrozumiałe, klienci dzwonią. Chaos. Naturalnie zaczynasz synchronicznie: jedno okno z AI, każdy krok kontrolujesz ręcznie. Ale po godzinie chaos opada. Zidentyfikowałeś przyczynę, masz hipotezę, potrzebujesz fixa w trzech serwisach. Nagle ten sam problem, który godzinę temu wymagał Twojej ciągłej obecności, nadaje się do trybu asynchronicznego. Zlecasz, review'ujesz, mergujesz.

Problem się nie zmienił. Zmienił się kontekst.

Albo odwrotnie. Masz skomplikowany, dobrze zdefiniowany problem. Teoria mówi: asynchronicznie. Ale nigdy tego nie robiłeś i chcesz się nauczyć. Zostajesz przy synchronicznej, bo Twoja intencja to wiedza, nie wynik.

Cynefin mówi jaki jest problem. Tryby mówią ile zaufania dajesz agentowi. To dwie osobne decyzje. Cynefin pomaga zdiagnozować sytuację, ale złożoność zadania to dopiero jeden z wymiarów, który wpływa na wybór trybu. I to nawet nie najważniejszy.

## Czego nie widać na pierwszy rzut oka

Przez pewien czas myślałem, że wystarczy zapytać: "jak złożony jest ten problem?" i dopasować tryb. Ale jest coś, co potrafi zablokować przesunięcie w prawo niezależnie od tego, jak dobrze rozumiesz zadanie: ryzyko.

Ryzyko ma dwa składniki. Odwracalność, czyli czy możesz cofnąć to co agent zrobi. `git revert` to łatwa odwracalność. Migracja bazy produkcyjnej bez backupu to niemożliwa. I konsekwencja, czyli kto ucierpi i jak mocno zanim zdążysz cofnąć. Zmiana w wewnętrznym narzędziu którego nikt nie używa to inna kategoria niż zmiana w systemie płatności.

Te dwa składniki nie kompensują się nawzajem. **Łatwa odwracalność nie neutralizuje wysokiej konsekwencji.** Email do tysiąca klientów technicznie cofniesz (wysyłasz sprostowanie), ale pierwsze wrażenie zostało.

Gorszy z dwóch składników determinuje Twój maksymalny tryb. Krytyczna konsekwencja *albo* niemożliwa odwracalność, i jesteś z powrotem w synchronicznej, z człowiekiem w pętli.

Mogłoby się wydawać, że te dwa wymiary (złożoność i ryzyko) wystarczą. Proste i bezpieczne? W tle. Złożone i ryzykowne? Synchronicznie. Ale jest jeszcze jedna rzecz, o której nikt nie mówi.

## Agent jest tak dobry jak proces, w który go wsadzisz

Wszyscy mówią o modelach, narzędziach, benchmarkach. Nikt nie mówi o tym, że **możesz mieć proste, bezpieczne zadanie i nadal nie być gotowy żeby puścić je asynchronicznie**. Bo Twój proces nie jest na to dojrzały.

Co to znaczy "dojrzały"?

Po pierwsze: czy potrafisz opisać co chcesz z wystarczającą precyzją, żeby agent nie musiał zgadywać? W trybie synchronicznym możesz być mglisty, bo jesteś obok i korygujesz na bieżąco. W trybie "w tle" mglistość to błąd odkrywany za dwie godziny. Im dalej od klawiatury, tym precyzyjniejszy musisz być na starcie.

Po drugie: czy wiesz jak sprawdzić, że agent zrobił to dobrze? Testy, definicja "done", automatyczne gate'y. Bez tego scrollujesz PR, kiwasz głową, mergujesz i modlisz się że nic się nie wysypie.

Po trzecie: co się dzieje kiedy agent się myli? Bo się myli, regularnie. Rollback, monitoring, alerty. Tryb asynchroniczny bez obsługi awarii to samolot bez procedur awaryjnych.

I po czwarte: czy agent wie czego *nie* ma robić? Scope creep AI jest realny. Agent który dostał zadanie A potrafi po drodze "poprawić" B, C i D. Każda poprawka wygląda rozsądnie w izolacji. Razem tworzą bałagan którego nikt nie zamawiał.

Dojrzałość procesu to nie kolejny wymiar do zważenia. To warunek wstępny, bez którego reszta się sypie.

## Wchodzą też inne rzeczy

Są jeszcze wymiary które w konkretnych sytuacjach potrafią zdominować decyzję. 

Czasochłonność: pięciominutowy fix na którego opisanie potrzebujesz piętnastu minut nie ma sensu delegować asynchronicznie. 

Zaufanie do AI w danej domenie: nie do AI ogólnie, ale w konkretnym zastosowaniu. Testowałeś, widziałeś wyniki, wiesz gdzie model jest mocny a gdzie kłamie. Zaufanie bez danych to wiara, a wiara nie jest strategią inżynieryjną.

Intencja uczenia się: delegowanie czegoś czego nie rozumiesz tworzy kruche fundamenty. Działa, dopóki nie musisz debugować.

Każdy wymiar sugeruje swój próg. I tu docieramy do sedna.

## Bierzesz minimum

Jak złożyć te wszystkie wymiary w jedną decyzję? **Finalny tryb to najbardziej konserwatywna odpowiedź spośród wszystkich wymiarów.** Jeden "czerwony" wymiar blokuje całą resztę, nawet jeśli pozostałe sugerują pełną autonomię. Proste zadanie, doskonale zdefiniowane, z dojrzałym procesem, ale z krytyczną nieodwracalną konsekwencją? Człowiek w pętli. Zawsze.

Mosty oblicza się pod najgorsze obciążenie, nie pod średnie.

Dlatego ten sam typ zadania może wymagać innego trybu w innym kontekście. I dlatego pytanie "jaki tryb pasuje do tego rodzaju pracy?" jest złym pytaniem. To pytanie naiwne. Raz ustalone, stosowane mechanicznie. 

Kod → asynchronicznie. 
Konfiguracja → w tle. 
Architektura → synchronicznie.

Lepsze pytanie brzmi: co mi mówi każdy wymiar kontekstu i który z nich jest dziś najbardziej ograniczający?

Różnica wygląda na subtelną. W praktyce to różnica między systemem który skaluje Twoją skuteczność, a systemem który skaluje Twoje błędy.

**Tryb pracy z AI to nie cecha narzędzia. To decyzja, którą podejmujesz, albo którą podejmuje za Ciebie nawyk.** A nawyk nie czyta kontekstu. Nawyk powtarza ostatnią rzecz, która zadziałała.
