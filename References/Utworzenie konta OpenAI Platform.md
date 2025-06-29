---
category: "[[Manual]]"
tags:
  - references
---
## Krok 1: Rejestracja na stronie OpenAI

1. **Przejdź na stronę [[Open AI]]**: Otwórz przeglądarkę i przejdź do [platform.openai.com](https://platform.openai.com/).
    
2. **Zarejestruj się**: Kliknij przycisk „Zarejestruj się” i podaj swój adres e-mail oraz wybierz hasło. Możesz również zalogować się za pomocą konta Google, Microsoft lub Apple.
    

## Krok 2: Potwierdzenie adresu e-mail

1. **Otrzymaj e-mail**: Po rejestracji otrzymasz e-mail z prośbą o potwierdzenie adresu.
    
2. **Potwierdź adres**: Kliknij link w e-mailu, aby potwierdzić swój adres. Masz na to 5 dni, po czym link wygaśnie.
    
## Krok 3: Uzupełnienie danych

1. **Podaj dane osobowe**: Po potwierdzeniu adresu e-mail, będziesz musiał podać dodatkowe dane, takie jak imię, nazwisko i data urodzenia.
    
2. **Weryfikacja numeru telefonu**: Możliwe, że będziesz musiał potwierdzić numer telefonu za pomocą kodu SMS.

## Krok 4: Generowanie klucza API

1. **Zaloguj się do konta**: Przejdź do swojego konta na platformie OpenAI.
    
2. **Przejdź do ustawień**: Kliknij ikonkę ⚙️ "Settings"
    
3. **Wygeneruj klucz API**: W zakładce „API Keys” w sekcji "Project" kliknij przycisk „Create new secret key” lub „Generate”.

![[_resources/a966c5a140cb93f3454286bdbe38050d_MD5.jpeg]]

4. **Nazwij klucz**: Opcjonalnie możesz nadać nazwę swojemu kluczowi API.
    
5. **Zapisz klucz**: Po wygenerowaniu klucz zostanie wyświetlony. Skopiuj go i przechowuj w bezpiecznym miejscu, ponieważ **nie będziesz mógł go zobaczyć ponownie na stronie OpenAI**.


## Krok 5: Zabezpieczenie klucza API

- **Przechowuj w bezpiecznym miejscu**: Unikaj umieszczania klucza API bezpośrednio w kodzie frontendowym. Rozważ użycie serwera pośredniczącego lub zmiennych środowiskowych.
    
- **Używaj HTTPS**: Zabezpieczaj komunikację między klientem a serwerem za pomocą szyfrowania HTTPS.