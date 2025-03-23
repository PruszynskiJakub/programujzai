**Komentarz:** Jeśli znasz już Airtable i Notion, a także składnię Markdown, to w tej lekcji skup się jedynie na sekcji dotyczącej Supabase i dziś całą uwagę poświęć na zapoznanie się z tym narzędziem oraz składnią SQL (tutaj porozmawiaj na ten temat z Alice).

* * *

Lekcja #6 zarysowała to, jak możemy wykorzystywać własne dane na potrzeby personalizacji AI. Wkrótce przekonamy się również o ich roli w automatyzacji oraz poznamy różne techniki pracy. Tymczasem zatrzymamy się na tworzeniu i organizacji treści w taki sposób, aby była ona przystępna zarówno dla nas, jak i naszych robotów.

## Dostępność dla ludzi i maszyn

Jeśli stworzymy teraz dowolny dokument, to jako ludzie raczej swobodnie będziemy mogli z nim pracować. Nie jest to jednak takie oczywiste w przypadku AI i automatyzacji. Pierwszy problem pojawia się już na etapie formatowania. Jak widać na poniższej animacji, tekst skopiowany z Google Doc do ChatGPT jest pozbawiony linków, obrazów, nagłówków czy podkreśleń. Pomimo tego, że główny przekaz zostaje przeniesiony, to tracimy po drodze mnóstwo informacji. Nie mamy także możliwości transformacji zawartości dokumentu (np. tłumaczenia, korekty). Ograniczone zostają także możliwości zadawania pytań.

![[_resources/e2f2bfd2cfa35d850ccd44249523d989_MD5.gif]]

Rozwiązaniem tego problemu, jest zastosowanie wspominanego przeze mnie [formatu Markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax), który co prawda posiada swoje ograniczenia i nie daje nam wszystkich możliwości znanych z popularnych edytorów tekstu. Jest jednak na tyle wystarczający, że sam wykorzystuję go dosłownie w każdym przypadku. Ostatnie lata pokazują również, że nie jest to wyłącznie moja opinia, ponieważ coraz więcej narzędzi, w tym także komunikatorów, domyślnie wspiera tę składnię.

![[_resources/d005cbfb6b454f2f649495f4f3d49b47_MD5.gif]]

Na rynku istnieje wiele edytorów Markdown, natomiast moim zdaniem tylko kilka z nich zasługuje na szczególną uwagę:

*   [Notion](https://www.notion.so/) — co prawda nie oferuje 100% zgodności, ale dowolny dokument możemy wyeksportować do formatu Markdown
    
*   [iA Writer](https://ia.net/writer) — to edytor tekstowy z którego sam korzystam
    
*   [Paper](https://paper.pro/) — edytor który ostatnio odkrywam i bardzo mi się podoba.
    
*   [Focused](https://www.71squared.com/focused) — najbliższa alternatywa dla iA Writer
    

*   [Obsidian](https://obsidian.md/) — świetne narzędzie do organizacji wiedzy
    
*   [Cursor](https://cursor.com/) — jak pokazywałem w poprzednich lekcjach, edytor kodu może okazać się świetnym narzędziem do pracy z plikami markdown.
    

Z perspektywy czasu trudno jest mi sobie wyobrazić pracę z tekstem, bez wsparcia składni Markdown. Tym bardziej, że wielokrotnie pojawia się ona w scenariuszach automatyzacji, gdzie mamy także możliwość łatwiej zamiany jej na składnię HTML. To z kolei pozwala na połączenie z narzędziami do maili, newsletterów, a nawet blogów.

W kontekście AI, fundamentalną przewagą składni Markdown nad innymi formatami treści jest możliwość swobodnej transformacji z pomocą LLM. Mogę więc przekazać cały dokument do GPT-4o i poprosić o wprowadzenie dowolnych zmian, a w odpowiedzi otrzymam rezultat, który mogę **po prostu wkleić do swojego edytora.**

## Otwarte formaty przyjazne LLM

Markdown to nie jedyny format, który zasługuje na naszą uwagę. Przez lata pracowaliśmy z plikami w formatach .doc, .xls czy .pdf, które nadal są bardzo popularne. W dodatku w wielu przypadkach nie będziemy mogli z nich zrezygnować. Na szczęście samo **odczytanie ich zawartości na potrzeby automatyzacji zwykle jest możliwe (choć nie zawsze)**, jednak wprowadzanie jakichkolwiek zmian, staje się już poważnym wyzwaniem. Przykład tego, o czym mówię, widoczny jest poniżej. Udało mi się tutaj poprawnie pobrać treść dokumentu Google Doc, więc mogę przekazać ją jako kontekst do modelu.

![[_resources/0c4ce7ee3a8cdf251b0867184e3130b1_MD5.png]]

Niestety w większości przypadków proces ten będzie nieodwracalny, więc nie będę mógł skorzystać z pomocy automatyzacji i LLM w edycji treści tego dokumentu. W dodatku łatwo też spotkać tutaj różnego rodzaju problemy, występujące także na etapie odczytywania treści pliku.

Zatem jeśli tylko mamy taką możliwość, zawsze powinniśmy dążyć do pracy z plikami zapisanych formatach tekstowych. Mowa tutaj o: **txt, md, json, html czy csv**. Bardzo dobrym pomysłem jest także posługiwanie się bazami danych, np. wspomnianym [Airtable](https://airtable.com/) i [Notion](https://www.notion.so/), ponieważ w ich przypadku także możemy swobodnie odczytywać i modyfikować zapisane w nich informacje.

Zasadniczo niemalże zawsze będzie nam zależało na tym, aby LLM mógł nie tylko uzyskiwać dostęp do danych, ale także był w stanie je modyfikować. Istotnym aspektem jest także nieustanna dostępność do najnowszych treści, a to zwykle zapewnia nam API obecne np. w Airtable.

To wszystko prowadzi nas do prostego wniosku — wszystkie informacje z jakimi mamy styczność, powinny być przechowywane w możliwie jak najprostszej formie, a także być opisane i połączone ze sobą tak, aby można było je łatwo **przeszukiwać**. Oczywiście fundamentem tej całej układanki jest dostępność API oferowana przez wykorzystywane przez nas narzędzia.

## Zasady projektowania treści na potrzeby LLM

Aktualnie LLM budują obraz naszej rzeczywistości wyłącznie poprzez tekst. Momentami wyobrażenie to jest nieprecyzyjne, ale też przede wszystkim niekompletne. Nie posiadają także jakichkolwiek informacji na temat naszego otoczenia oraz aktualnego kontekstu i opierają się wyłącznie o swoją bazową wiedzę oraz treść zawartą w prompcie.

Najlepszym znanym mi przykładem prezentującym problem, jaki mamy przed sobą, jest moje doświadczenie z połączeniem LLM do transkrypcji serwisu [eduweb.pl](http://eduweb.pl/). Potencjalnie jest to świetne źródło informacji, bezpośrednio związane z treścią, którą ogląda użytkownik. Gdy przyjrzymy się bliżej, okaże się, że mamy do czynienia z treścią zrozumiałą dla człowieka (który widzi także wideo), a dość niejasną dla modelu. Otóż w transkrypcie pojawiają się nawiązania do tego, co jest obecnie na ekranie, lub co zostało powiedziane kilka lekcji wcześniej. Nierzadko obecne są także wzmianki na temat treści, których bezpośrednio nie ma w szkoleniu i jednocześnie nie ma ich także w bazowej wiedzy modelu.

![[_resources/7896dc3d75cf7703a13246557f8aa662_MD5.png]]

  
Zatem transkrypcje są rodzajem treści w której z punktu widzenia LLM występuje mnóstwo szumu, który negatywnie wpływa na jakość odpowiedzi. Z drugiej strony, transkrypt zawiera także jakościowe informacje, które mogą zostać wykorzystywane do pomocy użytkownikowi.

Choć duże modele językowe zwykle są w stanie świetnie radzić sobie z nieustrukturyzowanym tekstem oraz odnajdywać w nim wartościowe informacje, to i tak naszym celem będzie zmniejszenie ryzyka wygenerowania błędnych odpowiedzi. A to w bardzo dużym stopniu będzie zależało od jakości dostarczonego kontekstu.

Patrząc na przykład transkrypcji, możemy wskazać kilka ogólnych zasad, którymi warto się kierować podczas budowania bazy wiedzy przydatnej zarówno dla człowieka, jak i sztucznej inteligencji. Nie możemy tutaj także zapomnieć o tym, że nie musimy opierać się wyłącznie na swojej pracy, ale mamy do dyspozycji także możliwości samych modeli. W każdym razie, zasady o których mowa obejmują:

*   **Opisywanie:** metadane to informacje opisujące dokument, umożliwiające jego organizację i odnalezienie. W kontekście LLM metadane mogą także nadać kontekst, informując model o tym, czego dotyczy wybrany dokument lub jego fragment. Zatem przy budowaniu bazy wiedzy, będzie nam zależało nie tylko na zapisaniu głównej treści, ale także na jej nazwaniu, dodaniu kategorii, tagów, powiązań oraz źródła. Całość prezentuje poniższy przykład. Oczywiście jego struktura generowana jest z pomocą automatyzacji i nie piszemy jej ręcznie za każdym razem
    
    ![[_resources/74f8e54a104bb0961a5148c9c3e14246_MD5.png]]
    *   **Oczyszczanie:** jak widać na przykładzie transkryptu, nie wszystkie dane będziemy chcieli przechowywać w całości. Co prawda zachowanie oryginalnej formy może okazać się przydatne, jednak z punktu widzenia modelu, będzie nas interesowało zredukowanie szumu rozumianej jako wszystko to, co będzie zwiększało ryzyko wygenerowania błędnej odpowiedzi czy niepoprawnego wykonania zadania przez LLM. Przykład widoczny poniżej pokazuje, jak z oryginalnej treści zostały wyodrębnione tylko kluczowe informacje.
    

![[_resources/ee6fb2727e338cd3dbdfd0138480602a_MD5.png]]

*   **Streszczenia:** nie zawsze będzie nam zależało na zapisywaniu oryginalnej treści, a jedynie przechowaniu odnośnika do źródła i opisu lub streszczenia, którymi model będzie się posługiwał. Przykładem może być sytuacja w której nie chcemy aby LLM uzyskał dostęp do oryginalnej treści, ale był w stanie ją wskazać. Drugim przykładem może być wygenerowanie streszczeń lub gotowych odpowiedzi na pytania, co pozwala na jednorazowe przetworzenie dużej ilości treści, a potem łatwe posługiwanie się wynikami.
    

![[_resources/2ef307c4392c73bcf0cb14dbe186a98f_MD5.png]]

*   **Dostępność:** praktycznie w każdym przypadku będzie nam zależało na dostępie do aktualnych oraz pełnych informacji. Oznacza to, że zwykle będzie nam zależało na stałym połączeniu ze źródłem danych, formacie łatwym do wykorzystania w kontekście LLM. Nierzadko wymagana będzie także możliwość aktualizowania danych. Należy tutaj pamiętać, że modele takie jak GPT-4 czy Gemini posiadają (dość ograniczone) zdolności opisywania obrazów, a także zamiany audio na tekst (i odwrotnie)
    

Na potrzeby automatyzacji zwykle nie będzie nam zależało na tym, aby LLM posiadał dostęp do ogromnej bazy danych. Znacznie lepiej wypadną małe zestawy informacji, nad którymi będziemy mieć dużą kontrolę, a niekiedy nawet samodzielnie będziemy zarządzać ich zawartością. Przykładowo scenariusz porządkujący nasze zadania, może być powiązany wyłącznie z danymi, które pomogą mu w ich organizacji i opisywaniu, a cała reszta będzie stanowić szum.

## Zasady organizowania treści na potrzeby LLM

Dane muszą być w jakiś sposób przechowywane i tutaj wspominałem już o Notion oraz Airtable, na których zwykle będziemy się skupiać tworząc automatyzacje. Niezależnie od tego, na które z nich się zdecydujemy (lub skorzystamy z alternatyw), to i tak staniemy przed wyzwaniem dotyczącym tematu struktury.

[07 — Databases.mp4](https://assets.circle.so/2rs5q7qnm6vfc1kwu5jibs3uqqzf)

Poniżej mamy przykład bazy danych, która pracuje dla mnie od kilku lat i jej rolą jest przechowywanie informacji na temat przeczytanych przeze mnie książek. Przez kilkanaście miesięcy jej zawartość była automatycznie zamieniana na wpisy, które były dopisywane do mojego harmonogramu publikacji.

![[_resources/dde72bb1a90c9b9f7694bb5c5d69f462_MD5.png]]

Obecnie baza ta stanowi jedno z wielu miejsc, które połączyłem z LLM. Mam więc możliwość zarówno przywołania dowolnego tytułu, jak i porozmawiania na jego temat w oparciu o bazową wiedzę GPT-4, a także moje notatki.

![[_resources/81670a57436177292dc3a38c6c4bdcbb_MD5.png]]

Chociaż projektowanie baz danych to rozległy temat, to na potrzeby większości automatyzacji będziemy potrzebować prostych struktur, opartych o kilka zasad.

Pierwszą z nich jest zakres informacji, który chcemy przechowywać w ramach jednej bazy. Gdy przyjrzymy się bliżej tabeli z książkami, zobaczymy, że znajduje się ona w bazie \"overment\" w której jest także kilkanaście innych tabel przechowujących dane związane z moim kanałem na YouTube i obecnością w sieci. Podobne tabele mam dla projektu Alice, ale także dla Programu Codzienność na Autopilocie.

Decyzja o tym, czy utworzyć nową bazę zależy głównie od tego, **czy potrzebuję móc wygodnie łączyć ze sobą dane**. Z kolei decyzja o tym, czy utworzyć nową tabelę jest uzależniona od tego, czy konkretny wpis powinien móc być edytowany niezależnie oraz **czy może być powiązany z wpisem z innej tabeli**.

![[_resources/57d48f02a006dc6de47e8f532afce2b4_MD5.png]]

Ujmując to inaczej — w bazie danych grupuję możliwie powiązane ze sobą informacje, a tabele pozwalają mi je od siebie odseparować. Z kolei rolą kolumn jest oddzielenie od siebie pojedynczych informacji.

[08 — Design 2.mp4](https://assets.circle.so/m6x8afuxx5c4a7bo3nzcmnpk36cj)

Przykładem obrazującym konieczność podziału mogą być okładki książek. Otóż wspomniałem, że informacje na temat przeczytanych książek były automatycznie zamieniane na wpisy social media. Do postów były dołączane wygenerowane na podstawie szablonu grafiki, na których znajdowała się okładka. Jak widać, znajduje się ona w oddzielnej kolumnie, przez co może być łatwo wykorzystana na potrzeby innych szablonów. Gdybym o tym nie pomyślał i zapisywał wyłącznie wygenerowane grafiki, to automatyczne wykorzystanie okładek nie byłoby możliwe.

![[_resources/ae1c59a69e2a976f2caa75819f323861_MD5.png]]

Ostatnią zasadą, którą należy podążać przy organizacji danych w tabelach, jest utrzymanie spójnych reguł nazewnictwa, oraz w ogóle stosowanie nazw, które łatwo zapamiętamy. Zasadniczo nie ma większego znaczenia to, jakie reguły wybierzemy, natomiast istotne jest to, aby się ich trzymać. Sam aktualnie zarówno bazy danych, tabele jak i kolumny nazywam korzystając z języka angielskiego, małych liter oraz podkreśleń \"\\_\" zamiast spacji. Nic skomplikowanego.

## Podstawy projektowania baz danych na potrzeby automatyzacji

Bazy danych współpracujące z automatyzacjami (a także aplikacjami) zwykle posiadają kilka dodatkowych kolumn, pozwalających na zidentyfikowanie, sortowanie i filtrowanie rekordów. Wartości tych pól w większości przypadków generowane i modyfikowane są automatycznie, więc zwykle nie będą zabierać nam zbyt dużo uwagi, ale będą odgrywały istotną rolę przy projektowaniu scenariuszy.

ID to **unikatowy** identyfikator rekordu (choć zwykle posiadają je także tabele i same bazy) w formie ciągu znaków bądź liczby. W przypadku Airtable, wyglądają one tak: **recL1gBls1ca6ywo7**.

![[_resources/816e9af6415be0483f26f01f5ebacc6a_MD5.png]]

Identyfikatory wykorzystywane są w celu **aktualizacji lub usunięcia rekordu**, oraz w celu **wiązania rekordów znajdujących się w innych tabelach**. Mówiąc wprost, identyfikator pozwala na łatwe **wskazanie** wybranego rekordu, unikając pomylenia ich ze sobą (choć i tak musimy zachować ostrożność, aby przypadkiem nie wskazać innego wpisu).

Poza identyfikatorami mamy jeszcze pola związane z obecnym statusem rekordów. Mogą mieć one formę tzw. \"flagi\" (tak lub nie) lub statusu dzięki którym jesteśmy w stanie automatycznie wybrać wpisy, które wymagają przetworzenia oraz oznaczyć je jako przetworzone, po wykonaniu automatyzacji.

Poniżej mam przykład jednej z moich tabel w której rekordy są filtrowane w zależności od zawartości kolumny \"content\". Jeśli jest pusta — oznacza to, że wpisy oczekują na uzupełnienie. W przypadku Airtable oraz Notion, filtrowane rekordu możemy wyświetlać w oddzielnych widokach, z których także będziemy mogli korzystać na potrzeby automatyzacji.

![[_resources/10716c1d88aa6a5b0b3800b0f0934753_MD5.png]]

Ostatnim elementem, który niemal zawsze powinien pojawiać się w naszych automatyzacjach, to **metadane** takie jak: czas utworzenia rekordu, czas ostatniej modyfikacji, linki kierujące do źródła lub w powiązane miejsce docelowe, oraz wszelkiego rodzaju dane, których możemy potrzebować w ramach automatyzacji.

[09 — Automation DB 2.mp4](https://assets.circle.so/zpmhw8va8lrgexrgq55hddwwjua8)

Jedne z najbardziej użytecznych linków, które możemy dołączać do naszych baz danych, to generowane adresy kierujące dokładnie w miejsce, w które powinniśmy być przekierowani. Przykładowo gdy otrzymuję powiadomienie z automatyzacji o tym, że jakaś akcja została wykonana, to w jego treści znajduje się adres prowadzący mnie tam, gdzie ewentualnie mogę coś zatwierdzić lub wprowadzić poprawki.

Co prawda nie każda aplikacja umożliwia utworzenie takiego linku, natomiast jeśli to robi, to zwykle łatwo możemy zauważyć które elementy adresu odpowiadają identyfikatorom. Następnie musimy sprawdzić jak z pomocą automatyzacji uzyskać do nich dostęp i ostatecznie połączyć ze sobą w odpowiedni sposób.

![[_resources/f83d30a9ae83185e28ef0c00d08998e8_MD5.png]]

Jeśli chodzi o projektowanie struktur baz danych na potrzeby automatyzacji, to w tej chwili mamy wszystko. Natomiast już niebawem będziemy mogli zobaczyć jak połączyć to z robotami.

## Supabase

Supabase to rozwiązanie, które, podobnie jak Cursor, na pierwszy rzut oka wygląda jak narzędzie dla programistów. W praktyce jest dokładnie takie. Jednak nikt nie powiedział, że musimy korzystać ze wszystkich dostępnych funkcjonalności, aby czerpać wartość w kontekście automatyzacji no-code.

Na początek musisz wiedzieć, że Supabase ma u swoich podstaw bazę danych PostgreSQL, jeden z najbardziej popularnych silników bazodanowych na świecie, a zwykle do pracy z informacjami przechowywanymi w takiej bazie potrzebujemy kodu, składni SQL bądź graficznych interfejsów, jednak w tym przypadku swobodny dostęp do danych mamy z poziomu panelu w przeglądarce.

Podobnie jak w Notion i Airtable, tutaj także dane organizujemy w ramach tabel, które składają się z kolumn oraz wierszy. Jest to więc struktura, którą doskonale kojarzysz z programów takich jak Microsoft Excel.

Także po założeniu konta na [supabase.com](https://supabase.com/) wystarczy, że otworzysz nowy projekt, a następnie dodasz nową tabelę.

![[_resources/7e54265d618492a7833643f8954820a3_MD5.png]]

W ramach tabel możesz dodawać kolumny posiadające **nazwę oraz typ**. Nazwa może być dowolna, ale nie powinna zawierać znaków specjalnych oraz spacji. Natomiast spośród typów najbardziej interesować nas będą:

1.  int4 – Liczba całkowita (najczęściej używana do ID i liczb całkowitych).
    
2.  float8 – Liczba zmiennoprzecinkowa (do wartości wymagających precyzji, np. ceny).
    
3.  text – Tekst o zmiennej długości (do opisów, nazw, komentarzy).
    
4.  bool – Wartość logiczna (prawda/fałsz, np. status aktywności).
    
5.  uuid – Unikalny identyfikator (często pojawiający się w automatyzacji).
    
6.  date – Data (do przechowywania dat, np. urodzin czy terminów).
    
7.  timestamp – Data i czas (przydatne do rejestrowania zdarzeń).
    
8.  jsonb – Dane w formacie JSON (do przechowywania dynamicznych struktur danych).
    

  

![[_resources/5b0e1004f5d1cb5b86d813c4eadacc1d_MD5.png]]

Na potrzeby zapoznania się z supabase, utwórz dwie tabele:

*   **authors** z polami **id, name, created\\_at**
    
*   **books** z polami **id, title, author\\_id, created\\_at**
    

Jest to zatem miejsce do przechowywania informacji o książkach oraz autorach. To typowy przykład tabel, które będziemy chcieli ze sobą połączyć, podobnie jak rekordy w Airtable. Tutaj jednak potrzebujemy tzw. **kluczy obcych** (foreign\\_key).

Możemy je dodać klikając przycisk znajdujący się pod sekcją dodawania kolumn. Konkretnie w tabeli **books** dodajemy klucz obcy łączący kolumnę **author\\_id** z tabeli **books** z kolumną **id** z tabeli **authors.**

Inaczej mówiąc — łączymy identyfikatory dwóch tabel.

![[_resources/c7abdbb102848b19860ec5da213e1bdb_MD5.png]]

Poniżej mamy rekord \"**Władca Pierścieni**\" podłączony do autora o identyfikatorze \"author\\_id\", który wskazuje na **J.R.R. Tolkien.** Zatem analogicznie jak w przypadku Airtable czy Notion, nasze wpisy zostały połączone.

![[_resources/8fa2d78ab48742121cfbdb26dfbb45d2_MD5.png]]

Jeśli chodzi o samo odczytywanie rekordów, to jak już wspomniałem, możemy posługiwać się interfejsem graficznym dostępnym w zakładce **Database** bądź skorzystać ze składni SQL. Tutaj twórcy Supabase oferują nawet natywną integrację AI i możemy zwyczajnie rozmawiać ze swoją bazą danych.

**UWAGA:** Składnia SQL pozwala na edytowanie oraz usuwanie wpisów. Warto więc spędzić dosłownie jeden wieczór z AI na rozmowie na temat podstaw SQL.

Zatem poniżej proszę jedynie o wyświetlenie autorów oraz książek pisząc \"get authors & books\" (ale możesz zapisać to pytanie także w języku polskim).

![[_resources/259364d562c9947a149de6893a66dcd0_MD5.png]]

Otrzymuję sugestię zapytania SQL, którą w tym przypadku akceptuję.

![[_resources/0227d71a8af5dc071bb34f69216c725a_MD5.png]]

No i mam rezultat, który mogę wyeksportować lub poprowadzić rozmowę z AI w taki sposób, aby zmodyfikować sposób wyświetlania tych danych.

![[_resources/d39aaaa4cca9a60741508730ac41c031_MD5.png]]

Jeśli chodzi o Supabase, to na ten moment to wszystko, ale jeszcze wrócimy sobie do tego narzędzia w dalszej części Zautomatyzowanych.

## Dynamiczne źródła danych

Dostęp do danych może uwzględniać dynamiczne źródła w przypadku których zwykle będziemy mogli pominąć bazy danych. Może się także zdarzyć, że i tak będziemy chcieli z nich skorzystać, ponieważ pozwoli nam to na wykonanie bardziej złożonych operacji.

W tej chwili nie będziemy się zatrzymywać nad tym tematem zbyt długo i wystarczy nam świadomość obecności kilku sposobów interakcji z dynamicznymi źródłami.

**Akcja:** Czyli najprostsza sytuacja z możliwych polegająca na podłączeniu do źródła i pobraniu z niego informacji. Wymiana danych odbywa się poprzez API, a konkretnie protokół HTTP oraz format JSON o których będziemy mówić w przyszłych lekcjach.

**Harmonogram:** Tutaj pobieranie danych lub podjęcie określonych działań, odbywa się według ustalonego harmonogramu, np. 30 minut w wybranych godzinach.

**Zdarzenie:** No i ostatecznie działania mogą być podejmowane w wyniku wystąpienia jakiegoś zdarzenia. Tutaj zwykle do gry wchodzą tzw. \"webhooki\" czyli adresy URL na które przesyłane są informacje, które może odebrać automatyzacja.

Widzimy więc, że nie wszystkie działania będą wymagały naszego zaangażowania, ale w każdym z nich możemy uwzględnić obecność LLM. Projektując automatyzacje będziemy korzystać z każdego z wymienionych sposobów i nierzadko to od nas będzie zależało to, jakie dane będą przekazywane — no ale teraz posiadamy już wiedzę na temat ich organizacji i zastosowania w promptach, więc wystarczy z niej tylko skorzystać.

## Metody wyszukiwania

Ostatnim wątkiem w temacie organizacji danych, jest ich przeszukiwanie. Na tym etapie musimy posiadać przynajmniej ogólne zrozumienie tego, jak automatyzacje oraz LLM będą mogły docierać do informacji, których w danej chwili potrzebujemy.

Zasadniczo wyszukiwanie może odbywać się na podstawie:

*   słów kluczowych (keyword search)
    
*   wyszukiwania pełnotekstowego (full-text search)
    
*   wyszukiwania z pomocą wyrażeń regularnych (regex search)
    
*   wyszukiwania znaczeniowego (semantic search)
    

Zatem odnalezienie filmu \"Incepcja\" w bazie IMDB mogłoby się odbyć w następujący sposób:

![[_resources/00a065ea93fd011736a3d16c420bced3_MD5.png]]

Zatem wyszukiwanie przez słowa kluczowe polega na precyzyjnym dopasowaniu fraz, a pełnotekstowe na uwzględnieniu wszystkich słów zawartych w zapytaniu. Z kolei wyszukiwanie z pomocą wyrażeń regularnych wymaga złożonego opisania poszukiwanego wzorca (w czym może pomóc nam GPT-4o). No i ostatecznie wyszukiwanie znaczeniowe jest w stanie dopasować słowa, które mogą nawet nie wyglądać na podobne, ale mówią mniej więcej o tym samym.

Podczas wyszukiwania zwykle wskazane jest także zawężenie przeszukiwanego zakresu. Wiemy już, że w tym celu wykorzystujemy kategorie oraz tagi, co było widać na wcześniejszym przykładzie z Airtable.

Bez wchodzenia w dalsze szczegóły już teraz widzimy, ze możliwości technik wyszukiwania są spore, jednak warto zadbać o to, aby możliwie zwiększyć szansę na łatwe dotarcie do potrzebnych danych. Przekłada się to na kilka ogólnych zasad:

*   powinniśmy wiedzieć, gdzie znajduje się to, czego szukamy. Istotny jest więc podział na bazy danych oraz tabele. Nie może on być zbyt ogólny (bo utrudni wyselekcjonowanie wpisów), ani zbyt rozproszony (bo będzie wymagał przeszukania wielu źródeł)
    
*   wpisy powinny posiadać swoje metadane (które mogą być generowane przez GPT-4), ponieważ umożliwia to filtrowanie, a także wykorzystanie na potrzeby kontekstu dla LLM
    
*   jeśli to możliwe, powinniśmy poruszać się w jednym języku, ponieważ w przeciwnym razie możemy mieć trudność z dopasowaniem słów kluczowych. Z drugiej strony pracę z wieloma językami umożliwia nam wyszukiwanie znaczeniowe, z którego także będziemy korzystać (ale nie zawsze jest tak precyzyjne, jak będziemy tego oczekiwać)
    
*   na potrzeby automatyzacji, zwykle będziemy korzystali z prostych reguł wyszukiwania, dzięki którym będziemy wybierać rekordy Airtable czy Notion, które mają zostać przetworzone. Tutaj szczególną rolę będzie odgrywać precyzyjne dopasowanie słów kluczowych i statusów z poszczególnych kolumn
    
*   natomiast na potrzeby LLM konieczne będzie zaangażowanie zaawansowanych technik wyszukiwania, a nasza kontrola nad całym procesem będzie utrudniona. Dlatego dobrą praktyką jest staranne budowanie oraz utrzymanie bazy, wykorzystując całą dotychczasową wiedzę na temat kontekstu stanowiącego część promptu.
    

* * *

## Zadanie praktyczne

Wybierz dowolny temat z Twojej codzienności, w którym istotną rolę odgrywają dane oraz sposób ich przetwarzania. Może to być zarówno budżet domowy, zarządzanie listą zakupów, plan wpisów na media społecznościowe czy zbiór Twoich notatek.

Następnie utwórz bazę Airtable lub Notion, w której zapiszesz swoje dane stosując wiedzę z dzisiejszej lekcji. Pamiętaj, że może to być coś prostego, ale dobrze, aby było dla Ciebie przydatne, ponieważ w późniejszych lekcjach będziemy mogli skorzystać z przygotowanej teraz bazy danych.