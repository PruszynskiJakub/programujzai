Ta publikacja jest kontynuacją o tym jak zrozumieć ewaluację AI i wykorzystać je w praktyce.

Buduję aplikację konwersacyjnego agenta AI mającego dostęp do pokaźnego zbioru narzędzi.
Ze względu na istniejący już backend w języku Python zdecydowałem się na wykorzystanie kombinacji:
- Langchain - framework do zbudowania agenta oraz jego toolingu
- Langfuse - zarządzenie promptami, eksperymenty, ewaluacja

Langfuse to open-source'owe rozwiązanie do observability i ewaluacji aplikacji AI. Wybrałem je ze względu na możliwość self-hostingu oraz rozsądne ceny w wersji hostowanej. Ten artykuł to zbiór moich osobistych doświadczeń, wyciągniętych wniosków i otwartych pytań, które pojawiały mi się w głowie przed budowaniem pierwszych aplikacji AI.

## Dlaczego w ogóle ewaluacja?

Na pewnym etapie budowania aplikacji z AI będziemy chcieli wyjść poza strefę eksperymentowania, wprowadzania modyfikacji w promptach i narzędziach wyłącznie z pomocą naszej intuicji, będziemy chcieli odzyskać kontrolę.

## Pytania, na które szukałem odpowiedzi

Oto pytania, na które szukałem odpowiedzi — i na które chciałbym znać odpowiedzi zanim zacząłem pracę z Langfuse. Pogrupowałem je tematycznie:

**Proces ewaluacji i analiza**
1. Jak wygląda cały proces ewaluacji w Langfuse?
2. Jak przeprowadzić analizę Open Codes i Axial Codes w Langfuse?

**Datasety i eksperymenty**
3. Jak zacząć budować pierwszy dataset?
4. Jakie dane wejściowe i wyjściowe powinny obejmować elementy datasetów?
5. Jak skutecznie przeprowadzać eksperymenty i co powinny obejmować?
6. Czy przeprowadzając eksperymenty powinniśmy przekazywać produkcyjne narzędzia czy też mocki/stuby?
7. Gdzie w kodzie trzymać eksperymenty?

**Prompty i zarządzanie**
8. Kiedy i dlaczego używać konkretnych typów promptów wspieranych przez Langfuse?
9. Jak skutecznie zarządzać promptami i środowiskami aby eksperymentowanie oraz analiza były przyjazne?

**Integracja Langchain ↔ Langfuse**
10. Dlaczego połączenie narzędzi Langfuse i Langchain nie jest idealne?
11. Dlaczego trace id się nie przypisuje gdy używasz uuid np. wiadomości?

## Terminologia Langfuse

Zderzając się pierwszy raz tymi wszystkimi terminami możemy czuć się przytłoczeni ilością różnych dziwnie brzmiących pojęć i ich powiązań. Wypiszmy je sobie aby uporządkować wiedzę:

- **Score Config** - to definicja metryki i wartości jakie może przyjąć
- **Score** - to po prostu metryka, może być reprezentowana przez wartość liczbową, wartość Prawda/Fałsz lub stanowić kategorię z wartościami w postaci etykiet
- **Annotation Queue** - to kolejka wyselekcjonowanych ręcznie lub automatycznie traces, które wymagają manualnej analizy przez człowieka
- **Dataset** - to zbiór par input + expected output, które stanowią reprezentację danych jakie przyjmuje nasz agent lub jakaś jego składowa
- **Eksperyment** - to proces, rozpoczęty hipotezą, obejmujący weryfikację tej hipotezy na podstawie rzetelnych danych i zakończony decyzją oraz wnioskami dotyczącymi prawdziwości postawionej hipotezy

## Jak to się łączy: hipoteza → weryfikacja

Mając już wspólne zrozumienie możemy przedstawić jak te wszystkie rzeczy łączą się.
Z jednej strony mamy rzeczy, które pozwalają nam postawić hipotezę, z drugiej rzeczy które tą hipotezę pozwalają nam zbadać.

**Stawianie hipotez: Score Config → Score → Annotation Queue**

Aby zastosować podejście Open Codes i Axial Codes, które pozwalają nam nie tylko lepiej zrozumieć błędy zachodzące w aplikacji, ale również określić ich kategorię i skalę, potrzebujemy binarnej metryki (Score), którą potrzebujemy utworzyć poprzez Score Config, aby ta metryka finalnie była dla nas dostępna w Annotation Queue aka Human Annotation.

**Weryfikacja hipotez: Dataset → Eksperyment**

Gdy już postawiliśmy np. hipotezę o tym co stanowi źródło konkretnego błędu, jesteśmy w stanie zbudować zróżnicowany zestaw danych, który kończy się tym błędem, a następnie wprowadzić zmianę np. w naszym promptcie celem weryfikacji wyników.

Hipotezy mogą obejmować niemal wszystko, nie tylko zaobserwowane błędy. Przykładowe inne hipotezy to:
- niewrażliwość aplikacji na prompt injection
- przyznawanie się do niewiedzy gdy agent nie ma dostatecznej wiedzy
- umiejętność wybrania odpowiedniej trajektorii narzędzi gdy zadanie jest skomplikowane i wieloetapowe
- umiejętność zbudowania odpowiedniego zapytania do narzędzia

O samych eksperymentach i ich umiejscowieniu w kodzie, lubię myśleć natomiast poprzez analogie do migracji baz danych i umieszczać je na podobnym poziomie. Sam nie wiem do końca dlaczego,  po prostu koncepcyjnie są one dla mnie czymś bliźniaczym, czymś co stanowi jakiś kluczowy poboczny element całej układanki.

## Problemy integracji Langchain ↔ Langfuse

Mimo, że Langfuse chwali się integracją z Langchain to nadal jest sporo nieścisłości i niedoróbek wg mnie, które powodują, że ten duet nie jest idealny.
To te na które sam natrafiłem:

1. Nieprzyjazne wyświetlanie input/output na liście traces, ze względu na różne formaty. Mianowicie Langchain ma swój specyficzny format inny niż wyrosły samoistnie standard role + content. Na szczęście na szczegółach trace dane są wyświetlane w przyjaznej formie
2. Nieoczywista konfiguracja dla "automatycznego" logowania do Langfuse oparta o instancję CallbackHandlera. Niestety, nie pozwala ona z automatu na zmiany identyfikatora sesji czy użytkownika, tym samym trzeba stosować obejścia w postaci wykorzystania innych metod m.in `propagate_attributes`. Ponadto, nie rozgryzłem jeszcze jak sprawić aby narzędzia prawidłowo wiązało się z prompt z Langfuse gdy korzystamy z LLM na poziomie tooli
3. Konieczność pamiętania o prawidłowej obsłudze placeholderów — Langfuse bazuje na `{{placeholder}}`, Langchain natomiast na `{placeholder}`

## Typy promptów w Langfuse: tekstowe vs chatowe

Jedną z bardziej mylących rzeczy dla mnie w ramach Langfuse jest rozróżnienie pomiędzy prompty tekstowe i prompty chatowe, nie różniące się tak naprawdę z perspektywy dewelopera niczym poza placeholderem na treść konwersacji.
I tu znów pojawia się problem związany z różnymi formatami oraz faktem, że Langfuse nie przyjmuje bardziej złożonych struktur np. z załącznikami.
Wynikiem tego eksperymenty przez UI czy nawet Playground mijają się w moim odczuciu z celem bo:
1. Format wiadomości w naszych traces jest różny od tych które możemy przekazać
2. Testowanie bardziej złożonych danych jest też niewykonywalne

Z tego powodu moje podejście bazuje na używaniu wyłącznie promptów tekstowych oraz robieniu eksperymentów tylko przez SDK. Ma to tą niepodważalną zaletę, że to ja decyduje o tym czy ewaluuje pojedynczy prompt czy całego agenta z narzędziami i co równie istotne dzielę format i metody  z kodem produkcyjnym.

Jak 


