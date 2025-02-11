Embedding to proces podobny do tokenizacji, ponieważ także polega na reprezentowaniu słów za pomocą liczb, a konkretnie tablicy liczb, czyli tzw. wektorów. Modele językowe wykorzystują tzw. "word embedding", który umożliwia im "rozumienie" znaczenia słów, co jest wykorzystywane między innymi na etapie generowania odpowiedzi.

Jeżeli weźmiemy teraz trzy słowa: samochód, motocykl oraz laptop, to jako ludzie wiemy, że pierwsze dwa są do siebie zbliżone znaczeniem (opisują pojazd). Embedding dąży do opisania tej zależności za pomocą liczb, co obrazuje poniższy, uproszczony przykład. Jeśli porównasz wartości liczbowe, zauważysz podobieństwo, o którym mówię. W praktyce jednak oddanie znaczenia słów jest znacznie bardziej złożone i ilość wymiarów wektora stworzonego podczas procesu embeddingu zależna jest od użytego modelu.

OpenAI aktualnie oferuje trzy modele:

*   text-embedding-ada-002 = 1536 wymiarów
    
*   text-embedding-3-small = 1536 wymiarów
    
*   text-embedding-3-large = 3072 wymiary
    

UWAGA: nawet jeśli dwa modele mają taką samą liczbę wymiarów, to nie oznacza to, że są ze sobą jakkolwiek kompatybilne.

![[86da53b1c6a2c68daac2aa90789c2390_MD5.jpg]]

  
Drugim rodzajem embeddingu, z którym mamy do czynienia przy okazji LLM, jest tzw. "sentence embedding", który, jak nazwa wskazuje, oddaje znaczenie dłuższych treści. Wówczas uwzględnione jest nie tylko znaczenie słów, ale także kontekst, w którym zostały użyte. Tutaj również podobieństwo wartości wektorów oznacza podobieństwo powiązanych z nimi informacji.

Taki embedding będziemy wykorzystywać podczas pracy z bazami wektorowymi, które mogą nam posłużyć do odnajdywania powiązanych ze sobą danych (np. na potrzeby rekomendacji) czy wręcz przeciwnie — ujawniać odchylenia (np. na potrzeby analizy). Rola baz wektorowych polega więc zarówno na przechowywaniu embeddingów, powiązanych z nimi metadanych umożliwiających identyfikację zapisanych danych, jak i wykonywaniu różnych operacji, takich jak np. Similarity Search, o którym powiem więcej w późniejszych lekcjach.

Sentence-embedding często charakteryzuje także większa liczba wymiarów, a dla modelu text-embedding-ada-002 (z którego będziemy korzystać), mówimy konkretnie o liczbie 1536. Obecnie do dyspozycji mamy także nowszy i większy model **text-embedding-3-large** dla którego liczba wymiarów wynosi 3072.