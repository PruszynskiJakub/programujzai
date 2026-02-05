Ta publikacja jest kontynuacją o tym jak zrozumieć ewaluację AI i wykorzystać je w praktyce.

Langfuse to open-source'owe rozwiązanie do observability i ewaluacji aplikacji AI. Wybrałem je ze względu na możliwość self-hostingu oraz rozsądne ceny w wersji hostowanej. Ten artykuł to zbiór moich osobistych doświadczeń, wyciągniętych wniosków i otwartych pytań, które pojawiały mi się w głowie przed budowaniem pierwszych aplikacji AI.

Oto pytania, na które szukałem odpowiedzi — i na które chciałbym znać odpowiedzi zanim zacząłem pracę z Langfuse:

1. Jak wygląda cały proces ewaluacji w Langfuse?
2. Kiedy używać konkretnych typów promptów wspieranych przez platformę?
3. Dlaczego integracja Langfuse z Langchain nie jest idealna — i jak sobie z tym radzić?
4. Jak skutecznie przeprowadzać eksperymenty i co powinny obejmować?
5. Jak budować datasety — jakie dane wejściowe i wyjściowe, od czego zacząć?
6. Jak zarządzać promptami, środowiskami i kodem eksperymentów?
7. Czy w eksperymentach używać produkcyjnych narzędzi czy mocków?

Na pewnym etapie budowania aplikacji z AI będziemy chcieli wyjść poza strefę eksperymentowania, wprowadzania modyfikacji w promptach i narzędziach wyłącznie z pomocą naszej intuicji, będziemy chcieli odzyskać kontrolę. 

Zderzając się pierwszy raz tymi wszystkimi terminami możemy czuć się przytłoczeni ilością różnych dziwnie brzmiących pojęć i ich powiązań. Wypiszmy je sobie aby uporządkować wiedzę:
- Score Config - to definicja metryki i wartości jakie może przyjąć 
- Score - to po prostu metryka, może być reprezentowana przez wartość liczbową, wartość Prawda/Fałsz lub stanowić kategorię z wartościami w postaci etykiet
- Annotation Queue - to kolejka wyselekcjonowanych ręcznie lub automatycznie traces, które wymagają manualnej analizy przez człowieka
- Dataset - to zbiór par input + expected output, które stanowią reprezentację danych jakie przyjmuje nasz agent lub jakaś jego składowa
- Eksperyment - to proces, rozpoczęty hipotezą, obejmujący weryfikację tej hipotezy na podstawie rzetelnych danych i zakończony decyzją oraz wnioskami dotyczącymi prawdziwości postawionej hipotezy

Mając już wspólne zrozumienie możemy przedstawić jak te wszystkie rzeczy łączą się.
Z jednej strony mamy mianowicie rzeczy, które pozwalają nam postawić hipotezę, z drugiej rzeczy którą tą hipotezę pozwalają nam zbadać.
Do pierwszej kategorii należy Score Config, Score i Annotation Queue.
Mianowicie aby zastosować podejście Open Codes i Axial Codes, które pozwalają nam nie tylko lepiej zrozumieć błędy zachodzące w aplikacji, ale również określić ich kategorię i skalę potrzebujemy binarnej metryki (Score), którą potrzebujemy utworzyć poprzez Score Config, aby ta metryka finalnie była dla nas dostępna w Annotation Queue aka Human Annotation. 


Do drugiej Dataset oraz Eksperyment.
Tutaj natomiast gdy już postawiliśmy np. hipotezę o tym co stanowi źródło konkretnego błędu, jesteśmy w stanie zbudować zróżnicowany zestaw danych, który kończy się tym błędem, a następnie wprowadzić zmianę np. w naszym promptcie celem werfyikacji wyników.

Hipotezy mogą obejmować niemal wszystko nie tylko zaobserwowane błędy. Przykładowe inne hipotezy to:
- niewrażliwość aplikacji na prompt injection
- przyznawanie się do niewiedzy gdy agent nie ma dostatecznej wiedzy
- umiejętność wybrania odpowiedniej trajektorii narzędzi gdy zadanie jest skomplikowane i wieloetapowe
- umiejętność zbudowania odpowiedniego zapytania do narzędzia 

A więc kontekst:
Buduję aplikację konwersacyjnego agenta AI mającego dostęp do pokaźnego zbioru narzędzi.
Ze względu na istniejący już backend w języku Python zdecydowałem się na wykorzystanie właśnie kombinacji 
- Langchain - framework do zbudowania agenta oraz jego toolingu
- Langfuse - zarządzenie promptami, ekspertymenty, ewaluacja

Pierwsza obserwacja mimo, że Langfuse chwali się integracją z Langchain to nadal jest sporo 





----
Lista pytań na które szukałem odpowiedzi lub chciałbym znać odpowiedzi na początku pracy z projektami AI:
1. Jak skutecznie przeprowadzać eksperymenty ?
2. Co powinny obejmować eksperymenty ?
3. Jak skutecznie zarządzać promptami i środowiskami aby eksperymentowanie oraz analiza były możliwe przyjazne ?
4. Kiedy i dlaczego używać konkretnych typów  promptów wspieranych przez Langfuse ?
5. Jakie dane wejściowe i wyjściowe powinny obejmować elementy datasetów ?
6. Jak wygląda cały proces ewaluacji ?
7. Dlaczego połączenie narzędzi Langfuse <> Langchain nie jest idealne? 
8. Dlaczego  trace id się nie przypisuje gdy używasz uuid np wiadomości ? 
9. Jak przeprowadzić analizę Open Codes i Axial Codes w Langfuse ?
10. Gdzie w kodzie trzymać eksperymenty ?
11. Czy przeprowadzając eksperymenty powinniśmy przekazywać produkcyjne narzędzia czy też mocki/stuby ?
12. Jak zacząć budować pierwszy dataset pierwszy z którym będziemy nieprzerwanie eksperymentować do końca ?