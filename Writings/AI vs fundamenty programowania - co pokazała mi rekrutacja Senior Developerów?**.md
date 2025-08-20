---
category:
  - "[[Posts]]"
tags:
  - linkedin
created: 2025-07-30
published: 2025-08-03
author: "[[Jakub Pruszyński]]"
---
### Backstory
Ostatnie pare tygodni rekrutuję intensywnie na stanowisko Senior Mobile Developera. Decolową technologią jest Kotlin Multiplatform Mobile. KMM mimo, że ma kilka lat to nadal jest on na wczesnym etapie adopcji.  W 2024 Google ogłosiło oficjalne wsparcie dla tej technologii i ogłosiło  ją jako first choice dla rozwiązań cross platformowych. W związku z tym jak można się spodziewać, stosunkowo niewiele kandydatów jest z nią zaznajomionych, są to głównie eksperci mobilnych spod znaku zielonego robocika (Androida), ale to nic KMM zwłaszcza w połączeniu z Compose Multiplatform stanowi relatywnie niski próg wejścia dla androidowców. Tym samym spore grono pytań i fragmentów rozmowy było skupione nie wokół samej technologii KMM i zastosowanych tam mechanizmów. Lwią część rozmowy techniczne oparłem pogłębionej analizie wspólnych technologii pomiędzy Androidem i KMM czyli frameworku do UI (Jetpack Compose / Compose Multiplatform) oraz obsłudze asynchroniczności (Kotlin Coroutines plus Flow). Ze względu na specyfikę stanowiska tj. prowadzenie samodzielnie projektu po stronie mobilnej, byciem zorientowanym biznesowo etc. wszyscy kandydaci są ekspertami z kilku czasem kilkunastoletnim doświadczeniem. Jakie było zatem moje zdziwienie gdy 100% kandydatów nie miało głębokiego  zrozumienia jak działają te fundamentalne technologię. Dla jasności moje pytania nie dotyczyły podawania niskopoziomowych szczegółów implementacyjnych, dotyczyly natomiast "must-have" w mojej opinii tj. obsługi wyjątków czy zrozumienia hierarchiczności w coroutines, czy też faz rysowania w Compose gdzie wiedza o tym pozwala świadomie zarządzać rekompozycją, uzasadniać wybór użycia jednych modyfikatorów nad inne.
Rozumiem, że obecnie mamy AI i jest to wspaniałe narzędzie z którego sam korzystam codziennie i nie wyobrażam sobie zrezygnowania teraz z niego. Jednak ta rekrutacja, która z resztą jest dalej w trakcie pokazała mi jak w tym wszystkim jest wewnętrzna potrzeba zrozumienia, ciekawości i dociekliwość - generalnie dążenie do bycia rzemieślnikiem swojego fachu.

### Draft

**Alternatywne tytuły:**
1. 🤖 AI vs fundamenty programowania - co pokazała mi rekrutacja Senior Developerów?
2. 💡 Dlaczego 100% ekspertów nie znało podstaw swoich technologii? Refleksje z rekrutacji
3. 🔧 Rzemieślnik czy operator AI? O czym zapominamy w programowaniu

**Propozycja obrazu:**
Wizualizacja przedstawiająca dwie ścieżki: jedną z powierzchownym użyciem AI (ikony, chatboty) i drugą z głębokim zrozumieniem (schemat algorytmu, diagramy architektury). W centrum pytajnik lub waga symbolizująca wybór między wygodą a wiedzą.

---

**🤖

Ostatnio intensywnie rekrutowałem Senior Mobile Developerów na pozycje związane z Kotlin Multiplatform Mobile (KMM) 📱. Mimo że technologia istnieje już kilka lat, wciąż jest we wczesnej fazie adopcji. W 2024 roku Google oficjalnie ogłosił wsparcie i uznał KMM za pierwszą opcję w cross-platform developmencie 🚀.

**🎯 Znalezienie kandydatów to wyzwanie** - niewiele osób ma doświadczenie z KMM, co zrozumiałe. Dla Android developerów to jednak naturalna ścieżka rozwoju w kierunku wszechstronności, szczególnie z Compose Multiplatform.

Ale oto najbardziej zaskakujące odkrycie: **💥 100% ekspertów** (z wieloletnim, często dekady doświadczeniem) miało braki w głębokim zrozumieniu fundamentalnych technologii jak Jetpack Compose/Compose Multiplatform czy Kotlin Coroutines + Flow.

Nie pytałem o niskopoziomowe detale implementacji 🔬. Chodziło o wiedzę "must-have": obsługę wyjątków, hierarchię coroutines, fazy rysowania w Compose - wiedzę pozwalającą na świadome zarządzanie zasobami i stabilnością aplikacji ⚡.

**🤖 AI to wspaniałe narzędzie codziennej pracy** - sam z niego korzystam. Ale ta rekrutacja pokazała mi, jak bardzo potrzebujemy wewnętrznego zrozumienia, ciekawości i rzetelności. Potrzebujemy mentalności rzemieślnika 🔧, który zna swoje narzędzia od podszewki.

Technologie ewoluują błyskawicznie ⚡, ale fundamenty pozostają kluczowe. Bez nich jesteśmy jak budowniczy bez znajomości statyki - możemy budować, ale czy konstrukcja się utrzyma? 🏗️

**💭 Jak myślicie - czy w erze AI głębokie zrozumienie fundamentów staje się mniej ważne, czy wręcz przeciwnie - bardziej kluczowe?**

Dla ciekawskich link do artykułu o obsłudze błędów w Coroutines 👇🏻