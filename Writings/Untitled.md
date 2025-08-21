---
tags:
  - writings
author:
---
### Backstory
Jakiś czas temu miałem ciekawą dyskusję z przyjacielem z organizacji, był to moment kiedy Claude Code wypuścił nowy gorący feature w postaci hooków. 
Obydwaj jako zapaleńcy tego narzędzia i deweloperzy od razu zakasaliśmy rękawy, żeby sprawdzić o co w tym chodzi. Pomysł był taki aby każdy z nas poeksperymentował w swoim zakresie na podstawie listy przykładów z dokumentacji, a potem spotkamy się na przysłowiową kawkę. Tak też zrobiliśmy. 
Tym samym złapałem się za dokumentację przejrzałem kilka przykładów i stwierdziłem z zapałem, że to właśnie od nich zacznę. 
Oto lista ze strony Anthropic

Example use cases for hooks include:

- **Notifications**: Customize how you get notified when Claude Code is awaiting your input or permission to run something.
- **Automatic formatting**: Run `prettier` on .ts files, `gofmt` on .go files, etc. after every file edit.
- **Logging**: Track and count all executed commands for compliance or debugging.
- **Feedback**: Provide automated feedback when Claude Code produces code that does not follow your codebase conventions.
- **Custom permissions**: Block modifications to production files or sensitive directories.

Zacząłem więc rozpatrywać każdy z tych przypadków z osobna w swoim projekcie - aplikacji mobilnej budowanej wewnątrz zespołu scrumowego. Niestety w moim przypadku po rozpatrzeniu wszystkiego i spojrzeniu na wynik byłem dość rozczarowany.
Z 5 przykładów tylko ostatni okazał się dla mnie przydatny. Spytacie dlaczego, mianowicie:
1. Notyfikacje - zmiana standardowego dźwięku, na komunikat głosowy mimo że jest miłym dodatkiem raczej, nie zwiększy naszej skuteczności a doda niewielkie opóźnienie. 
   Wydaje mi się że ma to sens ale w innych obszarach niż programowanie.
2. Automatyczne formatowanie -mimo przydatności uważam, że zanim skorzystamy z AI zawsze warto się zastanowić czy nie istnieje juz szybsze i bardziej deterministyczne podejście, które nie rozwiązuje nam już tego problemu np autoformatowanie w momencie commitowania. Nie warto odkrywać koła na nowo bo ma kształt liter AI.
3. Logowanie - debugowanie agenta podobnie jak notyfikacje ma wg mnie sens w momencie gdy korzystamy z niego poza programowaniem, w złożonym systemie podejmującym wiele operacji dalece wykraczających poza implementowanie nawet najbardziej złożonej funkcjonalności.
4. Feedback - podobnie, mamy już względem tego arch unity, autoformatowanie, pakietyzację, multimodalność, bazę dobrego kodu który powinniśmy wygenerować w 3-cim etapie z 6 do prawdziwego AI-codingu oraz możliwość umieszczenia wszystkich takich wskazówek w pamięci agenta CLAUDE.md
5. Uprawnienia - tutaj w końcu znalazłem fajne zastosowanie, mogąc odfiltrować plik, które uwazałem za wrażliwe

Byłem jeszcze bardziej pozytywnie zaskoczony jak po spotkaniu i rozmowie z przyjacielem okazało się że podobne obserwacje.
Innymi słowy - zastanów się zawsze czy realnie coś zyskujesz, czy nie możesz osiągnąć podobnych rezultatów za darmo, szybciej i w ramach już istniejących rozwiązań jak IDE, nie podążaj ślepo za hypem i zawsz ale to zawsze szukaj swoich rozwiązań skrojonych do swoich potrzeb.
### Draft

**Nowa funkcja w Claude Code? Sprawdźmy, czy warto.**

Ostatnio Anthropic wypuścił hooks w Claude Code. Kolega przysłał mi linka z entuzjazmem: "Musisz to zobaczyć!". Pomyślałem - kolejna nowość, ale czy rzeczywiście nam pomoże?

**Postanowiliśmy to przetestować.**

Wzięliśmy 5 przykładów z dokumentacji i każdy sprawdził osobno:

🔔 **Notyfikacje** - dodawanie wiadomości głosowych tylko zwiększa delay, zamiast usprawniać pracę
⚙️ **Automatyczne formatowanie** - pre-commit hooks robią to lepiej i szybciej  
📝 **Logging** - OK dla złożonych systemów, ale nie dla zwykłego programowania
💬 **Feedback** - mamy już narzędzia + CLAUDE.md pamięta kontekst
🔒 **Custom permissions** - jedyne, co faktycznie się przydało (filtrowanie wrażliwych plików)

Po eksperymentach zadzwoniliśmy - nasze wnioski były niemal identyczne.

**Wniosek:** 4 z 5 funkcji to było "nice to have", ale bez realnej wartości.

**Szerszy obraz:** W świecie tech łatwo wpaść w pułapkę "shiny object syndrome". Zanim rzucisz się na najnowszą funkcję, zadaj sobie pytanie:
- Czy to rzeczywiście rozwiązuje mój problem? 
- Czy nie mogę tego zrobić szybciej i za darmo istniejącymi narzędziami?
- Czy to dopasowane do moich konkretnych potrzeb?

Czasem najlepsza odpowiedź to po prostu "nie, dziękuję".

A Wy jak podchodzicie do nowych tech features? Testujecie od razu czy czekicie? 👇

#development #tech #productivity #claude #ai

### Final
