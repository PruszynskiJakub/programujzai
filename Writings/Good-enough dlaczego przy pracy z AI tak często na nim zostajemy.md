---
author: "[[Sebastian Druciak]]"
---

### Backstory
Od dłuższego już czasu obserwuje board na linkedin, kursy o tematyce AI, oraz współpracowników w firmie i obserwuje jak wszyscy zatrzymują się na przyjęciu konwencji good-enough
- udaje mi się wygenerować kod który prawie pokrywa wymagania funkcjonalności - a to prawie oznacza, przekope większości kodu aby przynajmniej matchowała kowencje projektowe, doklepuje brakujące części kodu,
- mój jedyny tool jaki używam to cursor, bo migracja na niego zajęła chwilę, w końcu używałem VSC,
- kod który generuje jest błędny, nie wspiera moich konwencji, źle formatuje i ogólnie to się nawet nie kompiluje!
- znowu AI mielił 10 minut, przekopał masę niepotrzebnych rzeczy - jest do niczego!
- przekopiowuje kod do chatu gpt, a następnie spowrotem do IDE! Rezultaty są bardzo zadowalające!

AI ma to do siebie, że ma bardzo, ale to bardzo niski niski próg wejścia, plus aktualnie modele bardzo dużo wybaczają, a narzędzia w teorii próbują ułatwiać życie.
Bardzo łatwo można wpaść w pułapkę i łykać co przyjmuje z minimalnym setupem / effortem, a później męczyć się i poprawiać to ręcznie.
Jednak jak z każdym narzędziem potrzeba czasu, obycia się, chęci rozwoju, refleksji i przede wszystkim rozwoju.
Kurde IDE jak np. Intellij jak zaczynałem w nim pracę od samego początku dawał mi wiele - sama nawigacja po plikach, generowanie boilerplate'u to było coś! Jednak czas w nim poświęcony, odkrywanie "ukrytych" funkcjonalności, skrótów klawiszowych - a przede wszystkim budowanie nawyków tak naprawdę dało pełnego powera.

Dlaczego z AI nie mamy tyle cierpliwości? Dlaczego nie zatrzymujemy się nad naszym propmptem, nie pomyślimy co mógłbym zrobić aby output był bardziej nakierowany na moje oczekiwania, czy mogę wykorzystać jakiegoś dodatkowego narzędzia, który jeszcze mi w tym pomoże?

Kursy natomiast wciąż obracają się wokół hype'u zbudowanego wokół AI, powtarzają podobną treść, tylko przedstawioną w inny dostosowany pod siebie sposób. Brakuje na rynku treści po eksploracji, po przetestowaniu masy rozwiązań i przedstawieniu swoich wniosków - bo to głównie na nich jesteśmy w stanie budować prawdzie workflow

AI to narzędzie jak każde inne! Dopiero po odpowiednim czasie esploracji nabiera rozpędu i otwiera drzwi, które przy podejściu good-enough są zamknięte!

---

## LinkedIn Post Draft

### Hook:
"Dlaczego 90% developerów używa AI na poziomie 'good enough' i frustruje się, że kod się nie kompiluje?"

### Post:

**Problem:**
Obserwuję LinkedIn, kursy AI, współpracowników. Wszędzie to samo zjawisko - zatrzymujemy się na "good enough". 
Zbieram często feedback z użycia AI taki jak:
- "AI wygenerował kod który *prawie* działa"
- "Przeklejam z ChatGPT do IDE i poprawiam ręcznie"
- "Używam tylko Cursor, bo przesiadka z VSCode była łatwa"
- "AI mielił 10 minut i wypluł śmieci!"

**Journey:**
Przy natłoku pracy sam byłem w podobnym miejscu, output był dla mnie good enough, a przy dostosowaniu kilku plików było to rozwiązanie którego szukałem - bez większej refleksji i zastanowienia się czy można było nakierować lepiej inicjalny output.

AI to narzędzie jak każde inne, kiedy kilka już dobrych lat temu zaczynałem używać IntelliJ jako głównego IDE od razu widziałem boost w swojej pracy - nawigacja po plikach, czy generacja boilerplate kodu wydawała się czymś naprawdę potężnym, ale moc tego IDE wyciągnąłem dopiero po miesiącach pracy i wciąż zdarza się, że odkrywam funkcjonalność i strzelam facepalm, że wcześniej tego nie wiedziałem.
Dlaczego więc z AI robimy dokładnie odwrotnie? Oczekujemy perfekcji od razu, a przecież jest to narzędzie w pewnym stopniu jak każde inne.

Aż przypomniałem sobie swoje początki z IntelliJ...

Pierwsze dni: "Okej, nawigacja po plikach jest spoko"
Po miesiącu: "O, są snippety!"
Po roku: "Refactoring, debugger, profiler - jak ja bez tego żyłem?"

Z AI robimy dokładnie odwrotnie. Oczekujemy perfekcji od razu.

**Lesson:**
AI to nie ChatGPT window. To ekosystem:
- Context windows (używasz .cursorrules? .aider.conf.yml?)
- Prompt engineering (nie "napisz kod", ale struktura, przykłady, ograniczenia)
- Tool chaining (Cursor + Aider + własne skrypty)
- Feedback loops (dlaczego ten output był zły?)

Przestałem traktować AI jak magiczną różdżkę. Zacząłem traktować jak IntelliJ - narzędzie wymagające nauki.

**Broader insight:**
Niski próg wejścia AI to pułapka. Łatwo zacząć, trudno przejść dalej.

Kursy sprzedają hype: "10x developer w weekend!"
Realność: Potrzebujesz miesięcy eksploracji, testowania workflows, budowania nawyków.

Good enough = copy-paste z ChatGPT
Mastery = zintegrowany workflow gdzie AI rozumie twój kontekst, konwencje, cele

**CTA:**
Jaki był twój "aha moment" z AI tools? Ten moment gdy przestałeś walczyć z narzędziem, a zacząłeś z nim współpracować?

---

AI w mojej opinii za mało przedstawiane jest jako narzędzie.

Kiedy kilka już dobrych lat temu zaczynałem używać IntelliJ jako głównego IDE od razu widziałem boost w swojej pracy - nawigacja po plikach, czy generacja boilerplate kodu wydawała się czymś naprawdę potężnym, ale moc tego IDE wyciągnąłem dopiero po miesiącach pracy i wciąż zdarza się, że odkrywam funkcjonalność i strzelam facepalm, że wcześniej tego nie wiedziałem.

Z AI robimy dokładnie odwrotnie. Oczekujemy perfekcjonizmu od pierwszego promptu.
Wypluł śmieci, cóż może to za wcześnie? Sprawdzę jak pojawi się nowy model! :)

Narzędzia i aktualne modele wybaczają już naprawdę wiele, ale wciąż przykuwamy zbyt mało uwagi na to jak ich używamy. Obserwuję to środowisko i w wielu przypadkach zatrzymujemy się na podejściu good enough i bare minimum :P 

Np. 
- Używam Cursor'a bo migracja z VSC była bezproblemowa,
- Output co prawda nie trzymał konwencji projektowej i pojawiła się masa błędów w formatowaniu, ale przecież poprawiłem ręcznie i czuję, że udało się dostarczyć szybko

Traktowanie AI jako narzędzie, poznawanie go, eksploracja dają masę efektów, ale z jakiegoś powodu tylko garstka naprawdę widzi ten potencjał...