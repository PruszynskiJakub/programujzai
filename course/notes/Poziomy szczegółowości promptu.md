---
tags:
  - prompt
  - todo
---
#### Niskopoziomowy
#### Średniopoziomowy
#### Wysokopoziomowy

Im większy context tym bardziej prompt powinien być szczegółowy
Im mniejszy tym bardziej wysokopoziomowy

Analogicznie dla złożoności zadania

![[29e00cf7b3431407f95d49f41546d29b_MD5.jpeg]]


>Im większe zadanie tym trzeba operować na mniejszym kontekście, z większym i bardziej szczegółowym promptem

>Im mniejsze zadanie tym możemy operować na większym kontekście, z mniejszymi wysokopoziomowym promptem

Balance the scope of the context and changes you wanna do - the sweet spot is a bit far from the point that you would be able make changes on your own having a clear perspective what should be changed 

----
**Analiza poziomów promptów i złożoności zadań**

W praktyce pracy z modelami językowymi można wyróżnić trzy „poziomy” promptów:

1. **Niskopoziomowy (Low-level)**
2. **Średniopoziomowy (Mid-level)**
3. **Wysokopoziomowy (High-level)**

Każdy z tych poziomów służy do innego rodzaju interakcji z modelem i zakłada inny zakres kontekstu, jaki chcemy zawrzeć w promptach. Dobór poziomu zależy zarówno od **złożoności zadania**, jak i od tego, **jak wiele informacji i detali** chcemy kontrolować w odpowiedzi.

---

## 1. Niskopoziomowy (Low-level)

### Charakterystyka

- **Duży poziom szczegółowości** w instrukcjach i ograniczeniach.
- Określasz bardzo precyzyjnie, co ma się znaleźć w wyniku (np. format, struktura, konkretne elementy).
- Kontrolujesz dokładnie sposób pracy modelu.

### Kiedy stosować?

- **Gdy zadanie jest bardzo skomplikowane**, ale wymaga jednocześnie ścisłej kontroli nad wynikiem, np. generowanie kodu z dokładnie określonym stylem czy formatowanie tekstu według ścisłych wytycznych.
- **Gdy nie ma zbyt wielu wątków kontekstowych**, a kluczowe jest wypełnienie restrykcji czy instrukcji krok po kroku.

### Zalety i wady

- **Zaleta**: Precyzyjna kontrola nad odpowiedzią.
- **Wada**: Wymaga większego nakładu przygotowania promptu – musisz sam dostarczyć modelowi szczegółowe instrukcje.

---

## 2. Średniopoziomowy (Mid-level)

### Charakterystyka

- Balans pomiędzy szczegółowością a ogólnością.
- Część wytycznych jest jasna i konkretna, ale zostawiasz modelowi pewien luz interpretacyjny.
- Podajesz kontekst, ale w rozsądnym zakresie – nie przesadzasz ani z detalami, ani z ogólnikami.

### Kiedy stosować?

- **Gdy zadanie jest umiarkowanie złożone**, np. napisanie koncepcji artykułu z kilkoma głównymi punktami, do których musi się odnieść model.
- **Gdy potrzebujesz sterować kierunkiem, ale pozwalasz modelowi współtworzyć szczegóły**.

### Zalety i wady

- **Zaleta**: Utrzymanie równowagi między sterowaniem odpowiedzi a kreatywnością modelu.
- **Wada**: Niekiedy trzeba będzie doprecyzować brakujące informacje w kolejnych iteracjach.

---

## 3. Wysokopoziomowy (High-level)

### Charakterystyka

- Ogólne wytyczne, bardziej zarys koncepcji niż szczegółowy plan.
- Model ma dużą swobodę w sposobie, w jaki wypełni zadanie.
- Kontekst może być dość obszerny (wiele wątków, duże otoczenie informacyjne), bo nie koncentrujesz się na detalach.

### Kiedy stosować?

- **Gdy zadanie jest raczej mniejsze lub mniej restrykcyjne** – np. burza mózgów, tworzenie krótkiego abstraktu, pisanie wstępnej wersji tekstu, w których szczegóły nie są jeszcze kluczowe.
- **Gdy dopiero eksplorujesz temat** i chcesz zobaczyć szersze spojrzenie modelu, bez narzucania mu wielu ograniczeń.

### Zalety i wady

- **Zaleta**: Większa swoboda, więcej inspiracji i kreatywnych rozwiązań.
- **Wada**: Możesz otrzymać zbyt ogólne lub niewystarczająco sprecyzowane wyniki.

---

## Równowaga między zakresem kontekstu a szczegółowością

1. **Im większe zadanie** (bardzo rozbudowany projekt z wieloma krokami czy warstwami), tym **bardziej szczegółowy** i „niskopoziomowy” prompt może być potrzebny – zwłaszcza jeśli chcesz ściśle kontrolować poszczególne elementy wykonania. Ale uwaga: duży, rozbudowany prompt może stać się trudny do utrzymania i zarządzania, jeśli zawiera mnóstwo składowych warunków.
    
2. **Im mniejsze zadanie** (np. krótka analiza, szybka podpowiedź), tym **bardziej zwięzły i „wysokopoziomowy”** może być prompt. Wtedy możesz pozwolić modelowi przetrawić większy kontekst, bo zależy Ci na ogólnych wnioskach i kierunkach, a nie na każdym detalu.
    
3. **„Słodki punkt” (the sweet spot)** znajduje się tam, gdzie:
    
    - Masz **wystarczająco duży kontekst** (by model rozumiał sens zadania).
    - Dostarczasz **tyle szczegółów**, by sterować pracą modelu w odpowiednim kierunku.
    - Sam masz na tyle jasną wizję efektu, że jesteś w stanie **nadać dobry kierunek** i wyłapać nieścisłości podczas generowania odpowiedzi.

Zbyt duży i szczegółowy prompt do prostego zadania może być przerostem formy nad treścią, natomiast zbyt ogólny prompt do trudnego zadania może dać chaotyczne, niespójne wyniki.

---

## Podsumowanie

- **Niskopoziomowy prompt**: wysoki stopień szczegółowości, odpowiedni przy zadaniach wymagających precyzyjnej kontroli (zwłaszcza dużej złożoności technicznej).
- **Średniopoziomowy prompt**: kompromis między kontrolą a swobodą – dobry przy pracach kreatywnych, ale częściowo sformalizowanych.
- **Wysokopoziomowy prompt**: duża swoboda, idealny do eksploracji i szybkiego generowania pomysłów przy mniejszych zadaniach lub w fazie koncepcyjnej.

Równoważenie **poziomu promptu** i **złożoności zadania** to klucz do efektywnej współpracy z modelem. Przy bardziej rozbudowanych projektach istotne jest, byś sam miał przejrzystą wizję końcowego efektu i potrafił umiejętnie wskazać modelowi, jakie obszary są kluczowe do doprecyzowania.