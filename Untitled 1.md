Super, w poprzedniej publikacji powiedzieliśmy sobie o tym jakie są kluczowe pojęcie oraz jak wygląda proces dekompozycji u jego podstaw.

**Materiały → Procesy → Scenariusze → User Stories**

Dziś pójdziemy krok dalej i powiemy o tym jak tą dekompozycję zdecydowaliśmy się wspierać wraz z AI.

Kilka założeń na początek, i powód za nimi stojących.
Mianowicie organizacja z którą współpracuje pracuje na wielu projektach jednocześnie, na bardzo zróżnicowanym stosie technologicznym, dodatkowo zespoły dość często rotują, podobnie z resztą jak same projekty, dodatkowo poziom wiedzy i umiejętności korzystania z AI też oscyluje.

Biorąc to pod uwagę, potrzebowaliśmy stworzyć rozwiązanie które:
- jest agnostyczne względem projektu
- jest agnostyczne względem narzędzia AI
- pozwala w prosty sposób synchronizować, nowe praktyki pomiędzy wszystkimi zespołami
- jest elastyczne i pozwala na proste rozszerzanie możliwości
- pozwala na dzielenie tooling wokół AI pomiędzy zespołami


Dodatkowe wyzwania:
- review rezultatów nie powinno zajmować więcej niż 10 min
- nie wspiera generowania tony treści, której nikt nie przeczyta
- pozwala na weryfikację treści przez człowieka
- domyślanie się niektórych rzeczy, które nie są jednoznacznie wyróżnione w materiał
- zachowania skuteczności wraz z czasem i wzrostem objętości danych
- możliwość kontrolowania autonomiczności agenta  

Jak widać wyzwań było sporo, generalnie większość z nich w pierwszej kategori daliśmy radę rozwiązać dość szybko bo i decyzje były dość oczywiste:
- system plików - organizacja i strukturyzacja 
- pliki markdown - przystępne dla AI i człowieka
- repozytorium git - zarządzanie wersjami, dzielenie zasobów

Natomiast druga kategoria jak to zwykle bywa była większym wyzwaniem, mianowicie szukanie proste i skutecznego rozwiązania dla większego grona odbiorców nie jest trywialne.
Iteracji było kilka.
Pierwotne, dość naiwne rozwiązanie w postaci transformacji z jednego etapu na kolejny, mimo że skuteczne nie było przyjazne. Skille w tym podejściu były wieloetapowymi procesami, które zaczynały od discovery aktualnej wiedzy, poprzez stworzenia draftu, a następnie samokrytykę z pomocą subagentów. Niestety przy tym podejściu agent pracował długo, a efekty mimo, że zadawalające były przytłaczające w swej ilości. Dodatkowo kognitywnie wymagającym było jednoczesne zrozumienie co się zadziało, dlaczego a następnie jeszcze ocenić jakość samego rezultatu.

W ramach tego założenia kluczowym skillem było skanowanie czy to na etapie Materiałów czy też dalej, które z jedno lub kilku dokumnetów generował jeden lub więcej dokumentów reprezentujący kolejny etap.

Dla przykładu rezultatem skanowanie materiałów z danego dnia były dokumenty opisujące zidentyfikowane procesy biznesowe.

Oczywiście skill w ramach prompta, wpierw wyświetlał sugerowaną dekompozycję w ramach okna czatu, co też stanowiło kiepski UX.

Kolejne próby starały się zaadresować wymienione wyżej bolączki w mniej lub bardziej skuteczny sposób. Granulacja skilli, uproszczenie ich czy też zrezygnowanie z niektórych etapów na rzecz szybkości to niektóre z przykładów. Rezygnacja z transformacji wielu procesów, na rzecz skupienia się na jednym.
Innymi słowy trochę zmian z perspektywy Context Engineeringu.


Mimo, że do skanowania dołaczył kolejny zestaw skill skupionych wokół dekompozycji.
Czytaj mając np pojedynczy proces wywolywalismy skill decompose który proponował po etapie samokrytyki listę scenariuszy.

Niestety dalej żadne z podejść nie dawało takiego poczucia satysfakcji jakiego poszukiwałem.

Tym sposobem wróciliśmy do deski kreślarskiej (w moim wypadku to było miro oraz excalidraw) i zadaliśmy sobie serię kolejnych pytań kwestionujących niektóre z naszych pierwotnych pomysłów. 
Tym sposobem doszliśmy do kilku kluczowych obserwacji:
- Surowe materiały chcemy przetwarzać tylko jeden raz i ani razu więcej. Są to dane nieuporządkowane, często chaotyczne i nieustrukturyzowane, zawierające również sporo szumu
- Na etapie przetwarzania surowych materiałów nie interesuje nas ich relacja z aktualnym stanem procesów, scenariuszy ani tym bardziej historyjek użytkownika.
- W tym rozwiązaniu jest przestrzeń na zastosowanie jednej z praktyk deweloperskich popularnych z AI mianowicie Spec Driven Development

Te spostrzeżenia okazały się brakującymi elementami aby zaadresować wszystkie nasze bolączki.

Jak to wszystko wygląda zatem finalnie.
Każdy z etapów Materiały/Procesy biznesowe/Scenriusze jest obsługiwany przez 3 dedykowane skille, każdy z nich obejmuję następująco:
1. skanowanie - czyli identyfikację kluczowych elementów dla etapu. W wypadku materiałów będą to pojęcia słownika oraz procesy, dla procesów będą to scenariusze, a dla scenariuszy user stories - skupiamy się wyłączenie na zrozumieniu tego co oferują nowe informacje i nic więcej
2. zderzenie - czyli porównanie odkryć z kroku pierwszego z aktualnym stanem wiedzy, czyli np. zidentyfikowane procesy zderzamy już z istniejącymi, dzięki temu na tym etapie skupiamy się wyłącznie na zrozumieniu tych informacji w kontekście naszego system
3. konsolidacja - czyli powiązanie nowych informacji z aktualnym stanem systemu, utworzenie np nowych procesów lub modyfikację już istniejących

Wynikiem tego 3 krokowego przetwarzania jest dokument stanowiący specyfikację reprezentującą snapshot zmian systemu, które zostaną wprowadzone, i na scenę wchodzi kolejny skill - implement - który wprowadza wszystkie zmiany zdefiniowane wewnątrz specyfikacji.

Tym sposobem uzyskujemy rozwiązanie które stanowi świetny fundament do dalszego rozwoju. jest elastyczne, pozwala na dowolnośc w postaci dołączania nowych workflows, odpalanie krytyków etc, pozwala na łatwą analizę artefaktów pośrednich i ich modyfikację w razie potrzeby przez użytkownika. Co wg mnie najważniejsze zachowuje użytkownika zaangażowane, bo pętle są krótkie i pozwalają na szybki feedback.



