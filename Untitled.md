Obserwacje i założenia
1. Rozwiązanie musi być agnostyczne względem używanego narzędzia
2. Musi być łatwe w ręcznej edycji w razie W zatem system plików MD
3. Każdy etap jest zdatny do recenzji nie zajmującej więcej niż 10min
4. Stawiamy świadomość i zrozumienie na pierwszym miejscu

Sources -> Process -> Human Review
Process -> Propozycja Dekompozycji na Flow-> Human Review
Dekompozycja na Flow -> Rozpisanie każdego z Flow -> Human Review
Pojedyncze Flow -> Propozycja Dekompozycji na User Stories -> Human Review
User Story -> Opisanie + Estymacja -> Human Review

Rozwiązanie powinno wspierać taką autonomiczność jakiej szuka uzytkownik.
Suwak nie wajha.

Rozwiązanie musi wspierać indepotencję - prompty powinny to zawierać co się wydarzy w sytuacji gdy ich rezultat już istnieje oraz powinno być możliwe ponowne odpalenie procesu od pewnego dyskretnego miejsca.

Zawsze gdy chcemy zrobić "X i Y i Z" warto rozważyć relacyjnośc wszystkich tych rzeczy. 
Czy one działają sekwencyjnie na swoich wynikach ?
Czy działają niezależnie ? Czy możemy je zrównoleglić ?

Zauważyłem, że często robię podagenta ale również jednocześnie command, który go wykorzystuje. Innymi słowy nie chcę być skazany na skuteczność autonomicznego wyboru narzędzi przez AI.



Czy wszyscy w zespole mogą zmieniać rzeczy ?
Czy wszyscy będą pamiętać i wiedzieć jak działa proces ?





Mamy dwa rodzaje pamięci ustruktoryzowaną i nieustrukturyzowaną.
Pierwsza służy do logiki, filtrowania i api.
Druga jest zoptymalizowana pod reasoning i personalizację.

Ponadto mamy pamięc sesyjną i pamięć globalną