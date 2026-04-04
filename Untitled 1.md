
Chaotyczne, złożone, skomplikowane, proste. Które z tych słów opisuje sposób, w jaki dziś pracujesz z AI — i czy to Twój świadomy wybór, czy po prostu nawyk?

Różnica między "pracuję z jednym oknem czatu" a "zadania dzieją się w tle bez mojego udziału" to nie kwestia lepszego narzędzia. To kwestia dojrzałości systemu, któremu ufasz.

Każdy system pracy z AI — niezależnie od narzędzi — ma jeden wspólny wymiar: tryb pracy. 
Są cztery:

![[00-Załączniki/Untitled 1/3e17492233773f08c3b8ca4412531f9c_MD5.jpeg]]

Co kryje się pod poszczególnymi terminami ?

Synchroniczna - pracujesz z jedną instancją AI  
Równoległa - pracujesz z kilkoma instancjami AI np kilka terminali, worktrees  
Asynchroniczna - zlecasz coś i potem robisz PR tylko np. Jules od Google albo Claude Code Web albo Cursor Agents  
W tle - praca po prostu dzieje się ze względu na Cron, Webhook etc np Claude Code /loop lub /dispatch  

Każdy tryb to inny poziom zaufania — do narzędzia, do procesu, do siebie.

![[00-Załączniki/Untitled 1/2199b320c2dfc370ba2bfb0c4d88dff2_MD5.jpeg]]

Im dalej w prawo potrafisz świadomie przesunąć swoją pracę, tym skuteczniejszy jesteś — Ty i Twoja organizacja. Słowo "świadomie" jest tu kluczowe.
Naturalną konsekwencją tego stwierdzenia jest pytanie. 
Kiedy i z czym mogę pracować w poszczególnych trybach ? To już zdecydowanie trudniejsze pytanie. Zacznijmy od prostej analogii, która częściowo na to pytanie odpowiada.

Te cztery słowa, którymi zaczęliśmy, to nie przypadek. 
To domeny Cynefin — modelu, który opisuje, jak podejmujemy decyzje w zależności od tego, jak dobrze rozumiemy sytuację. Spotkałem się z nim po raz pierwszy w ramach szkolenia SCRUM-owego, i to właśnie jego pamiętam z tych warsztatów najmocniej.

Wygląda on mniej więcej tak:

![[00-Załączniki/Untitled 1/eaa20eee58f0ca3e1044ebb54f0cbc8c_MD5.jpeg]]

I tak SCRUM jako metodologia znajduje się w obszarze Złożone, a Waterfall w Skomplikowane, a stara i poczciwa lista TODO jako Proste.

Okazuje się, że tryby pracy z AI poniekąd wpasowują się w ten model. 

![[00-Załączniki/Untitled 1/64a6d4be43d7bb0a993fb69a1ca954b2_MD5.jpeg]]

Oczywiście jest to zbyt duże uproszczenie.
Cynefin - help leaders make decisions by categorizing problems based on how clearly cause-and-effect relationships can be identified

Cynefin mówi: jaki jest problem.
Tryby AI mówią: ile zaufania dajesz agentowi. To osobna decyzja.




Typ zadania
	Złożoność




Ryzyka
	Odwracalność
	Konsekwencje


Wszyscy mówią o modelach, narzędziach, trybach. Nikt nie mówi o tym, że agent jest tak dobry jak proces, w który go wsadzisz.

Zacznijmy od pytania bazowego: co właściwie musi być "dojrzałe" żeby można było bezpiecznie przesunąć się w prawo?



[[00-Załączniki/Untitled 1/0754dcecda122ea8792f7eb53ae8ca97_MD5.jpeg|Open: Screenshot 2026-04-04 at 11.26.42.png]]
![[00-Załączniki/Untitled 1/0754dcecda122ea8792f7eb53ae8ca97_MD5.jpeg]]
[[00-Załączniki/Untitled 1/35b461c8bf3561a48ebc6c000ee4e92f_MD5.jpeg|Open: Screenshot 2026-04-04 at 11.34.27.png]]
![[00-Załączniki/Untitled 1/35b461c8bf3561a48ebc6c000ee4e92f_MD5.jpeg]]

Każdy wymiar sugeruje swój próg. Finalny tryb = najbardziej konserwatywna odpowiedź.
Dlatego ten sam typ zadania może wymagać innego trybu w innym kontekście.


trzy własności tego frameworku.

Jest **przenoszalny**, bo oś autonomii jest uniwersalna — pasuje do każdej organizacji i każdej pracy z AI. Nie musisz go przepisywać, tylko kalibrować wagi wymiarów.

Jest **kontekstowy**, bo różne organizacje będą różnie ważyć wymiary. Bank nada ryzyku wagę krytyczną. Startup na wczesnym etapie może złagodzić ryzyko na rzecz szybkości. Zespół uczący się nowej domeny nada wysoki priorytet intencji uczenia się, co ich spychać będzie w stronę synchronicznej nawet przy prostych zadaniach.

Jest **dynamiczny**, bo te wymiary zmieniają się w trakcie projektu. Ten sam task może być Chaotic w poniedziałek i Clear w środę — i tryb pracy powinien to śledzić, nie być ustalony raz na zawsze.

Praktyczny wniosek: przed delegacją zadania nie pytasz "jaki tryb pasuje do tego rodzaju pracy", ale "co mi mówi każdy wymiar kontekstu i który z nich jest dziś najbardziej ograniczający".