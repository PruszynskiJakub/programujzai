---
category: "[[Tips & Tricks]]"
---
### Zasady:
Unikaj przekazywania ścieżek plików bez znaku '@' 
Przekazuj pełne ścieżki z katalogu w którym [[Claude Code]] został uruchomiony.

### Powód:
[[Claude Code]] jako agentowe rozwiązanie sam dobiera narzędzia i ścieżkę do rozwiązywania określonego przez użytkownika zadania.
Chcemy ograniczać ilość zbędnych kroków, zastosowanie wyżej podanych zasad umożliwia zasilenie [[Context]] 'u w znacznie efektywniejszy sposób - redukuje wyszukiwanie plików w katalogach.
