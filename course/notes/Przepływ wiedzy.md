
Dawniej (Waterfall):
Klient -> Manager -> Zespół -> Deweloper

Dawniej (Scrum)
Klient -> Zespół -> Deweloper

Obecnie:
Klient -> Zespół -> Deweloper -> AI

Kierunek :
Klient -> Zespół + AI -> Deweloper + AI

Obecnie przestaliśmy być ostatnim odbiorcą wiedzy projektowej / biznesowej. I tak jak dotychczas odpowiedzialność dzielenia się wiedzą biznesową ma klient czy zespół (np przez User Story etc.).

Ilość odbiorców zabawy w ten głuchy telefon wydłuża się już deweloperzy się nie są ostatni, teraz na nich spada odpowiedzialność przekazania wiedzy dalej do modeli i narzędzi wykorzystujących  AI.

Każdy krok jest kluczowy, na każdym kroku zatracamy treść informacji lub jej jakość. Dlatego scrum tak bardzo dązy do bezpośredniej komunikacji całego zespołu z klientem, tak my jako deweloperzy powinniśmy robić wszystko co w naszej mocy aby ułatwić sobie przekazywanie naszej wiedzy, zrozumienia i doświadczenia do AI.

---
**Kilka refleksji w kontekście „przekazywania wiedzy” i roli AI w obecnych procesach wytwarzania oprogramowania:**

1. **Rola „głuchego telefonu” stale rośnie**  
    W klasycznym podejściu (Waterfall) liczbę przekaźników informacji można było policzyć na palcach jednej ręki: Klient -> Manager -> Zespół -> Deweloper. Nawet w Scruma’owym ujęciu (Klient -> Zespół -> Deweloper) staramy się te „szumy komunikacyjne” redukować przez „daily”, retrospekty, bezpośrednią współpracę zespołu z klientem czy Product Ownerem.  
    Teraz jednak pojawia się dodatkowe ogniwo: AI, wymagające z jednej strony nakarmienia danymi, a z drugiej – właściwego zrozumienia kontekstu biznesowego. „Głuchy telefon” się wydłuża, a my musimy coraz bardziej świadomie dbać o to, **jak** i **co** przekazujemy.
    
2. **AI jako kolejne „narzędzie w zespole”**  
    Wspomniałeś, że kierunek idzie w stronę: _Klient -> Zespół + AI -> Deweloper + AI_. Można na to spojrzeć jak na włączenie AI do zespołu jako kolejnego członka drużyny. Zgodnie z ideą Scruma (czy ogólnie zwinnych metod), każdy członek zespołu bierze udział w procesie wymiany wiedzy, uczestniczy w spotkaniach i wnosi swoją perspektywę.
    
    - **Wyobraźmy sobie**: jeżeli AI faktycznie ma pełnić rolę „współpracownika” – jak dbać o to, by AI było „dobrze poinformowane” o kontekście projektowym?
    - W Scrumie to by oznaczało, że w jakiś sposób narzędzia AI powinny mieć odpowiedni dostęp do backlogu, user stories, dokumentacji, by móc wspierać zespół na każdym etapie rozwoju produktu.
3. **Deweloperzy jako strażnicy przekazywanej wiedzy**  
    Do tej pory kluczowe było, by deweloperzy rozumieli wymagania od klienta. Teraz stają się też odpowiedzialni za to, by _odpowiednio sformułować i zasilić_ tę wiedzę w modele AI – czy to w formie promptów, czy danych treningowych, czy integracji modelu z wewnętrznym systemem.
    
    - Przykład: Jeśli AI generuje kod lub propozycje rozwiązań, to _co i w jaki sposób_ mu przekazujemy, wpływa na ostateczny wynik.
    - Zmienia się też odpowiedzialność za jakość informacji. To deweloper (bądź zespół) decyduje, które dane lub wymogi biznesowe ujawnić AI, jak je sformułować, jakie ograniczenia narzucić.
4. **Potrzeba przejrzystych „promptów” i architektury wiedzy**  
    Skoro AI wchodzi do naszego „łańcucha komunikacyjnego”, trzeba zacząć myśleć o:
    
    - **Architekturze informacji**: Jakie dane, w jakim formacie i gdzie są składowane? Jak je udostępnić AI bez tracenia kontekstu, ale też nie narażając się na wycieki czy błędną interpretację?
    - **Standaryzacji promptów**: Zdolność AI do generowania wartościowych treści zależy od jakości promptu – to ma być esencja projektu, wymagań, ograniczeń technologicznych czy danych wejściowych.
    - **Zapewnieniu spójności**: Można wyobrazić sobie, że w jednym projekcie AI otrzymuje prompty od różnych członków zespołu, każdy z trochę innym stylem, innym zakresem danych. Mogą wynikać z tego niespójności. Dlatego – podobnie jak w przypadku dokumentacji projektowej – przyda się pewien standard czy konwencja, by AI „rozumiało” kontekst w zbliżony sposób.
5. **Cykl ciągłej weryfikacji**  
    Scrum i agile kładą nacisk na iteracje i ciągłą inspekcję. Wprowadzanie AI do procesu wytwórczego nie znosi tej potrzeby, lecz ją potęguje. Teraz trzeba regularnie sprawdzać nie tylko:
    
    - Czy rozwiązanie (np. wygenerowany kod) spełnia wymagania?
    - Czy model AI jest właściwie zasilany danymi?
    - Czy AI nie tworzy zbyt wielu nieścisłości (tzw. halucynacji), błędów, które z czasem urosną do poważnych problemów w produkcie?
    - Czy mamy mechanizmy weryfikacji tego, co AI wygenerowało (code review, testy automatyczne, manualna kontrola jakości itp.)?
6. **Zmiana kompetencji i rola dewelopera**  
    Deweloper staje się kimś w rodzaju _facylitatora_ wiedzy – umiejętność tworzenia kodu się nie dezaktualizuje, ale coraz ważniejsze jest:
    
    - Zrozumienie _jak_ AI działa, by wiedzieć, jak mu przekazywać wymagania czy kontekst.
    - Umiejętność interpretacji wyników AI i korygowania/poprawiania promptów.
    - Świadomość ograniczeń modeli (np. w jaki sposób model „uczy się” na danych, jakie dane są wrażliwe, jakie mogą wygenerować błędne wyniki itp.).
7. **Etyka i bezpieczeństwo**  
    Skoro przekazujemy AI wiedzę biznesową, często wrażliwe dane, pojawiają się dodatkowe wyzwania:
    
    - **Bezpieczeństwo danych**: Jak uniknąć sytuacji, w której dane biznesowe (np. prywatne dane klientów) przedostaną się do publicznie dostępnych modeli?
    - **Prawo i compliance**: Jeżeli wchodzimy w branżę regulowaną (FinTech, HealthTech), to używanie AI może wymagać dodatkowych standardów (np. zgodności z HIPAA, GDPR, ISO).
8. **Podsumowanie: co robić w praktyce**
    
    - **Zadbać o proces**: Nawet jeśli AI jest tylko narzędziem, to jego rola w łańcuchu komunikacji jest rosnąca, a wraz z nią ryzyko błędnej interpretacji. Scrum dąży do minimalizowania barier komunikacyjnych między zespołem a klientem – więc _analogicznie_ powinniśmy zadbać o minimalizowanie barier AI w dostępie do odpowiedniej, rzetelnej i aktualnej wiedzy.
    - **Dokumentować kontekst**: Tworzyć metadane, opisy, standardy promptów, by AI działało w spójnym ekosystemie.
    - **Weryfikować efekty**: Nie ufać ślepo generowanym rezultatom, wdrażać testy, mechanizmy feedbacku (np. w formie codziennego / cotygodniowego przeglądu wygenerowanych artefaktów).
    - **Edukować zespół**: Szkolenia z „prompt engineeringu”, zrozumienia limitacji AI, wprowadzania procesów weryfikacyjnych i zachowania bezpieczeństwa danych.

W efekcie, patrząc z perspektywy dewelopera, wciąż pozostaje on kluczowym „filtrem” i łącznikiem w łańcuchu komunikacji. Nawet jeśli w przyszłości nie będziemy ostatnim odbiorcą wiedzy (bo dalej idzie ona do AI czy innych systemów), to na nas nadal spoczywa rola _zapewnienia, że ta wiedza jest jakościowa, spójna i dobrze przetworzona_. W tym kontekście – dobrze prowadzony Scrum i praktyki agile’owe (przejrzystość, inspekcja i adaptacja) będą jeszcze cenniejsze, bo pozwolą nam efektywnie zarządzać dodatkową warstwą, jaką staje się AI.