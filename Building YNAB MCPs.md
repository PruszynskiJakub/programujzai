Tydzień zakończony wiedzą apropo Model Context Protocol oraz YNAB MCP.

Od czego zacząć świadome budowanie MCP ?
MCP (jak i inne narzędzia dla AI) powinny rozpoczynać się od hipotez czy też scenariuszy użytkownika. Scenariusze powinny obejmować pośrednie i bezpośrednie przypadki.
Pośredni to gdy np agent zapamiętując nasze marzenie wyjazdowe na ten rok, proponuje utworzenie celu w budżecie.
Generalnie warto wychodzić od agnostycznego wzg API podejścia.
Innymi słowy co i jak chcemy zrobić vs co za pomocą tego zrobić możemy.

Scenariusze dla budżetu domowego:
1. Bezpośrednie
	1. Chcę zarejestrować zarejestrować transakcją wykonaną przed chwilą
	2. Chcę zarejestrować kilka transakcji które dziś poczyniłem na koniec dnia
	3. Chcę zarejestrować cykliczną transakcję, gdy wykupiłem subskrypcję do HBO Max
	4. Chcę zarejestrować przelew pomiędzy kontami
	5. Chcę wyrównać stan konta z realnym stanem
	6. Chcę przenieść pieniądze między kategoriami
	7. Chcę zarejestrować wydatek w oparciu o fakturze na poczcie
	8. Chcę wystawić fakturę która będzie zaplanowana jako przychód dla daty płatności
	9. Chcę podsumowanie wszystkich moich wydatków w danej kategorii
	10. Gdy dodaję transakcję w danej kategorii chcę dowiedzieć się robię overspent lub ile mi zostało
	11. Chcę spytać AI czy stać mnie na wydatek X w tym miesiącu i jeśli nie przesunąć go na kolejny miesiąc jeśli to ważne
	12. Chcę aby AI mnie ostrzegł gdy widzi trend wydawania zbyt dużo
	13. 
2. Pośrednie
	1. Utworzenie celu w danej kategorii w reakcji na zaplanowane zdarzenie prowadzące do wydatków np. marzenie wyjazdowe, zbliżające się urodziny widoczne w kalendarzu, 
	2. Agent rozumie, że np moje wyjście na ściankę czy bachatę generuje transakcję więc proaktywnie mi o nich przypomina na podstawie kalendarza lub lokalizacji
	3. 


Na podstawie scenariuszy możemy następnie utworzyć przykładowe zapytania:








Czym jest MCP, jak działa i do czego służy ? 
Jest to otwarty protokół pozwalający na komunikację aplikacji AI z zewnętrznymi źródłami. 
Pozwalające w sposób agnostyczny względem narzędzia udostępniać kontekst w postaci zasobów, promptów oraz narzędzi.
Stanowi zatem de facto klocek skupiony wokół jednej usługi będący niezależną składową agenta.

Hostem jest aplikacja, która zarządza klientami gdzie każdy klient jest połączony z dokładnie jednym serwerem.
Klient jest odpowiedzialny za utrzymanie połączenia z serwerem.

Są dwa rodzaje serwerów - lokalne (stdio) i zdalne (streamable http).


Są dwie warstwy - daty i transportu.

Czym jest JSON-RPC ? 
RPC to **Remote Procedure Call**
Ideologicznie pozwala na wywołanie funkcji w innym programie jak lokalną funkcję.
JSON bo odpowiedź i prośba są w tym formacie
JSON RPC jest agnostyczny względem formy komunikacji stad jego zaleta.
W JSON RPC mamy id do powiązania odpowiedzi z żądaniem.

Brak id oznacza brak konieczności odpowiedzi niezależnie od kierunku, dając możliwość powiadamiania o postępie lub zmianie/statusie/stanie



Poza toolami, prompta i zasobami wspiera też logowanie, prośbe o dodatkowe informacje od usera, oraz prośbę o odpowiedź z modelu


Czym się różni od Function Calling ?
Function Calling pozwalało agentowi wywoływać funkcję które pobierały dane z zewnątrz bez zmiany głównej logiki agenta.

Projektowanie MCP powinno bardziej przypominać nowy przestrzeń możliwości w naszej aplikacji a nie być naiwną nakładką na API.