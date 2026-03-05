Budując nowe narzędzie i mając okazję współpracować bliżej z Product Ownerami i Product Managerami jako klientami, miałem wgryźć się głębiej w podstawowe pojęcia i przepływ. Pojęcia te to Proces biznesowy, Flow oraz User Stories. Są to terminy, które każdy zna i używa. Sam niedawna myślałem że sam je świetnie rozumiem, budowanie produktu pokazało mi że się myliłem.
A zatem:

> Proces biznesowy - to ustrukturyzowana, połączona sekwencja aktywności podjętych przez aktora lub aktorów podjętych w celu osiągnięcia celu

Każdy proces możemy wyobrazić sobie jako drzewo, które rozgałęzia się w różnych miejscach, korona tego drzewa reprezentuje natomiast różne stany w których aktor zakończył swoje aktywności próbując osiągnąć cel (jeden ze stanów)

> Flow/Scenariusz - to pojedyncza ścieżka w tym  drzewie przepływu procesu biznesowego

Ale jak to się ma do User Stories/ Epików etc ?

> User Story -  jest schematem opisywania funkcjonalności z perspektywy użytkownika końcowego z definicją kryteriów akceptacyjnych i zachowań obejmujących pełny scenariusz lub jego wycinek.

Mianowicie nigdy wcześniej nie zastanawiałem się głębiej nad transformacją dokumentów czy wymagań od klienta na User Stories.
Jednocześnie ze względu na doświadczenie rozumiałem podskórnie, jak dzielić storki, jak dostarczać w nich wartość etc choć jak nigdy nie miałem pełnego obrazu.

Oba powyższe pojęcia w pełni pozwalają wg mnie połączyć brakujące klocki.

Po pierwsze proces biznesowy wg mnie jest czymś co idealnie przekłada się na Epik. Zarazem proces biznesowy reprezentuje pewien kontekst, który wg mnie nie powinien być wg mnie mieszany w ramach jednej user story.
Dodatkowo procesy biznesowe mają między sobą relację, niektóre elementy budujące proces są potrzebne przez inny np. Dodawanie zdjęć do ulubionych (Proces tworzenia kolekcji_, nie ma sensu jeśli nie wyświetlamy zdjęć (Proces biznesowy zdjęć np. w galerii)
...czyli po dewelopersku "Nie możemy zrobić X bo zależy to od Y".

Po drugie Flow/Scenariusze pozwalają świetnie zrozumieć różne ścieżki aplikacji skupiony wokół konkretnych procesów. Dzięki temu rozmawiając o jakimś przepływie w aplikacji możemy zawężać dyskusje do konkretnych flow w jasno wybranych procesach..bez ciągłego dodawania.. "..i na tym ekranie możemy dodać like, możemy pobrać , możemy, możemy , możemy", NIE, zamiast tego jeżeli rozmawiamy o procesie kolekcji, wówczas skupiamy się wyłącznie na tym jak dodawać, zarządzać kolekcjami i elementami w nich.

I tak z pojedynczych  różnorakich scenariuszy skupionych wokół jednego procesu powstaje jedna lub. wiele user stories zależnie od naszych upodobań w granulacji.

Osobiście preferuje niemal perfidnie prostej user stories na poziomie dodania przycisku na jednym ekranie. Im prostsze tym skuteczniej i prościej możemy opisać, bez miejsca na niedomówienia czy niejasności. Możemy wycenić je skuteczniej, oraz sami deweloperzy mogą mieć szybszą satysfakcję dowiezienia czegoś, choć wiem , że niektórzy z moich kolegów po fachu preferują pełniejsze zadania, które bardziej kompleksowo podchodzą do scenariuszy np. zamiast dodania jednego przycisku na jednym ekranie, dodajemy ten przycisk we wszystkich miejsach gdzie ma on wystąpić.

Przykład:

