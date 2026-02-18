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
	13. Chcę spytać jakie są nadchodzące transakcję
2. Pośrednie
	1. Utworzenie celu w danej kategorii w reakcji na zaplanowane zdarzenie prowadzące do wydatków np. marzenie wyjazdowe, zbliżające się urodziny widoczne w kalendarzu, 
	2. Agent rozumie, że np moje wyjście na ściankę czy bachatę generuje transakcję więc proaktywnie mi o nich przypomina na podstawie kalendarza lub lokalizacji


Na podstawie scenariuszy możemy następnie utworzyć przykładowe zapytania:
- "Zapłaciłem 230 zł u dentysty kartą mBanku"
- "Dzisiaj: Biedronka 67 zł, obiad w kantynie 22 zł, Allegro paczka 145 zł, ścianka 35 zł"
- "Netflix podniósł cenę z 43 na 60 zł"
- "Przelałem 2000 z mBanku na Revolut"
- "Revolut pokazuje 890 zł, wyrównaj"
- "Groceries mi się skończyło, przerzuć 150 z Dining Out"
- "Wystawiłem fakturę na 8000 zł netto, termin płatności 14 dni"
- "Porównaj moje wydatki na jedzenie miesiąc do miesiąca"
- "Chcę kupić monitor za 2500 — da radę w tym miesiącu? Jeśli nie, przesuń na przyszły"
- _(agent widzi "Ścianka" w kalendarzu i wie że Jakub zawsze płaci 35 zł)_ → "Dziś ścianka — rejestruję 35 zł jak zwykle?"

Warto następnie zidentyfikować płaszczyzny w których nasz zestaw narzędzi może nie domagać:
- Date scope 
	- Agent błędnie zinterpretuje datę transakcji
	- Przykładowe wartości: today, yesterday, next month, on wednesday
- Category Misalignment 
	- Agent błędnie przypisze kategorię
	- Przykładowe sytuacje: 
		- Zajęcia bachaty to hobby czy fitness,
		- Wspinaczka to hobby czy fitness
		- Nurkowanie na wyjezdzie to vacation czy hobby 
		- Kolacja z partnerką to eating out czy goi
		- Co w sytuacji gdy istnieje specyficzna kategoria dla użytkownika
- Accounts Misalignment
	- Agent nie będzie wiedział jakiego konta użyć dla specyficznych sytuacji oczywistych dla użytkownika
	- Przykład:
		- PC zapłaciło mi fakturę XYZ - jest to wpłata na konto biznes czego on może nie wymyśleć by default
- 







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