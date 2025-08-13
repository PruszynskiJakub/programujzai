## Podstawowe komendy
Sprawdź, lub edytuj swoją stałą pamięć w [[Claude Code]]
```
/memory
```

Pusto? Zainicjalizuj pamięć projektową
```
/init
```

## Rodzaje pamięci
W [[Claude Code]] wyróżniamy 4 poziomy pamięci (+ [[Context]] rozmowy)
Od najniższego poziomu:

|      Typ      |                                                               Domyślna lokalizacja pliku                                                                |                            Główny cel                             |
| :-----------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------: |
|    Lokalna    |                                                                    ./CLAUDE.local.md                                                                    |             Personalna pamięć do aktualnego projektu              |
|  Projektowa   |                                                                       ./CLAUDE.md                                                                       | Pamięć projektowa przeznaczona do dzielenia się wewnątrz projektu |
|   Globalna    |                                                                   ~/.claude/CLAUDE.md                                                                   |          Pamięć dzielona pomiędzy wszystkimi projektami           |
| Organizacyjna | macOS: `/Library/Application Support/ClaudeCode/CLAUDE.md`  <br>Linux: `/etc/claude-code/CLAUDE.md`  <br>Windows: `C:\ProgramData\ClaudeCode\CLAUDE.md` |     Pamięć przeznaczona do dzielenia się wewnątrz organizacji     |

Stała pamięć zostaje zaciągana automatycznie przy starcie CC.
Przeznaczona jest do ciągłego iteracyjnego utrzymywania, jest to jeden z **NAJWAŻNIEJSZYCH** czynników, który zapewni nam oczekiwany rezultat na prompt. 

## Jak robić to dobrze

##### Referuj pliki bezpośrednio 
[[Claude Code referencje do plików]]

##### Najszybsze zasilenie pamięci
Rozpocznij prompt od znaku '#' aby dalszą treść dodać do pamięci, lub bezpośrednio edytuj konkretny plik memory

##### Jak najczęściej iteruj po pamięci
Duży procent niezadowalających odpowiedzi to niewystarczający [[Context]].
Chcemy utrzymywać pamięć, aby zredukować ilość powtarzających się błędów i naszych manualnych interwencji.

Któryś raz widzisz, że odpowiedź nie trzyma się konwencji? - Memory 🧠
Rozwiązanie wykorzystuje libki, której Ty nie używasz? - Right to the Memory 🧠
Mimo, że komponent już istniał to został napisany na nowo, zamiast wykorzystać istniejący? - Guess what? Memory 🧠
Ponownie hardcoded stringi / kolory przenosisz ręcznie - 🧠
