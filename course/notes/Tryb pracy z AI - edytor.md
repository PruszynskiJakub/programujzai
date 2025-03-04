Współpracę z agentem AI do generację kodu rozpoczynamy od trybu edytora.

Przez tryb edytora rozumiemy orkiestrowanie modelu aby wprowadzał zmiany bezpośrednio do pliku.

Cały proces rozpoczyna się od prostego jednak bardzo istotnego kroku czyli: zasilenia kontekstu.

Należy znaleźć zdrowy balans i przychodzi to głównie z praktyką. [[Poziomy szczegółowości promptu]] może być pomocnym źródłem. 

Przy pojawieniu się łatwo dostępnym LLM'ów pojawiła się również ogromna pokusa - zasilenia LMM'u pełnym source code'm projektu i praca na nim. Wraz z upływem czasu ta próba się nie obroniła. Czy jest to możliwe?

Tak! Istnieją modele posiadające bardzo szerokie okno kontekstowe, jak dla przykładu Googlowe Gemini. Jednak dlaczego tak świetnie zapowiadający się eksperyment nie wypalił? Potężna ilość kontekstu, robi najzwyczajniej szum. LLM nie jest skupiony na zadaniu, ale na bardzo ogólnikowych danych. Co skutkuje równie ogólnikowymi wynikami modelu.

  

Więc jak robić to efektywnie? Dodajemy do kontekstu minimalną ilość plików wymaganych do wykonania zadania. Wyobraź sobie, że sterujesz juniorem, chcesz mu przekazać kontekst, nie za dużo bo się pogubi, ale też nie za mały bo będzie mu brakowało potrzebnych informacji, więc gdzieś popełni błąd.

Jeżeli agent którego używasz ma możliwość dodawania plików read-only korzystaj z tego, ograniczy on skupienie edycji tylko na konkretnych plikach.

  

---

Kolejny krok edytora to zbudowanie konkretnego promptu, którego egzekucja pozwoli nam uzyskać chciany rezultat.

  

Prompt ograniczony powinien być również do minimum. Staraj się używać [[Słowa bogate znaczeniowo]] , jeżeli posiadasz plik który chcesz edytować wskaż go, to samo z konkretną metodą. Więc w skrócie zamiast ręcznie wprowadzać kod, skupiamy się na tym co chcemy osiągnąć, bez potrzeby podawania konkretnych detali technologicznych

  

---

TODO

Przykład:

- 3 encje - read only

- 1 klasa którą edytujemy

Wygenerowanie kodu w pliku editable

---

  

Można się zastanowić, gdzie haczyk? 
Czy to jest złoty środek? 
Czy już nie muszę znać języku, a każdy z ulicy zastąpi mnie na moim stanowisku?

  

Otóż nie. Narzędzia pokroju Aider potrafią bardzo przyśpieszyć naszą produktywność, pozwala skupić się na problemie, nie koniecznie na detalach.

  

[[Mentalność problem first]]

No właśnie - problem. To na nim się skupiamy. Największy boost produktywności zyskamy dopiero kiedy świetnie go rozumiemy i potrafimy go rozwiązać bez wsparcia LLM. Kiedy sami nie jesteśmy w stanie uporać się z problemem, albo nie mamy jeszcze pomysłu to pojawi się spora ilość irytacji, naprowadzanie LLM na rozwiązanie którego nie jesteśmy pewni miewa poczucie stania w miejscu. Klasyczne modelowanie iteracyjne, daje nam poczucie powolnego poruszania się do przodu, wykończona potężnym refaktorem po uzyskaniu oczekiwanego rezultatu.

  

Na koniec wróćmy do tych detali na których jak wspomnieliśmy nie skupiamy się. Czy musi to oznaczać obniżenie jakości naszego kodu? Otóż nie, nasze skille review które pozyskaliśmy powinny być teraz bardzo istotne. LLM ma nam pomóc szybko dostarczyć upragnione rozwiązanie, skupić się na biznesie, a kiedy już je mamy. Skupmy się na weryfikacji, poświęćmy niezbędny czas na refaktor.