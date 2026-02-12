Data driven development - decyzje o dodawaniu narzędzi, o ich zmianie, o modyfikacji promptów powinny wynikać z rzeczywistych zapytań uzytkownika

Reference free and reference based data sets - co innego znajdzie sie w expected output. 


Jak streamować wiadomości ?
Kiedy powinien nastąpić zapis bloków ?
Czy istnieją reference-based wiadomości w aplikacji chatowej ?
Kiedy zbudować CI dla LLM ?
Jak odpalać eksperymenty na CI i je walidować ?
System tagów dla aplikacji ?

Jak organizować eksperymenty i ewaluacje w kodzie ?




https://www.youtube.com/watch?v=R_HnI9oTv3c


Czy zaimplementowane zadania lub storki dotyczące AI można uznać za zamknięte ?
Skąd w ogóle to pytanie. Buduję wraz z zespołem aplikacją mającą podsystem AI. Jedna ze storek obejmowała prawidłowe wyświetlanie danych na frontendzie, storka w swej wypracowanej formie zawierała również w formie subtasków scenariusze testowe. Scenariusze te nie przechodziły po zakończeniu prac. Problem jednak nie leżał po stronie frontendu, ale po stronie backendu oraz samego asystenta, którego odpowiedź w formacie markdown wyświetlaliśmy. 
Prompt został spisany zgodnie oczekiwaniami, był wokół niego zbudowany dataset potwierdzający hipotezę formatowania, a mimo to w momencie testowania scenariuszy, znaleźliśmy case w którym agent zwracał inny wynik niż oczekiwany i tym samym. I tu ciekawy przypadek, w innych okolicznościach zapewne zaktualizowalibyśmy prompt domkneli scenarusze i zapomnieli o temacie. Tutaj sytuacja była natomiast inna sam prompt powstał tydzień wcześniej, a storka obejmowała wyłącznie improement po stronie frontendu. A sam prompt był w fazie developmentu dotyczącego innego zadania.
Płyną z tego ciekawe rzeczy :
1. Pytanie: kiedy storki obejmujące współdziałanie z AI można uznać za zamknięte ?
2. Zarządzanie samą etykietą liniowo ( production + development) jednego prompta może doprowadzić do blokera w postaci oczekiwania na inną storkę aby jednocześnie podbić aplikację oraz sam prompt.
   Nie mogąc testować przez UI promptów potrzebujemy mechanizmu który pozwoli skutecznie

Czy zatem prompty w ogóle powinny być powiązane z storkami ? czy też powinny stanowić osobne substaski ? Co w sytuacji gdy paru developerów pracuję nad częścią AI ???


Podejścia:
1. Jeden prompt, dwie etykiety development i production, wybór na podstawie środowiska odpowiadającego etykiecie - w takim scenariuszu może nastąpić case z tego co wyżej, mam wersję development i nie chcemy jej jeszcze oznaczać jako produkcyjną 
2. Prompt per środowisko unikamy problemu, łatwo wprowadzać hot fixy, większa złożoność w postaci przenoszenia prompta w aplikacji wersjonującej , tu również możemy mieć label production i in-progress
3. Prompty nie stanowią części storek są osobnym streamem

Innymi słowy rozwój promptów powinien być niezależny od storek.
Wyobraźmy sobie sytuację gdy kilku deweloperów pracuje nad aplikacją AI, wówczas jest są streamy per storka oraz stream z promptami.

jak zatem eksperymentować ?
mam prompt w langfuse oraz dataset
mam hipotezę, która potrzebuje zmiany prompta
tworzę nową wersję albo tworzę nowy prompt i używam go w zastępstwie
odpalam eksperymenty i robię analizę czy hipoteza jest potwierdzona czy nie
wprowadzam LLM as judge aby wraz z rosnącą złożonością obsługiwać to sprawnie

prompt nie jest częścią feature'a — jest infrastrukturą, która feature'y konsumują

Twój szkic jest dobry, doprecyzowałbym go:

1. **Hipoteza** — np. "dodanie few-shot examples poprawi formatowanie tabel w 90% przypadków"
2. **Nowa wersja prompta** w Langfuse (nie nowy prompt — chcesz zachować historię wersji)
3. **Ewaluacja offline** — odpalam dataset, porównuję wyniki nowej wersji vs obecnej `production`. Tu wchodzi LLM-as-judge dla kryteriów, które trudno sprawdzić regexem (np. "czy odpowiedź brzmi naturalnie").
4. **Analiza regresji** — nie tylko "czy nowy case przechodzi", ale "czy stare case'y nie zostały zepsute". To jest krytyczne i łatwo o tym zapomnieć.
5. **Promotion** — jeśli metryki się zgadzają, przesuwam label `production` na nową wersję. To jest niezależne od jakiejkolwiek storki.

