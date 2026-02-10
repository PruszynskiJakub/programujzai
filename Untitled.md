Data driven development - decyzje o dodawaniu narzędzi, o ich zmianie, o modyfikacji promptów powinny wynikać z rzeczywistych zapytań uzytkownika

Reference free and reference based data sets - co innego znajdzie sie w expected output. 


Jak streamować wiadomości ?
Kiedy powinien nastąpić zapis bloków ?
Czy istnieją reference-based wiadomości w aplikacji chatowej ?
Kiedy zbudować CI dla LLM ?
Jak odpalać eksperymenty na CI i je walidować ?
System tagów dla aplikacji ?

Jak organizować eksperymenty i ewaluacje w kodzie ?


Wersjonowanie promptów per środowisko
np max-production, max-development
w takim wypadku możemy niezależnie wersjonować i testować sobie prompty zależnie od środowiska



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