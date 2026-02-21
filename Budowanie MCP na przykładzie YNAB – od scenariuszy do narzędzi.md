# Budowanie MCP na przykładzie YNAB — od scenariuszy do narzędzi

Spędziłem tydzień zagłębiając się w Model Context Protocol i budując MCP dla YNAB-a. Oto wnioski, które wyniosłem z tego procesu — zarówno o samym protokole, jak i o tym, jak projektować narzędzia dla AI, żeby faktycznie działały.

## Czym jest MCP i po co nam kolejny protokół?

MCP (Model Context Protocol) to otwarty protokół pozwalający aplikacjom AI komunikować się z zewnętrznymi źródłami danych i usługami. W sposób agnostyczny względem konkretnego narzędzia udostępnia kontekst w postaci zasobów, promptów oraz narzędzi. Stanowi de facto niezależny klocek skupiony wokół jednej usługi — samodzielną składową agenta.

Architektura wygląda następująco: **host** to aplikacja zarządzająca klientami, gdzie każdy **klient** jest połączony z dokładnie jednym **serwerem** i odpowiada za utrzymanie tego połączenia. Serwery mogą być lokalne (stdio) lub zdalne (streamable HTTP).

Protokół opiera się na dwóch warstwach — danych i transportu — a pod spodem wykorzystuje **JSON-RPC** (Remote Procedure Call). JSON-RPC pozwala wywołać funkcję w innym programie tak, jakby była lokalna, a komunikacja odbywa się w formacie JSON. Kluczowa cecha: każde żądanie ma `id` pozwalające powiązać je z odpowiedzią. Brak `id` oznacza notyfikację — wiadomość niewymagającą odpowiedzi, przydatną np. do informowania o postępie czy zmianie stanu.

Poza narzędziami, promptami i zasobami MCP wspiera również logowanie, prośby o dodatkowe informacje od użytkownika oraz prośby o odpowiedź z modelu.

### Czym się różni od Function Calling?

Function Calling pozwalało agentowi wywoływać funkcje pobierające dane z zewnątrz, ale bez zmiany głównej logiki agenta. MCP to coś więcej — projektowanie MCP powinno przypominać tworzenie nowej przestrzeni możliwości w aplikacji, a nie być naiwną nakładką na API.

I właśnie o tym jest reszta tego artykułu.

## Od czego zacząć świadome budowanie MCP?

MCP (jak i inne narzędzia dla AI) powinno się projektować wychodząc od hipotez i scenariuszy użytkownika. Scenariusze powinny obejmować zarówno przypadki bezpośrednie, jak i pośrednie.

Bezpośredni scenariusz to np. „chcę zarejestrować transakcję". Pośredni to np. agent, który zapamiętując nasze marzenie wyjazdowe, sam proponuje utworzenie celu oszczędnościowego w budżecie.

Generalnie warto wychodzić od podejścia agnostycznego względem API. Innymi słowy: najpierw *co i jak chcemy zrobić*, a dopiero potem — *co za pomocą konkretnego API zrobić możemy*.

## Scenariusze dla budżetu domowego

### Bezpośrednie

1. Chcę zarejestrować transakcję wykonaną przed chwilą.
2. Chcę zarejestrować kilka transakcji, które dziś poczyniłem — na koniec dnia.
3. Chcę zarejestrować cykliczną transakcję (np. wykupiłem subskrypcję HBO Max).
4. Chcę zarejestrować przelew pomiędzy kontami.
5. Chcę wyrównać stan konta z realnym saldem.
6. Chcę przenieść pieniądze między kategoriami.
7. Chcę zarejestrować wydatek na podstawie faktury z poczty e-mail.
8. Chcę wystawić fakturę, która zostanie zaplanowana jako przychód na datę płatności.
9. Chcę podsumowanie wszystkich wydatków w danej kategorii.
10. Przy dodawaniu transakcji w danej kategorii chcę wiedzieć, czy robię overspent, czy ile mi jeszcze zostało.
11. Chcę spytać AI, czy stać mnie na wydatek X w tym miesiącu — a jeśli nie, przesunąć go na kolejny miesiąc.
12. Chcę, aby AI ostrzegł mnie, gdy widzi trend nadmiernego wydawania.
13. Chcę sprawdzić, jakie są nadchodzące zaplanowane transakcje.

### Pośrednie

1. Utworzenie celu oszczędnościowego w reakcji na zaplanowane zdarzenie prowadzące do wydatków — np. marzenie wyjazdowe, zbliżające się urodziny widoczne w kalendarzu.
2. Agent rozumie, że np. wyjście na ściankę czy bachatę generuje transakcję, więc proaktywnie o niej przypomina na podstawie kalendarza lub lokalizacji.

## Od scenariuszy do przykładowych zapytań

Na podstawie scenariuszy tworzymy realistyczne zapytania — takie, jakie użytkownik faktycznie napisałby w czacie:

- *„Zapłaciłem 230 zł u dentysty kartą mBanku"*
- *„Dzisiaj: Biedronka 67 zł, obiad w kantynie 22 zł, Allegro paczka 145 zł, ścianka 35 zł"*
- *„Netflix podniósł cenę z 43 na 60 zł"*
- *„Przelałem 2000 z mBanku na Revolut"*
- *„Revolut pokazuje 890 zł, wyrównaj"*
- *„Groceries mi się skończyło, przerzuć 150 z Dining Out"*
- *„Wystawiłem fakturę na 8000 zł netto, termin płatności 14 dni"*
- *„Porównaj moje wydatki na jedzenie miesiąc do miesiąca"*
- *„Chcę kupić monitor za 2500 — da radę w tym miesiącu? Jeśli nie, przesuń na przyszły"*
- *(agent widzi „Ścianka" w kalendarzu i wie, że Jakub zawsze płaci 35 zł)* → *„Dziś ścianka — rejestruję 35 zł jak zwykle?"*

## Identyfikacja narzędzi

Na podstawie scenariuszy i zapytań identyfikujemy potencjalne narzędzia MCP:

1. **Record transaction** — dodaje jedną lub więcej transakcji (jednorazowych lub cyklicznych).
2. **Move money** — przenosi pieniądze pomiędzy kontami.
3. **Schedule transaction** — planuje przyszłe lub cykliczne transakcje.
4. **Modify transaction** — edytuje istniejącą transakcję.
5. **Modify scheduled transaction** — edytuje zaplanowaną transakcję.
6. **Get accounts** — pobiera listę kont użytkownika.
7. **Get categories** — pobiera kategorie budżetowe.

## Gdzie AI będzie się mylić?

Równie ważne co zaprojektowanie narzędzi jest zidentyfikowanie obszarów, w których AI może popełniać błędy. Oto trzy kluczowe:

### Interpretacja dat

Agent może błędnie zinterpretować datę transakcji. Problematyczne wartości: „dzisiaj", „wczoraj", „w przyszłym miesiącu", „w środę".

### Przypisanie kategorii

Agent może błędnie przypisać kategorię. Przykłady niejednoznacznych sytuacji:

- Zajęcia bachaty — hobby czy fitness?
- Wspinaczka — hobby czy fitness?
- Nurkowanie na wyjeździe — vacation czy hobby?
- Kolacja z partnerką — eating out czy date night?
- A co, gdy użytkownik ma własną, specyficzną kategorię?

### Przypisanie konta

Agent może nie wiedzieć, jakiego konta użyć w sytuacjach oczywistych dla użytkownika. Przykład: „PC zapłaciło mi fakturę XYZ" — to wpłata na konto firmowe, czego agent domyślnie może nie wywnioskować.

Na podstawie tych obszarów generujemy zapytania o zwiększonym prawdopodobieństwie błędnego działania — i testujemy je.

## Naiwne vs świadome podejście — praktyczny przykład

Spójrzmy na [API YNAB](https://api.ynab.com/v1#/). Podstawowym endpointem jest `/transactions`, który między innymi obsługuje przelewy pomiędzy kontami. Przelew realizuje się tak, że jedno konto jest `account`, a drugie — `payee`. Ważny niuans: gdy przenosimy pieniądze pomiędzy kontami czekowymi (checking accounts), kategoria transakcji nie jest wymagana.

### Podejście naiwne

W naiwnym podejściu tworzymy jedno narzędzie `record_transactions`, które odwzorowuje zachowanie API. Problem? Zostawiamy AI sporo miejsca na błędy:

- AI musi samodzielnie odgadnąć, czy kategoria jest wymagana na podstawie typów kont biorących udział w transakcji.
- AI musi prawidłowo określić, które konto jest źródłem, a które odbiorcą — i jak mapują się na `account` vs `payee`.
- AI może wywoływać nadmiarowe narzędzia w różnych kombinacjach: konta → payee → przelew, konta → payee → kategoria → przelew, albo nawet kategoria → konta → payee → przelew (nadmiarowe zapytanie o kategorię, gdy przelew jej nie wymaga).

### Podejście świadome

Alternatywą jest obserwacja tego, jak użytkownik komunikuje swoje potrzeby. Nikt nie mówi: „Zapłaciłem 500 PLN z konta X na rzecz konta Y". Użytkownik raczej powie: „Przelałem 500 z X na Y" albo „Przenieś pieniądze z X na Y".

W naturalny sposób wyłania się stąd osobne narzędzie **`move_money`**.

Co nam to daje? Przestrzeń na uproszczenie sposobu, w jaki AI korzysta z narzędzi. Pozwala też umieścić na końcu odpowiedzi zupełnie inny zestaw wskazówek dotyczących tego, jak ta odpowiedź może być wykorzystana — co przekłada się na skuteczniejszy i przyjaźniejszy UX.

## Nie zapomnij o inicjalizacji

Jeszcze jeden przykład: jeśli naiwnie zaimplementujemy pobieranie kategorii lub kont, ryzyko błędu jest bardzo wysokie. W YNAB-ie kategorie i konta nie mają opisów. Oczywiście możemy nadać deskryptywne nazwy kategoriom i podkategoriom, ale z doświadczenia wiem, że skuteczność takiego podejścia to loteria.

Dużo skuteczniejszym rozwiązaniem jest rozszerzenie MCP o **proces inicjalizacji** — tak aby w ramach MCP utworzyć opisy kategorii i kont wygenerowane wspólnie z użytkownikiem. Dzięki temu agent od pierwszej interakcji wie, że „Ścianka" to fitness, a „PC" to konto firmowe.

---

Projektowanie MCP to nie opakowywanie API w narzędzia. To projektowanie nowej przestrzeni możliwości — z perspektywy użytkownika, nie endpointów.
