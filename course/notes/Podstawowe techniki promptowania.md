---
tags:
  - prompt
  - todo
---
https://www.promptingguide.ai/

Nie każda wiadomość, którą wysyłamy do AI musi być starannie zaprojektowana i uwzględniać wszystkie omówione sekcje. Gdy prowadzimy bezpośrednią rozmowę z modelem, możemy łatwo poprosić o wprowadzenie ewentualnych poprawek. Inaczej wygląda to w przypadku promptów, które będziemy projektować na potrzeby automatyzacji. Wówczas wysoka precyzja wypowiedzi jest ważna, a czas spędzony na starannym zbudowaniu instrukcji i jej przetestowaniu będzie nam się zwracać przy każdym uruchomieniu scenariusza.

Projektowanie promptów polega więc na precyzyjnym opisaniu tego, na czym nam zależy, unikając przy tym dwuznaczności i zachowując możliwie wysoką zwięzłość. Jest to umiejętność, która w dużym stopniu opiera się o doświadczenie wynikające z obserwowania zachowania modelu w różnych sytuacjach. Możemy także skorzystać z ogólnych technik, z których część mieliśmy okazję już obserwować. Oto najważniejsze z nich:

- Zero-shot: to prosta instrukcja, dążąca do udzielenia odpowiedzi bez sugerowania rozwiązań. Mamy więc tu przestrzeń na dużą dowolność i kreatywność wypowiedzi. Przykładem może być zadanie zwykłego pytania czy prośba o przetłumaczenie tekstu. Model opiera się tutaj wyłącznie o swoje własne zdolności do podążania za instrukcjami
    
- One-shot / Few-shot: to instrukcje zawierające dodatkowe przykłady rozwiązań, których rolą jest zaprezentowanie naszych oczekiwań i umożliwienie modelowi samodzielne wychwycenie schematów pomocnych przy generowaniu odpowiedzi
    
- Zero-shot Chain of Thought: to instrukcja, która zawiera polecenie takie jak "let's think step by step", zachęcające model do wyjaśnienia swojego rozumowania przed udzieleniem odpowiedzi. Jest to niezwykle przydatna technika, szczególnie w przypadku zadań logicznych i pytań nieposiadających oczywistych odpowiedzi
    
- Chain of Thought: to wariant poprzedniej techniki, jednak w przeciwieństwie do niej, proces myślowy nie jest generowany przez model, lecz tworzymy go samodzielnie. Budujemy więc opis dojścia do rozwiązania, a samą odpowiedź pozostawiamy modelowi. Dzięki temu zmniejszamy ryzyko popełnienia błędu na wczesnym etapie, zwiększając tym samym skuteczność działania promptu
    
- Tree of Thoughts: to technika polegająca na przeprowadzeniu rozbudowanego procesu myślowego, składającego się z kilku etapów. Pierwszy polega na zarysowaniu różnych strategii rozwiązania problemu, drugi na ich pogłębieniu, trzeci na ocenie i czwarty na udzieleniu odpowiedzi. Poszczególne etapy mogą się od siebie różnić w zależności od realizowanego zadania, jednak ogólny cel polega na równoległym przejściu przez różne scenariusze i skorzystanie z tego, który został uznany za najlepszy.
    

Praktycznie każda z wymienionych technik dąży do tego, aby jakościowo wzbogacić treść instrukcji oraz zwiększyć szansę na skierowanie uwagi modelu we właściwym kierunku.

Natomiast też w codziennej pracy, nierzadko w ogóle nie będziemy potrzebować konkretnych instrukcji, a jedynie opisu problemu, który chcemy rozwiązać. Problem może być opisany tekstem, obrazem, a w przypadku niektórych modeli także z pomocą nagrania audio bądź wideo.

Z drugiej strony, gdy przyjdzie nam projektować automatyzacje czy nawet proste akcje dla narzędzi takich jak Alice, to tutaj wymienione wyżej techniki tworzenia promptów nadal odgrywają ważną rolę.