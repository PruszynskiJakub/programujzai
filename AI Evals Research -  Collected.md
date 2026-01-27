https://langfuse.com/blog/2025-08-29-error-analysis-to-evaluate-llm-applications
https://langfuse.com/blog/2025-09-05-automated-evaluations
https://langfuse.com/blog/2025-10-21-testing-llm-applications
https://langfuse.com/guides/cookbook/example_synthetic_datasets
https://langfuse.com/blog/2025-11-06-experiment-interpretation
https://hamel.dev/blog/posts/evals-faq/?ck_subscriber_id=3836412167


# Jak rozpocząć ewaluację aplikacji AI, kiedy nie wiesz gdzie zacząć

## Dlaczego ewaluować, kiedy  i czego potrzebujesz

> Ewaluacja - proces ciągłego mierzenia wyników w celu utrzymywania, analizowania i podnoszenia jakości

Ewaluacja w kontekście aplikacji opartych o LLM jest szczególnie kluczowa ze względu na niedeterministyczne zachowanie dużych modeli językowych oraz nie dające się przewidzieć zachowanie użytkownika. 
Innymi słowy chcąc budować aplikację AI w sposób rzetelny oraz ukierunkowany, potrzebujemy podejścia, które połączy jednocześnie praktyki na przecięciu: 
1. programowania - ciągłego testowania, redefiniowania problemu, rozbijania go na mniejsze
2. budowania produktu - zrozumienia użytkownika,  domeny problemu,  jak i stosowania metryk świadczących o kondycji produktu
3. nauk społecznych - metodologii i praktyk dla spraw niepodlegających jasnym definicjom czy standardom
Konieczność balansowania pomiędzy tymi trzeba zestawami umiejętności powoduje, że to zadanie jest niełatwe, wymaga elastyczności oraz zaakceptowanie faktu, że klasyczne binarne podejście do programowania nie ma tu miejsca - tj. nie możemy jednoznacznie i z pełną stanowczością stwierdzić ten asystent czy agenta jest zakończoną funkcjonalnością, możemy jedynie stwierdzić, że w dniu dzisiejszym jest on skuteczny w X procentach.

Co jest konieczne aby wdrożyć proces ewaluacji do swojej aplikacji AI lub zacząć taki proces od zera ?
1. Aplikacja AI - czy w postaci pojedynczego prompta systemowego czy złożonego agenta w systemie ReAct.
2. Platforma typu Langfuse lub jakaś inna forma pozwalająca nam logowanie obserwacji wynikłych podczas działania aplikacji
Mając tylko te dwie rzeczy, możemy rozpocząć proces doskonalenia.

Meta celem ewaluacji jest zrozumienie danych czyli zrozumienie użytkownika oraz funkcjonowania LLM w kontekście aplikacji.

## Cały proces w skrócie

### Dla nowej aplikacji

1. Utwórz pierwszy, wstępny prompt zgodnie z najlepszymi praktykami prompt engineeringu, możliwie dobrym zrozumieniem domeny oraz użytkownika końcowego
2. Wygeneruj zestaw danych syntetycznych opartych na analizie kierunków zapytań, dla których nasza aplikacja ma największe szanse na generowanie nieprawidłowych wyników
	1. składający się z około 50-100 elementów
	2. składający się ze zróżnicowanych, obejmujących możliwie duże spektrum 
   %% Dodać przykład takiego prompta %%
3. Każdy elementu powyższego zestawu przeprocesuj z pomocą aplikacji, w wyniku tego otrzymasz nie tylko zestaw odpowiedzi, ale również zestaw ścieżek (traces)
4. Następnie w sposób manualny przeanalizuj każdy trace (to tak zwana analiza open codes)
	1. Dodaj binarną adnotację Pass/Fail
	2. Dodaj komentarz pierwszej napotkanej nieprawidłowości patrząc od góry,
5. Następnie zbierz wszystkie komentarze i skategoryzuj je (to tak zwana analiza Axial Codes) - w tym momencie określiłeś kierunki w których Twój agent popełnia błędy
### Dla aplikacji istniejącej
1. Wyselkcjonuj zestaw danych produkcyjnych (spośród dostępnych traces) lub wygeneruj zestaw danych syntetycznych. Zestaw ten powinien w sposób możliwie wyczerpujący obejmować różnorodność zapytań użytkownika w aplikacji.
	1. składający się z około 50-100 elementów
	2. składający się ze zróżnicowanych, obejmujących możliwie duże spektrum 
   %% Dodać przykład takiego prompta %%
2. Następnie w sposób manualny przeanalizuj każdy trace (to tak zwana analiza open codes)
	1. Dodaj binarną adnotację Pass/Fail
	2. Dodaj komentarz pierwszej napotkanej nieprawidłowości patrząc od góry,
3. Następnie zbierz wszystkie komentarze i skategoryzuj je (to tak zwana analiza Axial Codes) - w tym momencie określiłeś kierunki w których Twój agent popełnia błędy

## Budowanie datasetu

Dataset jest kluczowy aby rozpocząć jakąkolwiek ewaluacjię. Może być zbudowany z danych produkcyjnych jak i syntentycznych.

## Po prostu spójrz na dane - Open Codes 
Przejrzyj wyselekcjonowane tracy, przeczytaj każdy uważnie i następnie zanotuj pierwszy zaoobserowany błąd czytając od góry

## Określ kierunki błędów - Axial Codes
Sklastruj wszystkie zanotowane błędy z pomocą AI lub samemu

## Kiedy i jak stworzyć automatyczny ewalutor
Gdy już przeszliśmy parę iteracji, rozumiemy błędy i manualna ewaluacja jest zbyt kosztowna wówczas dopiero warto się zastanowić nad tworzeniem automatu.

## Poziomy ewaluacji

Są trzy poziomy ewaluacji BlackBox (na poziomie odpowiedzi agenta) , GlassBox( na poziomie wywołania narzędzia, prawidłowej trajektorii), WhiteBox ( na poziomie pojedynczej obserwacji)



