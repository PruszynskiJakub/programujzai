
Tokeny to podstawowe jednostki, którymi "myślą" modele językowe. Wyobraź sobie, że model nie widzi tekstu tak jak my - jako ciąg liter i słów - ale jako sekwencję ponumerowanych fragmentów.

## Czym właściwie są tokeny?

Tokeny to fragmenty tekstu, które model językowy przetwarza jako pojedyncze jednostki. Mogą to być:

- Całe słowa

- Części słów

- Pojedyncze znaki

- Znaki interpunkcyjne

Najprościej mówiąc, token to kawałek tekstu, który model traktuje jako niepodzielną całość.

## Jak działa tokenizacja?

Gdy wpisujesz tekst do ChatGPT lub innego LLM, dzieje się coś takiego:

- Twój tekst zostaje "pocięty" na tokeny

- Każdy token zamienia się na liczbę (według słownika modelu)

- Model przetwarza te liczby, nie oryginalny tekst

- Przy generowaniu odpowiedzi, model przewiduje kolejne tokeny jeden po drugim

## Dlaczego to ważne?

Tokeny mają praktyczne znaczenie z kilku powodów:

- Limity kontekstu - modele mają ograniczenia ile tokenów mogą przetwarzać (jest to wartość w zakresie 4-8k dla większości modeli)

- Koszty - wiele API modeli językowych pobiera opłaty za liczbę tokenów

- Wydajność - mniejsza liczba tokenów = szybsze przetwarzanie

## Jak tokeny wyglądają w praktyce?

Weźmy przykład z dokumentu:

Słowo "government" zostaje podzielone na dwa tokeny: "govern" i "ment"

Dlaczego? Ponieważ algorytm tokenizacji uznał, że takie rozbicie jest najbardziej efektywne. Modele  są zoptymalizowane głównie pod język angielski, więc angielskie słowa często tokenizują się bardziej efektywnie niż słowa w innych językach.

## Zadanie

Sprawdź, jak tokenizowane są różne słowa i zdania:

- Odwiedź platform.openai.com/tokenizer lub tiktokenizer.vercel.app

- Wpisz kilka słów w różnych językach

- Porównaj, ile tokenów zajmują podobnej długości słowa w języku angielskim i polskim

- Zastanów się, jakie ma to konsekwencje dla efektywnego wykorzystania kontekstu w prompts

Czy zauważasz, że niektóre języki wymagają więcej tokenów niż inne? Jak myślisz, dlaczego tak jest?