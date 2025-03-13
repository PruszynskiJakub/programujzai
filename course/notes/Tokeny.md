---
tags:
  - context
  - todo
  - module_2
---
It's always crucial to have in mind the context limitations to output tokens are between 4-8k.


**Tokenizacja**

Projektowanie modeli językowych wymaga zamiany tekstu na ich reprezentację liczbową. Obecnie najpopularniejszą strategią jest tzw. **subword tokenization**, czyli zapisywanie za pomocą liczb fragmentów słów. Podczas generowania odpowiedzi, model generuje kolejne tokeny (fragmenty słów), odpowiadając na wspomniane wyżej pytanie, które w takiej sytuacji brzmi: "Biorąc pod uwagę dotychczasowy tekst, **jaki token stanowi jego kontynuację?**".

Bardzo wyraźnie możemy to zaobserwować na tej stronie: [platform.openai.com/tokenizer](https://platform.openai.com/tokenizer) lub [https://tiktokenizer.vercel.app](https://tiktokenizer.vercel.app/). Kolejne tokeny zostały tutaj wyróżnione kolorami i wyraźnie widać, że np. słowo "overment" składa się z dwóch tokenów: "over" i "ment", które model zamienia sobie na liczby. Można więc powiedzieć, że np. GPT-4 właśnie tak widzi tekst.

![[7f7a171c846e5b96c60eba80b048e628_MD5.jpg]]

Decyzja o tym, które fragmenty słów stają się tokenami, zależy od algorytmu tokenizacji oraz zestawu danych, na których pracujemy. W ten sposób powstaje słownik (eng. vocabulary), stanowiący element modelu językowego. **Głównym językiem dla modeli GPT jest angielski, dlatego tokeny dobierane są w taki sposób, aby możliwie efektywnie wykorzystywać je podczas generowania treści.** Samo wygenerowanie słownika nie jest jednak wystarczające, ponieważ konieczne jest także uwzględnienie dodatkowych informacji, takich jak chociażby znaczenie słów, które także należy zamienić na zestawy liczb, które w tym przypadku nazywamy embeddingiem.

-----

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

Dlaczego? Ponieważ algorytm tokenizacji uznał, że takie rozbicie jest najbardziej efektywne. Modele GPT są zoptymalizowane głównie pod język angielski, więc angielskie słowa często tokenizują się bardziej efektywnie niż słowa w innych językach.

## Zadanie

Sprawdź, jak tokenizowane są różne słowa i zdania:

- Odwiedź platform.openai.com/tokenizer lub tiktokenizer.vercel.app

- Wpisz kilka słów w różnych językach

- Porównaj, ile tokenów zajmują podobnej długości słowa w języku angielskim i polskim

- Zastanów się, jakie ma to konsekwencje dla efektywnego wykorzystania kontekstu w prompts

Czy zauważasz, że niektóre języki wymagają więcej tokenów niż inne? Jak myślisz, dlaczego tak jest?