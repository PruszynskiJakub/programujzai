prowadzić dziennik pomysłów, rzeczy które mnie spotkały ciekawych tego dnia, przemyslenia na ich temat





Even now thinking keywords matters in slash commands



Traditional programming: DRY (Don’t repeat yourself).
Programming with AI: Prompts should be DRY too. 
I shouldn’t repeatedly enter the same info in prompts. If I’m repeating prompts, I should probably add the context to an instructions file like CLAUDE .md, or create a skill.

----


Ewaluacja to testy zachowania promptów, na podstawie ich inputu i oczekiwanego wyniku

LLM as a Judge generuje score i umozliwia automatyczną ewaluację przeszłych i przyszłych traców przy czym prompt ewaluacyjny możemy ograniczyć do zagnieżdzonych obserwacji

Score Config natomiast to score pod manualny proces adnotacji i potem każda kolejka adnotacji ma podpięte X score configów.

Dataset natomiast pozwalać odpalać testy na promptach z ewalutorem.


To start our error analysis, we assemble a representative dataset of 50-100 traces produced by the example chat app. The quality of your analysis depends on the diversity of this initial data.
1. Simple Good/Bad Output + Comment
2. Failure Modes - identyfikacja i klastrowanie na podstawie komentarzy
3. 

Wybór traces, otagowanie ich jako deployment / test. Na deployment dopracowujemy prompt ewaluatora z wynikiem powyżej 90%, potem odpalamy na test.


zatem inputem będą dokumenty, lub grupa dokumentów wokół konkretnego tematu,  będzie obecna data, będzie sugestia z poprzedniego kroku
outputem będzie natomiast najzwyczajniej odpowiedź LLM-a

LLM as a judge do adnotacji dla datasetów

**True Positive Rate (TPR)** and **True Negative Rate (TNR)**. TPR measures what fraction of actual “Passes” your judge correctly identifies, while TNR measures what fraction of actual “Fails” it correctly identifies.

pojedynczy trace usera powoduje X traców ewaluatora


Innymi słowy chat prompt w langfuse nie przyjmuje contentu w postaci tablicy, czyli już gdy jest załącznik nie ma szans tego skompilować


Trackujemy to co faktycznie wchodzi do prompta i z niego wychodzi, nic więcej nic mniej, ewentualnie jako metadane coś ekstra





kciuki w dół i w góre jako anotacje odpowiedzi od modelu.- user feedback


Black Box (agent output) -> Glass Box (tool calls, correct path) -> White Box (single step eval)


Ewaluacja wokół  elementu w pętli - think albo use albo act
Happy path, multiple turns, error 
Ewaluacja black box wokół całego agenta i tutaj potrzebujemy pełne casy np dodanie wpisu do logbooka, dodanie wielu wpisów do logbooka, zapis + odczyt, odczyt jednego, odczyt wielu

Experymenty dotyczą pojedynczego prompta.

Każdy trace odpowiada pojedynczej interacji użytkownika z systemem a zatem, nie ma sensu najmniejszego wysyłanie całej konwersacji za każdym razem, 
Wejścia i wyjścia dla traca i jego obserwacji to tak naprawdę działanie na kontekscie poprzednich interacji oraz najnowszej wiadomości użytkownika.

Dodatkowo konwersja jako całość obejmuje wyłącznie dane od użytkownika oraz TYLKO odpowiedzi od agenta.


Before building an evaluator, it’s important to differentiate between two types of failures to prioritize your efforts:

**Missing Instructions:** The first type are errors caused by vague or incomplete instructions in your prompt. For instance if your agent uses too many bullet points or doesn’t ask follow-up questions, and you never instructed it to do so, the first step is to fix the prompt. Creating an evaluator for a failure that a simple prompt tweak can solve is often unnecessary effort.

**Model Limitations:** The second type occur when the LLM fails to perform correctly despite receiving clear and precise instructions. These are the ideal candidates for automated evaluation because they represent the model’s inherent limitations, not a misunderstanding of your intent.


Jak zarządzać danymi w dataset podczas gdy dane które przyjmuje prompt się zmieniają ???



Eksperymenty mają pomóc decyzję czy np zmienić model, czy nowa wersja promptu jest lepsza i nie ma regresji.
W razie porównania i niejasnych wyników lub wymagających doprecyzowania może poszczególne wyniki anotować

Score może mieć swój start w anotacji oraz w ewaluacji


![[Attachments/Strona główna/127a4d1a17418c55afa536e0b837f908_MD5.jpeg]]