
W świecie pracy z modelami językowymi (LLM) oraz narzędziami wspomagającymi pisanie kodu takimi jak [[Aider]], czy [[Cursor]], niezwykle przydatne okazuje się posiadanie jednego, centralnego pliku konwencji. Plik ten pozwala na zdefiniowanie kluczowych zasad oraz preferencji dotyczących tworzonego oprogramowania. Dzięki temu można:

- Uspójnić styl i architekturę kodu w całym zespole/projekcie.
- Ułatwić pracę modelowi AI, który będzie generować kod zgodnie z ustalonymi regułami.
- Przyspieszyć on-boarding nowych członków zespołu – zamiast tłumaczyć konwencje za każdym razem, wystarczy przekazać jeden plik z zasadami.

W tej sekcji kursu poznamy **jak przygotować** taki plik, **co w nim zawrzeć** i **jak go wykorzystać** razem z narzędziami generatywnymi.

---

## Format pliku konwencji

Najlepszym formatem do przechowywania konwencji jest zazwyczaj **Markdown** (`.md`).  
Dlaczego Markdown?

- Jest czytelny zarówno dla ludzi, jak i dla modeli AI.
- Pozwala na dodawanie przykładów kodu w osobnych blokach z odpowiednim formatowaniem.
- Narzędzia takie jak Aider czy Cursor bez problemu wczytują i analizują takie pliki.

Zaleca się również stosowanie jasnych nagłówków (np. `## Architektura`, `## Narzędzia`, `## Konwencje nazewnicze`), dzięki czemu duże modele językowe łatwiej zrozumieją i przetworzą poszczególne sekcje.

---

## Co warto zawrzeć w pliku konwencji?

1. **Stack technologiczny**
    - Jakiego języka używamy (np. Java 17).
    - Jakie frameworki i biblioteki są preferowane (np. Spring Boot, Hibernate, Lombok itp.).
    - Specyficzne narzędzia (Maven, Gradle, Jenkins/CI).
2. **Konwencje kodowania**
    - Styl formatowania (np. wcięcia, maks. długość linii, itp.).
    - Reguły nazewnictwa (np. klasy w PascalCase, zmienne w camelCase).
    - Preferowane praktyki (np. używanie `final` tam, gdzie to możliwe, unikanie niepotrzebnych komentarzy).
3. **Struktura projektu i zasady architektoniczne**
    - Jak dzielimy pakiety (np. `com.example.projectname.service`, `com.example.projectname.controller`).
    - Jakie wzorce projektowe stosujemy (np. Service/Repository, MVC/MVP, DDD?).
    - Jak organizujemy warstwy aplikacji.
4. **Testowanie**
    - Jakie frameworki testowe (np. JUnit 5, Mockito).
    - Konwencje nazewnicze testów i pakietów testowych (np. `src/test/java/...`).
    - Wskazówki dot. testów integracyjnych, jednostkowych, e2e.
5. **Przykłady kodu**
    - Krótki snippet pokazujący, w jaki sposób tworzymy np. klasę kontrolera w Spring Boot.
    - Używasz jakiejś specyficznej implementacji? Np. niestandardowy http client? Uwzględnij snippet używania go
6. **Konwencje dotyczące wyjątków i logowania**
    - W jaki sposób logujemy (używamy np. SLF4J).
    - Czy tworzymy niestandardowe wyjątki czy używamy istniejących.
7. **Inne ważne informacje**
    - Zasady dotyczące bezpieczeństwa, standardów Clean Code, itp.
    - Zalecenia dla commitów (np. wzór komunikatów, reference do taska).

---

## Przykładowy plik konwencji dla Java

Poniżej przedstawiam przykładową, **bardzo uproszczoną** wersję pliku konwencji w formacie Markdown. Możesz go nazwać np. `CONVENTIONS_JAVA.md`.

````markdown
# Project Conventions (Java)

## 1. Stack Technologiczny
- **JDK**: Java 17
- **Framework**: Spring Boot 3.x
- **Build Tool**: Maven 3.x (preferowany), ale Gradle jest dopuszczalny
- **Testy**: JUnit 5, Mockito
- **Logowanie**: SLF4J (logback jako implementacja)

## 2. Konwencje Kodowania
- **Formatowanie**:
  - Używamy 4 spacji zamiast tabów.
  - Maksymalna długość linii: 120 znaków.
  - Pusta linia między metodami, pusta linia pośród pól klasy dla czytelności.
- **Nazewnictwo**:
  - Klasy: PascalCase (np. `MySuperClass`).
  - Metody i zmienne: camelCase (np. `calculateSum`).
  - Stałe: UPPER_CASE_SNAKE_CASE (np. `MAX_CONNECTIONS`).
- **Komentarze**:
  - Unikamy nadmiarowych komentarzy, kod powinien być sam w sobie czytelny.
  - Javadoc tylko przy publicznych metodach i klasach, jeżeli coś wymaga dodatkowego wyjaśnienia.

## 3. Architektura i Organizacja Kodów
- **Pakiety**:
  - `com.mycompany.myproject.controller` – warstwa kontrolerów (REST).
  - `com.mycompany.myproject.service` – warstwa logiki biznesowej.
  - `com.mycompany.myproject.repository` – warstwa dostępu do danych.
  - `com.mycompany.myproject.model` – encje i modele domenowe.
- **Wzorce**:
  - Stosujemy wzorzec architektoniczny Model-View-Controller (MVC) dla aplikacji webowych.
  - Szybkie zasady Domain-Driven Design, gdzie ma to sens.

## 4. Testowanie
- **JUnit 5**:
  - Testy jednostkowe w pakiecie `com.mycompany.myproject.*.test` lub analogicznym `...test`.
  - Nazwa pliku testowego: `NazwaKlasyTest.java` (np. `MyServiceTest.java`).
- **Mockito**:
  - Używamy do mockowania zależności.
  - Staramy się unikać mockowania wszystkiego i pisać testy możliwie zbliżone do rzeczywistych przypadków użycia.

## 5. Logowanie i Obsługa Błędów
- Używamy `@Slf4j` (z Lombok) lub ręcznie definiowanego loggera `private static final Logger log = LoggerFactory.getLogger(...)`.
- W przypadku błędów logicznych rzucamy jasno zdefiniowane wyjątki (np. `BusinessException`).

## 6. Przykładowy Kod
```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping("/{id}")
    public ResponseEntity<UserDto> getUser(@PathVariable Long id) {
        // Zwraca użytkownika lub błąd w zależności od wyniku
        UserDto user = userService.findById(id);
        if (user == null) {
            log.warn("User not found with id {}", id);
            return ResponseEntity.notFound().build();
        }
        return ResponseEntity.ok(user);
    }
}
````

_Powyższy fragment pokazuje styl, nazewnictwo i wykorzystanie logowania._

## 7. Użycie convention file w aider
Property w pliku [[Aider Config Template]]
```yaml
read: [CONVENTIONS_JAVA.md, innyPlik.md]
```
lub
	Uruchamiając Aider, użyj flagi `--read`, np.:
    
    ```bash
    aider --read CONVENTIONS_JAVA.md Main.java
    ```
    

Dzięki temu Aider będzie proponował rozwiązania kodu w Javie, uwzględniając określone w pliku reguły.

## 8. Uwagi
1. Convetions file nie zastępuje narzędzi formatujących typu linter, tak samo analityczne jak np. SonarQube. Plik konwencyjny powinien być używany równolegle z innymi narzędziami, jego główny celem jest poprawienie jakości generowanego kodu.
2. Zbyt rozbudowany plik może robić szum w kontekście przekazanym do LLM. Jeżeli tego wymaga od Ciebie projekt podziel go na kilka mniejszych plików (np. architecture.md, database.md) 


---

## Zadanie dla Kursanta

1. **Stwórz własny plik konwencji**:
    - Bazując na przykładzie powyżej, zaprojektuj i zapisz w repozytorium plik o nazwie `MY_CONVENTIONS.md` (lub innej, dowolnej).
    - Dodaj do niego krótkie sekcje określające Twoje wytyczne projektowe: formatowanie, nazewnictwo, testy, używane frameworki, itp.
2. **Wykorzystaj go w praktyce**:
    - Skonfiguruj Aidera lub Cursor, aby zawsze wczytywał Twój plik konwencji.
    - Poproś model AI o wygenerowanie fragmentu kodu (np. prostego serwisu w Spring Boot) i sprawdź, czy sugerowany kod faktycznie uwzględnia reguły z Twojego pliku.
3. **Rozbuduj dokument**:
    - W miarę rozwoju projektu dodawaj nowe sekcje (np. obsługa wyjątków, styl dokumentacji API, standard wprowadzania zmian w bazie danych itp.).
    - Pamiętaj o aktualizowaniu pliku tak, aby był spójny z bieżącymi praktykami zespołu.

Dzięki temu zadaniu przekonasz się, jak bardzo przydatne jest jednorodne zdefiniowanie konwencji i reguł w jednym miejscu – zarówno dla ludzi, jak i dla narzędzi opartych o sztuczną inteligencję. Powodzenia!
---
md file , AI follows this tips
stores project structure

Każdy projekt powininen mieć dokument markdown opisujący praktyki, decyzje architektoniczne etc. jako źródło dla LLM

https://www.youtube.com/watch?v=QlUt06XLbJE

https://aider.chat/docs/usage/conventions.html

LLM love file with all the entities in one places