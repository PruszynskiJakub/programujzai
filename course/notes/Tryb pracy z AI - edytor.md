# Tryb pracy z AI - edytor

## Wprowadzenie

Współpracę z agentem AI do generacji kodu rozpoczynamy od trybu edytora. Przez tryb edytora rozumiemy orkiestrowanie modelu, aby wprowadzał zmiany bezpośrednio do pliku.

## Zasilanie kontekstu - klucz do sukcesu

Cały proces rozpoczyna się od prostego, jednak bardzo istotnego kroku: **zasilenia kontekstu**. Należy znaleźć zdrowy balans, co przychodzi głównie z praktyką. [[Poziomy szczegółowości promptu]] może być pomocnym źródłem.

Przy pojawieniu się łatwo dostępnych LLM-ów pojawiła się również ogromna pokusa zasilenia modelu pełnym kodem źródłowym projektu. Wraz z upływem czasu ta próba się nie obroniła. Czy jest to możliwe?

Tak! Istnieją modele posiadające bardzo szerokie okno kontekstowe, jak na przykład Googlowe Gemini. Jednak dlaczego tak świetnie zapowiadający się eksperyment nie wypalił? Potężna ilość kontekstu najzwyczajniej tworzy szum. LLM nie jest skupiony na zadaniu, ale na bardzo ogólnikowych danych, co skutkuje równie ogólnikowymi wynikami.

### Jak robić to efektywnie? 

Dodajemy do kontekstu minimalną ilość plików wymaganych do wykonania zadania. Wyobraź sobie, że sterujesz juniorem - chcesz mu przekazać kontekst, nie za dużo bo się pogubi, ale też nie za mały bo będzie mu brakowało potrzebnych informacji i gdzieś popełni błąd.

> 💡 Jeżeli agent, którego używasz, ma możliwość dodawania plików read-only, korzystaj z tego. Ograniczy to skupienie edycji tylko na konkretnych plikach.

## Budowanie efektywnego promptu

Kolejny krok to zbudowanie konkretnego promptu, którego egzekucja pozwoli nam uzyskać pożądany rezultat.

Prompt powinien być również ograniczony do minimum. Staraj się używać [[Słowa bogate znaczeniowo]]. Jeżeli posiadasz plik, który chcesz edytować, wskaż go, to samo z konkretną metodą. W skrócie: zamiast ręcznie wprowadzać kod, skupiamy się na tym, co chcemy osiągnąć, bez potrzeby podawania konkretnych detali technologicznych.

## Mentalność problem first

Można się zastanowić - gdzie haczyk? Czy to jest złoty środek? Czy już nie muszę znać języka, a każdy z ulicy zastąpi mnie na moim stanowisku?

Otóż nie. Narzędzia pokroju Aider potrafią bardzo przyśpieszyć naszą produktywność, pozwalają skupić się na problemie, niekoniecznie na detalach.

[[Mentalność problem first]] jest kluczowa. To na problemie się skupiamy. Największy boost produktywności zyskamy dopiero, kiedy świetnie go rozumiemy i potrafimy go rozwiązać bez wsparcia LLM. 

Kiedy sami nie jesteśmy w stanie uporać się z problemem albo nie mamy jeszcze pomysłu, pojawi się spora ilość irytacji. Naprowadzanie LLM na rozwiązanie, którego nie jesteśmy pewni, miewa poczucie stania w miejscu. Klasyczne modelowanie iteracyjne daje nam poczucie powolnego poruszania się do przodu, zakończone potężnym refaktorem po uzyskaniu oczekiwanego rezultatu.

## Jakość kodu i rola recenzenta

Na koniec wróćmy do tych detali, na których jak wspomnieliśmy, nie skupiamy się. Czy musi to oznaczać obniżenie jakości naszego kodu? 

Otóż nie. Nasze umiejętności recenzowania kodu, które pozyskaliśmy, powinny być teraz bardzo istotne. LLM ma nam pomóc szybko dostarczyć upragnione rozwiązanie, skupić się na biznesie, a kiedy już je mamy - skupmy się na weryfikacji, poświęćmy niezbędny czas na refaktor.

## 🔑 Kluczowe wnioski

- **Minimalizm kontekstowy** - dodawaj do kontekstu tylko niezbędne pliki
- **Precyzyjne prompty** - używaj bogatych znaczeniowo słów, wskazuj konkretne pliki i metody
- **Problem first** - najpierw zrozum problem, potem wykorzystaj AI do implementacji
- **Mentalność recenzenta** - zawsze weryfikuj i refaktoruj kod wygenerowany przez AI
- **Balans** - znajdź równowagę między szybkością dostarczania a jakością kodu

## Zadanie

1. Wybierz prosty problem programistyczny, który znasz i rozumiesz.
2. Przygotuj minimalny zestaw plików kontekstowych.
3. Sformułuj precyzyjny prompt dla AI, skupiając się na problemie, nie na implementacji.
4. Po wygenerowaniu rozwiązania, przeprowadź dokładny code review.
5. Zastanów się: co możesz poprawić w swoim podejściu do współpracy z AI?

Jak zmienia się Twoje podejście do programowania, gdy pracujesz z AI jako asystentem? Czy zauważasz, że więcej czasu poświęcasz na zrozumienie problemu, a mniej na pisanie kodu?