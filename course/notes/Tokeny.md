---
tags:
  - context
  - todo
---
It's always crucial to have in mind the context limitations to output tokens are between 4-8k.


**Tokenizacja**

Projektowanie modeli językowych wymaga zamiany tekstu na ich reprezentację liczbową. Obecnie najpopularniejszą strategią jest tzw. **subword tokenization**, czyli zapisywanie za pomocą liczb fragmentów słów. Podczas generowania odpowiedzi, model generuje kolejne tokeny (fragmenty słów), odpowiadając na wspomniane wyżej pytanie, które w takiej sytuacji brzmi: "Biorąc pod uwagę dotychczasowy tekst, **jaki token stanowi jego kontynuację?**".

Bardzo wyraźnie możemy to zaobserwować na tej stronie: [platform.openai.com/tokenizer](https://platform.openai.com/tokenizer) lub [https://tiktokenizer.vercel.app](https://tiktokenizer.vercel.app/). Kolejne tokeny zostały tutaj wyróżnione kolorami i wyraźnie widać, że np. słowo "overment" składa się z dwóch tokenów: "over" i "ment", które model zamienia sobie na liczby. Można więc powiedzieć, że np. GPT-4 właśnie tak widzi tekst.

![[7f7a171c846e5b96c60eba80b048e628_MD5.jpg]]

Decyzja o tym, które fragmenty słów stają się tokenami, zależy od algorytmu tokenizacji oraz zestawu danych, na których pracujemy. W ten sposób powstaje słownik (eng. vocabulary), stanowiący element modelu językowego. **Głównym językiem dla modeli GPT jest angielski, dlatego tokeny dobierane są w taki sposób, aby możliwie efektywnie wykorzystywać je podczas generowania treści.** Samo wygenerowanie słownika nie jest jednak wystarczające, ponieważ konieczne jest także uwzględnienie dodatkowych informacji, takich jak chociażby znaczenie słów, które także należy zamienić na zestawy liczb, które w tym przypadku nazywamy embeddingiem.