## Przydatne Linki
- [Repozytorium GitHub](https://github.com/Aider-AI/aider)
- [Oficjalna Dokumentacja](https://aider.chat/)

## Wprowadzenie
Aider to asystent programowania wspomagany sztuczną inteligencją, który umożliwia programowanie w parach z wykorzystaniem modeli językowych (LLM). Działa jako narzędzie wiersza poleceń, integrujące się bezpośrednio z kodem źródłowym i przepływem pracy Git. Dzięki swojej naturze jako narzędzie CLI, Aider jest kompatybilny ze wszystkimi popularnymi środowiskami programistycznymi, takimi jak IntelliJ, PyCharm, VSCode i inne.

## Główne Funkcje
- 💬 Edycja i generowanie kodu przy użyciu języka naturalnego
- 🔄 Integracja z Git do kontroli wersji
- 📁 Świadomość kontekstu wielu plików
- 🤝 Interaktywne doświadczenie programowania w parach
- ⚡ Wsparcie dla różnych dostawców LLM (OpenAI GPT-4, Claude itd.)
- 🛠️ Rozbudowana konfigurowalność i możliwości dostosowania
- 📖 Projekt open source z aktywną społecznością

## Praca z Aider

### Popularne Komendy
- `/help` - Pokaż dostępne komendy
- `/add <plik>` - Dodaj pliki do sesji czatu
- `/ls` - Lista plików w sesji czatu
- `/drop <plik>` - Usuń pliki z sesji czatu
- `/commit` - Zatwierdź zmiany w git
- `/undo` - Cofnij ostatnią zmianę

### Dobre Praktyki
1. **Jasne Instrukcje**: Bądź precyzyjny w określaniu celów
2. **Stopniowe Zmiany**: Wprowadzaj małe, skoncentrowane modyfikacje
3. **Przegląd Zmian**: Zawsze weryfikuj wygenerowany kod przed zatwierdzeniem
4. **Kontrola Wersji**: Korzystaj z integracji Git dla bezpieczeństwa

## Zaawansowane Funkcje

### Integracja z Git
- Automatyczne tworzenie commitów
- Zarządzanie gałęziami
- Śledzenie zmian

### Edycja Wielu Plików
- Modyfikacje świadome kontekstu w wielu plikach
- Obsługa zależności
- Wsparcie refaktoryzacji

### Konfigurowalność i Open Source
- Możliwość dostosowania ustawień poprzez plik konfiguracyjny
- Wsparcie dla różnych modeli językowych i dostawców API
- Aktywna społeczność na GitHub
- Możliwość własnych rozszerzeń i modyfikacji
- Pełna transparentność kodu źródłowego
- Regularne aktualizacje i ulepszenia od społeczności

Plik konfiguracyjny znajdziesz [[Aider Config Template|tutaj]]

## Wskazówki i Triki
- Użyj komendy `/edit` do precyzyjnej edycji plików
- Wykorzystaj `/diff` do przeglądania zmian przed zatwierdzeniem
- Używaj `/tokens` do monitorowania zużycia tokenów
- Włącz `--dark-mode` dla lepszej widoczności w terminalu
- Użyj komendy `/editor` aby ułatwić sobie pisanie złożonych promptów

