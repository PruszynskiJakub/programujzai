---
category:
  - "[[Posts]]"
tags:
  - linkedin
published: 2025-08-02
---
### Backstory
Tworzę aplikację w Kotlin Multiplatform Mobile będąc odpowiedzialnym za obie platformy - iOS i Android. Projekt medyczny, który właśnie osiągnął fazę MVP. Aplikacja podczas wewnętrznych faz testowania działa bez zarzutu. Gdy już wychodzi do ograniczonego grona użytkowników nagle na Sentry pojawiają się nam crashe, każdy z tą samą nic nie mówiącą nazwą 
**"C++ Exception N12_GLOBAL__N_122ExceptionObjHolderImplE"**, co jeszcze ciekawsze każdy błąd posiada zupełnie inny stackstrace - czasem zawiera on odniesienia do Coroutines, czasem do ViewModeli innym razem do czegoś jeszcze innego. 
Spędzam 6 dni na szukaniu przyczyny eksplorując wszystkie ścieżki jakie podpowiadają mi lata doświadczenia wsparte przez modele SOTA. 7 dnia osiągam fazę otwierania okien i przygotowania laptopa do lotu, i gdy już biorę zamach postanawiając zostać pszczelarzem, nagle przed oczami miga mi jedna z flag kompilatora Kotlin **"-Xpartial-linkage-loglevel=WARNING"**. Wiem, że próbowałem już innych flag w ciągu ostatnich dni, ale cóż mi szkodzi, okno dalej pozostaje otwarte. Przełom. Podczas kompilacji iOS dostaję ponad 40 wykrzykników, wszystkie mówią o tym samym - o niemożności znalezienie całej masy klas związanych z klientem Http,  błędy odnoszą się m.in do silnika DarwinLegacy, którego nie jest używany bezpośrednio przeze mnie. Szybka 5-minutowa detektywistyczna robota i okazuje się, że biblioteka do autentykcji polega na  przestarzałej wersję ktor-a w wersji 2. Stety niestety projekt jest budowany przez community  na licencji MIT, a więc pozostało a. wystawić PR profilaktycznie oraz b. potwierdzić że faktycznie podbicie wersji libki w libce rozwiązuje problem. Zmieniamy dwie linijki w lokalnej wersji, przebudowujemy - ostrzeżeń już brak, dajemy apkę do intensywnych wewnętrznych błędów, potem do zaprzyjaźnionych testerów. Mija 7 dni a błędy już się nie pojawiają. Mamy to.

### Draft

**6 days debugging a production crash. The fix? One compiler flag I'd never heard of.**

Here's what happened:

Our Kotlin Multiplatform Mobile medical app worked perfectly in testing.

Then we released to users.

Suddenly, Sentry exploded with crashes.

Every single one had the same cryptic name: "C++ Exception N12_GLOBAL__N_122ExceptionObjHolderImplE"

But here's the weird part...

Each crash had a completely different stack trace.

Sometimes it pointed to Coroutines.

Sometimes ViewModels.

Sometimes random code.

I spent 6 days exploring every possible cause.

Years of experience + AI models = nothing.

Day 7: I was literally opening windows, preparing my laptop for flight. ✈️

Maybe beekeeping wasn't such a bad career change after all.

Then I spotted it.

One compiler flag I hadn't tried: "-Xpartial-linkage-loglevel=WARNING"

What could it hurt? The window was already open anyway.

**Breakthrough.**

40+ warnings appeared during iOS compilation.

All about missing HTTP client classes.

All pointing to an old authentication library using Ktor v2.

The problem wasn't our code.

It was a dependency we barely touched.

Two lines changed in the local version.

7 days of testing later: zero crashes. ✅

**The lesson?**

Sometimes the hardest bugs hide in the quietest corners.

That authentication library we added months ago? Silent killer.

The error messages that seem unrelated? They're breadcrumbs.

**Broader insight:**

In mobile development, your biggest enemy isn't bad code.

It's invisible dependencies making decisions for you.

The tools are only as good as the flags you remember to check.

---

**What's the weirdest place you've found a critical bug hiding? 🐛**

### Final

**6 days debugging a production crash. The fix? One compiler flag I'd never heard of. 🧵**

Here's what happened:

Our Kotlin Multiplatform Mobile medical app worked perfectly in testing.

Then we released to users.

Suddenly, Sentry exploded with crashes. 💥

Every single one had the same cryptic name: "C++ Exception N12_GLOBAL__N_122ExceptionObjHolderImplE"

But here's the weird part...

Each crash had a completely different stack trace.

Sometimes it pointed to Coroutines.
Sometimes ViewModels.
Sometimes random code.

I spent 6 days exploring every possible cause.

Years of experience + AI models = nothing. 🤷‍♂️

Day 7: I was literally opening windows, preparing my laptop for flight. ✈️

Maybe beekeeping wasn't such a bad career change after all.

Then I spotted it.

One compiler flag I hadn't tried: "-Xpartial-linkage-loglevel=WARNING"

What could it hurt? The window was already open anyway.

**Breakthrough. 💡**

40+ warnings appeared during iOS compilation.

All about missing HTTP client classes.
All pointing to an old authentication library using Ktor v2.

The problem wasn't our code.

It was a dependency we barely touched.

Two lines changed in the local version.

7 days of testing later: zero crashes. ✅

**The lesson?**

Sometimes the hardest bugs hide in the quietest corners.

That authentication library we added months ago? Silent killer.

The error messages that seem unrelated? They're breadcrumbs.

**Broader insight:**

In mobile development, your biggest enemy isn't bad code.

It's invisible dependencies making decisions for you.

The tools are only as good as the flags you remember to check. 🔧

---

**What's the weirdest place you've found a critical bug hiding? 🐛**