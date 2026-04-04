# Tryby pracy z AI: framework świadomego delegowania

Chaotyczne, złożone, skomplikowane, proste. Które z tych słów opisuje sposób, w jaki dziś pracujesz z AI? I czy to Twój świadomy wybór, czy po prostu nawyk?

Kilka lat temu siedziałem na szkoleniu SCRUM-owym. Trener narysował na tablicy dziwny diagram. Nie macierz, nie oś, ale coś w rodzaju mapy terenu. Cztery domeny, każda z inną logiką podejmowania decyzji. To był Cynefin. Z całego szkolenia zapamiętałem właśnie tę mapę. Nie ceremonie, nie role, nie artefakty. Mapę, która mówi: zanim zdecydujesz *jak* działać, musisz zrozumieć *gdzie* się znajdujesz.

Wtedy nie wiedziałem jeszcze, że ten sam schemat myślenia będzie mi potrzebny do czegoś zupełnie innego.

## Jedna oś, cztery tryby

Każdy system pracy z AI, niezależnie od narzędzi, stacku czy organizacji, ma jeden wspólny wymiar: **tryb pracy**. Są cztery, ułożone na osi rosnącej autonomii.

**Synchroniczna.** Pracujesz z jedną instancją AI w czasie rzeczywistym. Ty prowadzisz, AI asystuje. Klasyczne okno czatu, pair programming z Copilot, sesja w terminalu z Claude Code. Jesteś przy kierownicy w każdej sekundzie.

**Równoległa.** Kilka instancji AI jednocześnie. Kilka terminali, git worktrees, trzy czaty z różnymi kontekstami. Ty koordynujesz: rozdzielasz zadania, synchronizujesz wyniki, rozwiązujesz konflikty. Dyrygent, nie pianista.

**Asynchroniczna.** Zlecasz zadanie i wracasz po wynik. Jules od Google, Claude Code Web, Cursor Agents. Przychodzi PR, robisz review, mergujesz albo odrzucasz. Nie musisz być obecny w trakcie pracy. Musisz być obecny przy ocenie wyniku.

**W tle.** Praca dzieje się bez Twojego udziału. Cron, Webhook, `/loop`, `/dispatch`. System reaguje na zdarzenia, uruchamia agentów, dostarcza wyniki. Ty dowiadujesz się o efektach, nie o procesie.

Każdy tryb to inny poziom zaufania — do narzędzia, do procesu, do siebie.

**Im dalej w prawo potrafisz świadomie przesunąć swoją pracę, tym skuteczniejszy jesteś.** Ty i Twoja organizacja. Słowo "świadomie" jest tu kluczowe. Przesunięcie w prawo bez zrozumienia kosztu to nie odwaga. To niedbałość.

## Pierwsze skojarzenie: Cynefin

Te cztery słowa, którymi zaczęliśmy, to nie przypadek. To domeny Cynefin, modelu który opisuje, jak podejmujemy decyzje w zależności od tego, jak dobrze rozumiemy relację przyczyna-skutek w danej sytuacji.

Proste (Clear): wiesz co robić, robisz. Best practice istnieje i działa.
Skomplikowane (Complicated): nie wiesz od razu, ale możesz się dowiedzieć. Ekspert analizuje, znajduje rozwiązanie.
Złożone (Complex): nikt nie wie z góry. Musisz próbować, obserwować, reagować.
Chaotyczne (Chaotic): najpierw gaś pożar, potem myśl.

Naturalne skojarzenie narzuca się natychmiast:
Proste → W tle.
Skomplikowane → Asynchroniczna.
Złożone → Równoległa.
Chaotyczne → Synchroniczna.

I to skojarzenie jest… użyteczne. Ale nieprecyzyjne. I właśnie ta nieprecyzyjność jest ciekawsza niż samo dopasowanie.

## Dwie różne osie

Cynefin opisuje naturę problemu, czyli jak dobrze rozumiesz relację przyczyny i skutku. To narzędzie diagnostyczne: mówi Ci *gdzie jesteś*. Framework trybów opisuje coś innego, ile zaufania dajesz agentowi. To narzędzie decyzyjne: mówi Ci *jak chcesz pracować*.

**To są dwie niezależne decyzje.**

Weźmy przykład.
Masz chaotyczny problem. Produkcja leży, logi są niezrozumiałe, klienci dzwonią. Naturalnie zaczynasz synchronicznie: jesteś z AI w jednym oknie, każdy krok kontrolujesz ręcznie. Ale po godzinie chaos opada. Zidentyfikowałeś przyczynę, masz hipotezę, potrzebujesz fixa w trzech serwisach. Nagle ten sam problem, który godzinę temu wymagał Twojej ciągłej obecności, nadaje się do trybu asynchronicznego. Zlecasz, review'ujesz, mergujesz.

Albo odwrotnie. Masz skomplikowany, ale dobrze zdefiniowany problem: migracja bazy danych, pięć tabel, znane schematy. Teoria mówi: asynchronicznie, niech agent pracuje. Ale Ty nigdy tego nie robiłeś. Chcesz się nauczyć. Zostajesz przy synchronicznej, bo **Twoja intencja to wiedza, nie wynik**. I to jest świadomy, dobry wybór.

Cynefin pomaga Ci zdiagnozować sytuację. Ale diagnoza to dopiero początek decyzji o trybie.

## Co naprawdę determinuje tryb

Skoro Cynefin to tylko jeden z wymiarów, to co jeszcze wchodzi do gry? Tryb pracy z AI jest zmienną zależną. Nie wybierasz go raz. Jego wartość wynika z kilku niezależnych wymiarów kontekstu, które musisz ocenić za każdym razem.

### Złożoność zadania

To jest ten wymiar Cynefin. Jak dobrze zdefiniowany jest Twój problem? Czy wiesz co chcesz, jak to zmierzyć, i jak wygląda "done"? Im mniej wiesz, tym bliżej synchronicznej powinno Cię to trzymać. Nie dlatego, że AI sobie nie poradzi, ale dlatego, że Ty nie wiesz jeszcze czego szukasz. Trudno review'ować coś, czego nie potrafisz opisać.

### Ryzyko: dwa wymiary, nie jeden

Ryzyko to nie jedno słowo. To dwie niezależne osie.

**Odwracalność** to właściwość techniczna akcji. Czy możesz cofnąć? `git revert` to łatwa odwracalność. Migracja bazy produkcyjnej bez backupu to niemożliwa. Email wysłany do tysiąca klientów: technicznie odwracalny (wysyłasz sprostowanie), praktycznie nie (pierwsze wrażenie zostało).

**Konsekwencja** to właściwość ludzka i biznesowa. Kto ucierpi i jak mocno, zanim zdążysz cofnąć? Zmiana w wewnętrznym narzędziu, którego nikt dziś nie używa? Niska konsekwencja. Zmiana w systemie płatności? Krytyczna.

I jest tu asymetria, którą łatwo przeoczyć: **nie skompensujesz wysokiej konsekwencji łatwą odwracalnością**. Szkoda powstaje *zanim* zdążysz zareagować. Utrata zaufania klientów jest technicznie odwracalna: naprawiasz system, wysyłasz przeprosiny, wdrażasz poprawki. Ale zaufanie nie wraca automatycznie z rollbackiem. Rollback cofnie kod. Nie cofnie emocji.

Praktyczna reguła: oba wymiary wchodzą jako ograniczniki. Najgorszy z nich determinuje Twój maksymalny tryb. Krytyczna konsekwencja *albo* niemożliwa odwracalność, i jesteś z powrotem w synchronicznej, z człowiekiem w pętli. Niezależnie od tego jak prosty jest sam problem.

### Dojrzałość procesu

Wszyscy mówią o modelach, narzędziach, benchmarkach. Nikt nie mówi o tym, że **agent jest tak dobry jak proces, w który go wsadzisz**. To nie kolejny wymiar do zważenia. To warunek wstępny, bez którego reszta się sypie.

Co musi być dojrzałe? Potrafię to sprowadzić do czterech rzeczy.

Po pierwsze, definiowalność zadania. Czy potrafisz opisać co chcesz z wystarczającą precyzją, żeby agent nie musiał zgadywać? W trybie synchronicznym możesz być mglisty, bo jesteś obok i korygujesz na bieżąco. W trybie "w tle" mglistość to błąd odkrywany za dwie godziny. Im dalej od klawiatury, tym precyzyjniejszy musisz być na starcie.

Po drugie, weryfikowalność wyniku. Czy wiesz jak sprawdzić, że agent zrobił to dobrze? Testy, definicja "done", automatyczne gate'y. Bez tego scrollujesz PR, kiwasz głową, mergujesz i modlisz się, że nic się nie wysypie.

Po trzecie, obsługa awarii. Co się dzieje kiedy agent się myli? Bo się myli, każdy agent, każdy model, regularnie. Rollback, monitoring, alerty, procedury eskalacji. Tryb asynchroniczny bez obsługi awarii to samolot bez procedur awaryjnych. Dopóki wszystko idzie dobrze, nie widzisz problemu. Kiedy przestaje, jest za późno na projektowanie rozwiązań.

Po czwarte, granice mandatu. Czy agent wie czego *nie* ma robić? Scope creep AI jest realny i podstępny. Agent który dostał zadanie A potrafi po drodze "poprawić" B, C i D. Każda z tych poprawek wygląda rozsądnie w izolacji. Razem tworzą bałagan, którego nikt nie zamawiał i nikt nie przeglądał.

Te cztery filary to nie checklist do odhaczenia raz. To pytania, które zadajesz sobie przy każdym przesunięciu w prawo. Dojrzałość procesu nie jest stanem. Jest praktyką.

### Co jeszcze wchodzi do gry

Poza złożonością, ryzykiem i dojrzałością procesu jest kilka wymiarów, które traktuję jako mniej uniwersalne, ale w konkretnych sytuacjach potrafią zdominować decyzję.

Czasochłonność: czy koszt precyzyjnego zdefiniowania zadania dla agenta nie przekracza kosztu zrobienia tego samemu? Pięciominutowy fix, na którego opisanie potrzebujesz piętnastu minut, nie ma sensu delegować asynchronicznie.

Zaufanie do AI w danej domenie. Nie do AI ogólnie, ale w konkretnym zastosowaniu. Twoje zaufanie powinno wynikać z historii: testowałeś, widziałeś wyniki, wiesz gdzie model jest mocny a gdzie regularnie kłamie. Zaufanie bez danych to wiara. A wiara nie jest strategią inżynieryjną.

Intencja uczenia się: czy chcesz wynik, czy wiedzę? To wymiar który potrafi wyciągnąć Cię z powrotem w lewo, do synchronicznej, nawet przy trywialnym zadaniu. I słusznie, bo delegowanie czegoś czego nie rozumiesz tworzy kruche fundamenty. Działa, dopóki nie musisz debugować.

Kontekst organizacji: kultura, regulacje, branża. Bank inaczej waży ryzyko niż startup na wczesnym etapie. Zespół w regulowanej branży ma inne granice mandatu niż solo developer na side projekcie. Framework jest ten sam, wagi się zmieniają.

## Reguła syntezy

Masz wymiary. Masz dla każdego z nich odpowiedź, od "pozwala na pełną autonomię" po "wymaga ciągłej kontroli". Jak je złożyć w jedną decyzję?

**Finalny tryb = najbardziej konserwatywna odpowiedź spośród wszystkich wymiarów.**

Bierzesz minimum. Jeden "czerwony" wymiar blokuje całą resztę, nawet jeśli pozostałe sugerują pełną autonomię. Proste zadanie, doskonale zdefiniowane, z dojrzałym procesem, ale z krytyczną nieodwracalną konsekwencją? Człowiek w pętli. Zawsze.

To jest projektowanie systemów które muszą być niezawodne. Mosty oblicza się pod najgorsze obciążenie, nie pod średnie. Z delegowaniem pracy agentom jest tak samo.

Dlatego ten sam typ zadania może wymagać innego trybu w innym kontekście. Deployment na staging kontra deployment na produkcję. Ten sam kod, te same narzędzia, zupełnie inna decyzja o trybie, bo zmienił się wymiar konsekwencji.

## Trzy własności frameworku

Ten framework ma trzy cechy, które moim zdaniem czynią go użytecznym w praktyce.

Jest **przenoszalny**, bo oś autonomii jest uniwersalna. Pasuje do każdej organizacji, każdego stacku, każdej pracy z AI. Nie musisz go przepisywać, kalibrujesz wagi wymiarów.

Jest **kontekstowy**, bo różne organizacje będą różnie ważyć wymiary. Bank nada ryzyku wagę krytyczną. Startup złagodzi ryzyko na rzecz szybkości. Zespół uczący się nowej domeny nada wysoki priorytet intencji uczenia się, co będzie ich spychać w stronę synchronicznej nawet przy prostych zadaniach. I to jest w porządku.

Jest **dynamiczny**, bo wymiary zmieniają się w trakcie projektu. Ten sam task może być chaotyczny w poniedziałek i prosty w środę, bo w międzyczasie zrozumiałeś problem, napisałeś testy, zbudowałeś obsługę awarii. Tryb pracy powinien to śledzić, nie być ustalony raz na zawsze.

## Przed delegacją

Naiwne podejście: "jaki tryb pasuje do tego rodzaju pracy?" Raz ustalony, stosowany mechanicznie. Kod → asynchronicznie. Konfiguracja → w tle. Architektura → synchronicznie.

Świadome podejście: "co mi mówi każdy wymiar kontekstu i który z nich jest dziś najbardziej ograniczający?"

Różnica wygląda na subtelną. W praktyce to różnica między systemem który skaluje Twoją skuteczność, a systemem który skaluje Twoje błędy.

**Tryb pracy z AI to nie cecha narzędzia. To decyzja, którą podejmujesz, albo którą podejmuje za Ciebie nawyk.** A nawyk nie czyta kontekstu. Nawyk powtarza ostatnią rzecz, która zadziałała.

Zanim następnym razem otworzysz czat z AI, zadaj sobie jedno pytanie: czy tryb w którym zaraz zacznę pracować to mój świadomy wybór, czy autopilot?
