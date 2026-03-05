Tworzyłem template pod generowanie user stories.

Transformowałem pipeline procesowania wychodząc z założenia, że każdy krok powinien być do review w 10 min, że każdy krok zawiera coś na kształt spisu treści, który pomaga AI jeśli odpowiednio wskazany do szybszego i efektywniejszego działania.

Tworzyłem podagentów.

Zauważyłem, że często robię podagenta ale również jednocześnie command, który go wykorzystuje. Innymi słowy nie chcę być skazany na skuteczność autonomicznego wyboru narzędzi przez AI

Zawsze gdy chcę zrobić "X i Y i Z" wówczas zastnaawiam się jaka jest relacja między nimi czy są to rzeczy niezależne czy też może jedne są konsekwencją innych.
Przykład: Proces i Edge Cases i Ryzyka na podstawie source material.
Pierwotnie wszystko działało się za pomocą jednego prompta.
Po chwili zorientowałem się że Edge Cases i Ryzyka są negative space dla Procesu, a zatem musi on istnieć wcześniej i musi być wysokojakościowy aby pozostałe artefakty miały również szansę takie być.
I tak kolejny krok, czy możemy je utworzyć bardziej efektywnie, czy mamy zależność między nimi . Odpowiedź brzmi NIE, a zatem możemy zrównoleglić ich tworzenie.

Dekompozycja jako kluczowa umiejętność.
Ponad to ważne aby być w stanie dołączyć albo porzucić proces na dowolnym etapie - przykład: 
Jeżeli mam command, który obejmuje wielokrokowy proces, wówczas w momencie zerwania połączenia, obciążenia modelu lub gdy po prostu nie podoba nam się kierunek i chcemy przerwać wówczas warto mieć zestaw narzędzi jak inne polecenia, skill, subagents które mogą ten proces dalej kontynuować w nowej sesji lub być sterowanych manualnie.


idempotency -  prompty powinny to zawierać co się wydarzy w sytuacji gdy ich rezultat już istnieje.


Fajną rzeczą jest również self healing czyli poproszenie AI o przeanalzowanie swoich komend, skill czy subagentów z adnotacją co nieprawidłowego zaobserwowaliśmy wówczas agenta, jest w stanie zidentfikować przyczynę i wprowadzić zmiany w swoim toolsecie. 

Jakie lekcje z tego wyciągnąłem ?

Dlaczeog tak mało rozmawiamy o tym jak istotny jest input a skupiamy się na tym jak efektywnie używać AI. 
Jesteśmy niczym jak silnik z niską efektywnością energetyczną.
Tracimy mnóstwo kontekstu pomiędzy w komunikacji.
Organizację wg mnie są w tyle, nie względu na to, że wdrożenia AI jest trudne tylko dlatego, że procesy które już powinny być zakorzenione wcale takie nie są, a wymaga tego efektywa praca z AI, bo inaczej trochę jedziemy na pierwszym biegu w lambo, wciskając po prostu mocniej pedał gazu.





Agent powinien odpowiadać za orkiestracje nie odpowiadanie.
Dla scenariusza pobierania treści z internetu i odpowiadanie na pytanie, powinnośmy zapisać plik na w pamięci, i mieć osobny tool o nazwie `answer_question` przyjmujący identyfikatory dokumentów.
Innymi słowy wszystko co możliwe wyciągamy z głównej pętli do dedykowanych narzędzi lub metod pomocniczych.





Co jest moim kołem zamachowym w życiu ???