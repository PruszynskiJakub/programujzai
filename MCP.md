Tydzień zakończony wiedzą apropo Model Context Protocol oraz YNAB MCP.


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





Czym się różni od Function Calling ?
Function Calling pozwalało agentowi wywoływać funkcję które pobierały dane z zewnątrz.

