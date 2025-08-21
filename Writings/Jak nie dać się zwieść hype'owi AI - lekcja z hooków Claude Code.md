---
tags:
  - writings
  - linkedin
author: "[[Jakub Pruszyński]]"
categories:
  - "[[Posts]]"
created: 2025-08-21
published: 2025-08-21
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

🚨 When AI hype meets reality: I tested Claude Code's hooks feature last month and got humbled 

My teammate and I were buzzing about Claude Code's new hooks feature. 5 promising examples from the docs:
• Notifications 🔔
• Auto-formatting ✨  
• Logging 📊
• Code feedback 🔍
• Custom permissions 🔒

We split up, experimented separately, then met for coffee to compare notes.

**The result? Only 1 out of 5 was actually useful.**

❌ Notifications: Cool sound effects don't make me more productive
❌ Auto-formatting: My IDE + git hooks already handle this perfectly
❌ Logging: Makes sense for complex systems, not for coding a single feature  
❌ Code feedback: CLAUDE.md, linting, and code reviews already cover this

✅ Custom permissions: Finally! Something that actually solved a real problem - protecting sensitive files

**The plot twist?** My teammate had identical findings.

Here's what 2 experienced developers learned about AI tooling:

🧠 **Always ask**: "Am I actually gaining something, or just adding complexity?"

⚡ **Check first**: Can existing tools (IDE, git, linting) solve this faster and more reliably?

🎯 **Resist the hype**: Just because it has "AI" doesn't mean it's better than proven solutions

💡 **Tailor to YOUR needs**: Don't follow examples blindly - find what actually moves the needle

The best AI tools don't replace everything - they fill gaps that traditional tools can't.

**Don't get me wrong** - hooks are a phenomenal feature with incredible potential. But for me, at least for now, their real power shines in complex systems rather than typical programming projects. Think multi-service orchestration, compliance workflows, or enterprise-scale operations where you need sophisticated coordination between multiple tools and processes.

What's your experience with AI dev tools? Are you solving real problems or just adding shiny complexity? 

#AI #DeveloperTools #ClaudeCode #ProductivityHacks #SoftwareDevelopment

### Final

🚨 When AI hype meets reality: I tested Claude Code's hooks feature last month and got humbled

My teammate and I were buzzing about Claude Code's hooks feature. 5 promising examples from the docs:
• Notifications 🔔
• Auto-formatting ✨  
• Logging 📊
• Code feedback 🔍
• Custom permissions 🔒

We split up, experimented separately, then met for coffee to compare notes.

**The result? Only 1 out of 5 was actually useful.**

❌ Notifications: Cool sound effects don't make me more productive
❌ Auto-formatting: My IDE + git hooks already handle this perfectly
❌ Logging: Makes sense for complex systems, not for coding a single feature  
❌ Code feedback: CLAUDE.md, linting, and code reviews already cover this

✅ Custom permissions: Finally! Something that actually solved a real problem - protecting sensitive files

**The plot twist?** My teammate had identical findings.

Here's what 2 experienced developers learned about AI tooling:

🧠 **Always ask**: "Am I actually gaining something, or just adding complexity?"

⚡ **Check first**: Can existing tools (IDE, git, linting) solve this faster and more reliably?

🎯 **Resist the hype**: Just because it has "AI" doesn't mean it's better than proven solutions

💡 **Tailor to YOUR needs**: Don't follow examples blindly - find what actually moves the needle

The best AI tools don't replace everything - they fill gaps that traditional tools can't.

**Don't get me wrong** - hooks are a phenomenal feature with incredible potential. But for me, at least for now, their real power shines in complex systems rather than typical programming projects. Think multi-service orchestration, compliance workflows, or enterprise-scale operations where you need sophisticated coordination between multiple tools and processes.

What's your experience with AI dev tools? Are you solving real problems or just adding shiny complexity? 

#AI #DeveloperTools #ClaudeCode #ProductivityHacks #SoftwareDevelopment

---

### Polish Translation

🏆 Jak nie dać się zwieść hype'owi AI - lekcja z hooków Claude Code 

Z kolegą z zespołu byliśmy podekscytowani funkcją hooków w Claude Code. Lista 5 obiecujących przykładów z dokumentacji wygląda następująco:
• Notyfikacje 🔔
• Auto-formatowanie ✨  
• Logowanie 📊
• Feedback kodu 🔍
• Niestandardowe uprawnienia 🔒

Pomysł był prosty, każdy eksperymentuje osobno, a potem spotykamy się na kawę żeby porównać notatki.

**Wynik? Tylko 1 z 5 okazał się naprawdę przydatny.**

❌ Notyfikacje: Fajne efekty dźwiękowe nie czynią mnie bardziej produktywnym
❌ Auto-formatowanie: IDE + git hooki już to obsługują perfekcyjnie
❌ Logowanie: Ma sens w złożonych systemach, nie przy kodowaniu pojedynczej funkcji
❌ Feedback kodu: CLAUDE.md, linting i code review już to pokrywają

✅ Niestandardowe uprawnienia: Wreszcie! Coś co naprawdę rozwiązało realny problem - ochrona wrażliwych plików

**Plot twist?** Mój kolega z zespołu miał identyczne obserwacje.

Oto krótka checklista przed wdrożeniem  narzędziach AI do procesu:

🧠 **Zawsze pytaj**: "Czy naprawdę coś zyskuję, czy tylko dodaję złożoność?"

⚡ **Sprawdź najpierw**: Czy istniejące narzędzia (IDE, git, linting) nie rozwiążą tego szybciej i niezawodniej?

🎯 **Opieraj się hype'owi**: To, że ma "AI" nie znaczy, że jest lepsze od sprawdzonych rozwiązań

💡 **Dostosuj do SWOICH potrzeb**: Nie śledź ślepo przykładów - znajdź to, co naprawdę ma znaczenie

Najlepsze narzędzia AI nie zastępują wszystkiego - wypełniają luki, których tradycyjne narzędzia nie mogą.

**Nie zrozumcie mnie źle** - hooki to fenomenalna funkcja o niesamowitym potencjale. Ale dla mnie, przynajmniej na razie, ich prawdziwa moc błyszczy w złożonych systemach, a nie w typowych projektach programistycznych. Pomyślcie o orkiestracji wielu serwisów, workflow compliance'u czy operacjach na skalę organizacji, gdzie potrzebna jest wyrafinowana koordynacja między wieloma narzędziami i procesami.

Jakie są wasze wnioski i ciekawe zastosowania, które realnie rozwiązują wasz problem? 🤔
👇🏻 Link do dokumentacji jeżeli jeszcze nie słyszał o hookach w komentarzu 

