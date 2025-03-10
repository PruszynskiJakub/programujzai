## Wprowadzenie

Modele językowe (LLM) zrewolucjonizowały sposób, w jaki wchodzimy w interakcję z technologią. Zanim zaczniemy wykorzystywać je w praktyce, warto zrozumieć podstawowe mechanizmy ich działania. Ta lekcja wprowadza kluczowe koncepcje, które pozwolą ci lepiej zrozumieć możliwości i ograniczenia tych narzędzi.

## Jak działają modele językowe?

Modele językowe to zaawansowane systemy sztucznej inteligencji, które przetwarzają i generują tekst w sposób przypominający ludzkie rozumowanie. Ich działanie opiera się na kilku fundamentalnych koncepcjach:

https://www.youtube.com/watch?v=LPZh9BOjkQs

### Tokenizacja

Tokenizacja to proces zamiany tekstu na reprezentację liczbową, którą model może przetwarzać. Innymi słowy tokeny to jednostki, którymi modele "myślą".

- Współczesne modele wykorzystują głównie subword tokenization – dzielenie tekstu na fragmenty słów.
- Każdy token (fragment słowa) jest reprezentowany przez liczbę w słowniku modelu.
- Model generuje odpowiedzi token po tokenie, odpowiadając sobie za każdym razem na pytanie: "Jaki token stanowi najlepszą kontynuację dotychczasowego tekstu?"

Przykłady narzędzi do tokenizacji:

- [platform.openai.com/tokenizer](https://platform.openai.com/tokenizer)
- [tiktokenizer.vercel.app](https://tiktokenizer.vercel.app)

Warto pamiętać, że większość modeli jest zoptymalizowana pod kątem języka angielskiego. Teksty w innych językach mogą wymagać większej liczby tokenów, co zwiększa koszty interakcji z modelem.

**Przykład tokenizacji:**

Zdanie: "Hello, world! 🌍"

Tokeny:
- "Hello"
- ","
- " world"
- "!"
- " 🌍"

Każdy z tych tokenów jest reprezentowany przez liczbę w słowniku modelu. Emoji często są tokenizowane jako osobne tokeny, co zwiększa liczbę tokenów w promptach zawierających dużo symboli graficznych.

#### Dlaczego to ważne?

Tokeny mają praktyczne znaczenie z kilku powodów:
- Limity kontekstu - modele mają ograniczenia ile tokenów mogą przetwarzać (jest to wartość w zakresie 4-8k dla większości modeli)
- Koszty - wiele API modeli językowych pobiera opłaty za liczbę tokenów
- Wydajność - mniejsza liczba tokenów = szybsze przetwarzanie

### Embeddingi

Embedding to reprezentacja znaczenia słów i zdań za pomocą wektorów liczbowych. Dzięki embeddingom modele mogą "rozumieć" semantyczne relacje między słowami i zdaniami.

Wyróżniamy dwa główne rodzaje embeddingów:

- **Word embedding** – reprezentacja znaczenia pojedynczych słów.
  - Słowa o podobnym znaczeniu mają podobne wartości wektorów.
- **Sentence embedding** – reprezentacja znaczenia całych zdań lub fragmentów tekstu.
  - Uwzględnia kontekst użycia słów.
  - Wykorzystywany w bazach wektorowych do wyszukiwania podobnych treści.

Przykładowe modele embeddingów od OpenAI:

- `text-embedding-ada-002` (1536 wymiarów)
- `text-embedding-3-small` (1536 wymiarów)
- `text-embedding-3-large` (3072 wymiary)

**Przykład embeddingów:**

Wyobraź sobie dwa słowa: "pies" i "kot". W przestrzeni embeddingów te słowa będą miały podobne wektory, ponieważ oba odnoszą się do zwierząt domowych. Natomiast słowo "samochód" będzie miało wektor bardziej odległy, ponieważ reprezentuje zupełnie inną kategorię znaczeniową.

### Kontekst

Kontekst to kluczowy element działania modeli językowych, determinujący ich zdolność do generowania spójnych odpowiedzi. Świadome zarządzanie kontekstem jest fundamentem efektywnej pracy z LLM.

#### Tokeny wejściowe vs wyjściowe

Każdy model ma dwa kluczowe ograniczenia kontekstowe:

- **Tokeny wejściowe (input tokens)** – maksymalna liczba tokenów, które możemy przekazać do modelu.
  - Obejmują prompt, historię konwersacji i dodatkowe dane.
  - Limity wynoszą zwykle od 120k do nawet 2M tokenów.
- **Tokeny wyjściowe (output tokens)** – maksymalna liczba tokenów, które model może wygenerować w odpowiedzi.
  - Limity wynoszą zwykle od 4k do 8k tokenów.
  - Przy długich odpowiedziach model może "zapomnieć" wcześniejsze instrukcje.

## Główni dostawcy modeli LLM

Na rynku dostępnych jest kilku znaczących dostawców modeli językowych:

- **OpenAI** – twórca modeli GPT (GPT-3.5, GPT-4)
- **Anthropic** – twórca modeli Claude
- **Google** – twórca modeli Gemini (dawniej Bard)
- **Ollama** – oferujący rozwiązania do lokalnego uruchamiania modeli od Mety

Każdy z dostawców oferuje modele o różnych możliwościach, ograniczeniach i specjalizacjach.

## Zadania praktyczne

### Zadanie 1: Eksperyment z tokenizacją

Przetestuj tokenizację różnych tekstów za pomocą narzędzia [tiktokenizer.vercel.app](https://tiktokenizer.vercel.app):

- Porównaj liczbę tokenów potrzebnych do wyrażenia tego samego zdania w języku angielskim i polskim.
- Sprawdź, jak tokenizowane są terminy techniczne, nazwy własne i emoji.
- Jakie implikacje ma to dla projektowania promptów i zarządzania kontekstem?

### Zadanie 2: Zarządzanie kontekstem

Zaprojektuj strategię zarządzania kontekstem dla następujących scenariuszy:

- Analiza długiego dokumentu (20+ stron) z wykorzystaniem LLM.
- Prowadzenie wieloetapowej konwersacji z modelem, która wymaga "pamiętania" wcześniejszych ustaleń.
- Generowanie długiej, spójnej odpowiedzi przekraczającej standardowy limit tokenów wyjściowych.

### Zadanie 3: Eksperyment z embeddingami

Wykorzystaj narzędzie [Embedding Projector](https://projector.tensorflow.org/) lub podobne, aby:

- Porównać embeddingi różnych słów (np. "pies", "kot", "samochód", "rower").

- Sprawdzić, jak zmieniają się embeddingi w zależności od kontekstu użycia słowa.

- Zastanów się, jak możesz wykorzystać tę wiedzę w praktycznych zastosowaniach (np. wyszukiwanie semantyczne).

## Podsumowanie

Zrozumienie fundamentów działania modeli językowych – tokenizacji, embeddingów i kontekstu – pozwala na bardziej świadome i efektywne wykorzystanie tych narzędzi. Szczególnie istotne jest opanowanie sztuki zarządzania kontekstem, która bezpośrednio wpływa na jakość interakcji z LLM, koszty operacyjne i możliwości zastosowań.

W kolejnych lekcjach będziemy zgłębiać praktyczne aspekty pracy z LLM, opierając się na tych podstawowych koncepcjach.

🚧 **Uwaga:** Technologia LLM rozwija się bardzo dynamicznie. Informacje przedstawione w tej lekcji mogą ulec zmianie wraz z pojawieniem się nowych modeli i rozwiązań.

## Pytania do refleksji:

- Jakie konsekwencje może mieć nieświadome zarządzanie kontekstem w dużych projektach?
- W jaki sposób tokenizacja wpływa na koszty korzystania z modeli językowych?
- Jakie są potencjalne ograniczenia embeddingów w rozumieniu niuansów językowych?