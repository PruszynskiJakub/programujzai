---
tags:
  - prompt
  - todo
  - module_2
---

#### Rola
LLM niczym kameleon potrafią doskonale wcielać się w różne role. Rolą może być znana postać (np. Joe Rogan), specjalizacja (np. Senior JavaScript Developer), zachowanie (np. krytyk) czy cokolwiek, o czym model ma wiedzę i może być pomocne do zrealizowania zadania (np. Generator obiektów JSON). **Określenie roli nadaje kontekst** konwersacji, **zmniejszając dwuznaczności słów**. Np. w roli programisty React, model zorientuje się, o co nam chodzi, gdy mówimy "component".
#### Instrukcja
Zawiera opis **sposobu realizacji** powierzonego zadania, określenie zachowań modelu, zestawienie faktów czy ściśle określonych zasad. Bardzo przydatną praktyką jest wykorzystywanie **formatu listy**, co zwiększa czytelność oraz ułatwia wprowadzanie modyfikacji.
#### Kontekst
 Uwzględnia zestaw danych **wykraczających poza bazową wiedzę modelu**, które mogą być dostarczone **ręcznie**, być **wygenerowane przez model** lub **dodane dynamicznie** przez logikę naszej aplikacji.
#### Przykłady
 Ze względu na naturę języka naturalnego, czasem łatwiej jest coś zaprezentować, niż opisać. Tym bardziej że duże modele językowe posiadają zdolność do **wychwytywania wzorców** i subtelnych zmian w dostarczonych przykładach
#### Zapytanie
Przedostatnim elementem promptu jest zapytanie, które model ma przetworzyć. Może to być zestaw danych do transformacji, pytanie, polecenie czy zwykła wiadomość będąca częścią dłuższej rozmowy. Pokazałem już jednak, że **zapytanie może zostać potraktowane przez model jako instrukcja do wykonania**, co w niektórych przypadkach nie jest zgodne z oczekiwaniami. Dlatego należy się na takie wypadki zabezpieczyć, ponieważ może to wpłynąć negatywnie nie tylko na realizacje zadania, ale nawet stanowić wyzwanie z punktu widzenia bezpieczeństwa, o czym powiem więcej za moment
#### Odpowiedź
Ostatnim fragmentem, który musimy brać pod uwagę, jest **odpowiedź modelu** dopełniająca nasz prompt. Według definicji **nie stanowi ona części promptu**, jednak uwzględniam go w strukturze prezentującej prompt, ponieważ jego obecność **uwzględniana jest w "Token Window", czyli limicie tokenów dla pojedynczego zapytania**.

----
W prompt równie istotne jest to co powinien robić, jak i to czego robić nie powinien

---

LOCATION: 
	ACTION DETAILS 

WHERE WHAT HOW
GDZIE CO JAK