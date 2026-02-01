
**1. Wstęp - kontekst**

- Krótkie nawiązanie do poprzedniego artykułu (link)
- Co daje Langfuse vs inne opcje (dlaczego akurat Langfuse?)

**2. Anatomia Langfuse** (szybkie podstawy)

- Trace, Span, Generation, Event - co jest czym
- Jak wygląda dobrze ustrukturyzowany trace

**3. Integracja Langchain ↔ Langfuse** (tu jest unikalna wartość!)

- Co działa out-of-the-box
- **Pułapki:** format placeholderów, słabe wyświetlanie na liście, różnice w strukturze
- Przykłady kodu z obejściami

**4. Workflow ewaluacji w praktyce**

- Score Config (dlaczego binarny > Likert)
- Annotation Queues (z uwagą o limitach Hobby/Core)
- Eksport i analiza

**5. Datasety i eksperymenty**

- Datasety przez UI vs w kodzie
- Prompt experiments vs testowanie całych agentów

**6. Praktyczne wskazówki**

- Jak formatować input żeby ładnie się wyświetlał (JSON z `role` i `content`)
- Tagowanie i filtrowanie traces




Jak tworzyć datasets skutecznie ???
Reference free vs reference based evaluation


----
Rodzaje obserwacji w Langfuse
Prompty chat vs text
Jak testować prompty  a jak testować złożone flow lub agenta ?
Datasety do testowania przez UI i w kodzie
Tworzenie Score Configu
Tworzenie Annotation Queue do ręcznej analizy
	   - *Uwaga:* Langfuse w wersji Hobby pozwala tylko na jedną kolejkę
	   - w wersji Core są to już 3 
Langfuse wyświetla na liście traces ładnie tylko JSON z polami `role` i `content` -

Spinanie Langchain z Langfuse, co działa co nie działa
	 format od Langchain jest słabo wyświetlany, na widoku szczegółów już jest dobrze
	 format dla placeholderów jest różny
	 

### Trace - definicja

### Workflow w Langfuse

![[Attachments/AI Evals Research -  Collected/2e622fd009ba4ce84c771b15fdb1272d_MD5.jpeg]]

1. **Selekcja traces** - dodaj interesujące traces do "Annotation Queue"

2. **Konfiguracja Score Config:**
   - Potrzebujesz binarnego score config Pass-Fail
   - W miarę możliwości stawiaj na metryki binarne - łatwe do interpretacji i mniej subiektywne niż skala Likerta (1-10) czy wartości rzeczywiste (0-1)

![[Attachments/AI Evals Research -  Collected/bc7912a323a09d8d66e0983feb2a8ca5_MD5.jpeg]]

3. **Utwórz Annotation Queue:**
   - Wymagana nazwa (np. "Open Codes") oraz score config


4. **Manualna ewaluacja:**
   - Dla każdego elementu wybierz Pass lub Fail
   - Przy Fail - dodaj komentarz z pierwszą zaobserwowaną nieprawidłowością

5. **Eksport i kategoryzacja:**
   - Eksportuj traces z wynikiem Fail
   - Na podstawie komentarzy zbuduj Axial Codes

### Uwagi praktyczne

- 
- Eksperymenty przez UI to prompt eksperymenty
- Datasety możemy wykorzytywać w kodzie jak i na UI
- Prompty typu chat pozwalają przekazywać historię konwersacji