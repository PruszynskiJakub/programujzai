---
tags:
  - writings
  - linkedin
author: "[[Jakub Pruszyński]]"
categories:
  - "[[Posts]]"
created: 2025-08-22
published: 2025-08-22
---
### Backstory
Z wielką mocą rodzi się wielka odpowiedzialność - LLMy i ich wykorzystanie idealnie pasują do tej maksymy. Jest to potężna i stosunkowy nowy obszar technologiczny, która nie jest jeszcze ugruntowany, troche jak dziki zachód - dużo skarbów i dużo niebezpieczeństw. Jednym z takich niebezpieczeństw o których sporo się mówiło zwłaszcza w kontekście interfejsów chatowych w aplikacjach webowych był temat danych wrażliwych. Znane m.in były przypadki w wycieków  z wewnętrznych projektów m.in Samsunga właśnie poprzez chat.
Troche mniej niestety się mówi o kwestiach bezpieczeństwa od strony deweloperskiej w wykorzystaniu AI asystentów. 
Początkowo gdy owi asystenci byli jeszcze nieociosanymi rozwiązaniami, których kontekst stanowi wyłącznie wyróżnione przez nas pliki nie stanowiło to dużego problemu. Wraz z rozwojem narzędzi zyskały one umiejętność podglądania obecnie lub niedawno otwartych plików. Aktualnie asystenci ewoluowali w kierunku rozwiązań agentów mających bogaty wachlarz dostępnych narzędzi. Narzędzi które mogą przeszukiwać w sposób aktywny nasz projekt na wiele różnych sposobów. Naiwnym jest myślenie, że przez to że wiele z tych asystentów AI wspiera się gitem wystarczającym zabezpieczeniem się przed wyciekaniem danych do AI jest dodanie przysłowiowego .env do .gitignore. Niestety tak to nie działa. Faktem jest, że np Claude Code uniemożliwia zastosowanie referencji do pliku z użyciem @, jednak jest to złudne, ponieważ sam agent jeżeli uzna wyszukanie takich plików za konieczne, nie będzie miał z tym najmniejszego problemu z wykorzystaniem narzędzi jak Grep czy Read. 
Dlatego Zawsze trzeba zachować zdrowy rozsądek i poznać swoje narzędzie, najlepiej w jakiś hobby projekcie gdzie konsekwencje są niewielkie,  jest to pierwszy krok do bezpiecznego i świadomego korzystania z narzędzi AI. 
Na szczęście w ramach Claude Code od ponad miesiąca istnieje wbudowana funkcjonalność hooków, która pozwala nam zabezpieczyć nasze sekrety przed wścibskim wzrokiem AI. Warto zarazem trzymać schemat .env jako odnośnik dla naszego asystenta aby ten mógł skutecznie wykorzystywać zmienne środowiskowego.
### Draft

🔐 I thought adding .env to .gitignore was enough to protect my secrets from AI assistants.

I was wrong.

**The Problem:**
When AI coding assistants were simple tools that only saw highlighted files, security felt manageable. But today's AI agents? They're digital detectives with access to search tools, file readers, and project explorers. 

**My Journey:**
I discovered this the hard way when I realized that while Claude Code blocks direct @ file references, the agent itself can easily use Grep and Read tools to find exactly what it needs. That .env file I thought was "hidden"? Just a search away.

**The Reality Check:**
Modern AI assistants are like giving someone the keys to your entire codebase. Sure, they can't directly access files you don't reference, but they can absolutely search for them when they deem it necessary.

**The Solution:**
🪝 Claude Code's hooks functionality became my safety net. Instead of playing hide-and-seek with sensitive files, I now use proactive security measures that actually work.

**The Bigger Picture:**
This isn't about paranoia – it's about responsible AI adoption. Just like we learned to sanitize database inputs and validate user data, we need new security patterns for the AI-assisted development era.

💡 **My advice:** Start experimenting with AI tools on hobby projects first. Learn their capabilities and limitations in a safe environment. The consequences of mistakes are smaller, but the lessons are just as valuable.

The power of AI assistants is incredible, but with great power comes great responsibility – especially when it comes to protecting sensitive data.

What security practices have you adopted for AI-assisted development? 

#AI #CyberSecurity #SoftwareDevelopment #DataProtection

### Final

🔐 I thought adding .env to .gitignore was enough to protect my secrets from AI assistants.

I was dead wrong. 💀

**The Wake-Up Call 📢**
Modern AI coding assistants aren't the simple tools they used to be. They've evolved into digital detectives 🕵️ with powerful search capabilities, file readers, and project explorers.

**My "Aha!" Moment 💡**
While Claude Code blocks direct @ file references, I realized the agent can easily use its Grep and Read tools to hunt down any file it needs. That .env file I thought was "safely hidden"? Just one search command away. 😱

**The Hard Truth 🎯**
Using today's AI assistants is like handing over the master keys 🔑 to your entire codebase. They can't directly peek at files you don't mention, but they absolutely can search for them when they think it's necessary.

**The Game Changer 🛡️**
Claude Code's hooks functionality became my security lifeline. Instead of playing digital hide-and-seek with sensitive files, I now use proactive protection that actually works.

**The Bigger Picture 🌍**
This isn't about AI paranoia – it's about evolving our security mindset. Just like we learned to sanitize SQL inputs and validate user data, we need fresh security patterns for the AI-powered development era.

**My Golden Rule ✨**
Always test AI tools on hobby projects first. Learn their superpowers and blind spots in a safe sandbox 🏖️ where mistakes don't cost you sleep (or your job).

The AI assistant revolution is incredible, but remember: with great power comes great responsibility – especially with sensitive data. 🦸‍♂️

**👇 Drop a comment below – I've got a ready-to-use gist for setting up Claude Code security hooks!**

What security practices have you adopted for AI-assisted development? Share your wins and fails! 🚀

#AI #CyberSecurity #SoftwareDevelopment #DataProtection #ClaudeCode

### Polish Version

🔐 Myślałem, że dodanie .env do .gitignore wystarczy, żeby chronić sekrety przed asystentami AI.

Bardzo się myliłem. 💀

**Moment prawdy 📢**
Współczesne asystenty AI to już nie te proste narzędzia sprzed lat. Ewoluowały w cyfrowych detektywów 🕵️ z potężnymi możliwościami wyszukiwania, czytania plików i eksploracji projektów.

**Moje "aha!" 💡**
Chociaż Claude Code blokuje bezpośrednie referencje przez @, zdałem sobie sprawę, że agent może łatwo użyć narzędzi Grep i Read, żeby znaleźć każdy plik, jakiego potrzebuje. Ten plik .env, który myślałem, że jest "bezpiecznie ukryty"? Jedna komenda wyszukiwania i gotowe. 😱

**Gorzka prawda 🎯**
Korzystanie z dzisiejszych asystentów AI to jak wręczenie kluczy do całej bazy kodu 🔑. Nie mogą bezpośrednio podglądać plików, których nie wspominasz, ale absolutnie mogą ich szukać, gdy uznają to za konieczne.

**Przełom 🛡️**
Funkcjonalność hooków w Claude Code stała się moją kotwicą bezpieczeństwa. Zamiast grać w cyfrowe chowanego z wrażliwymi plikami, teraz używam proaktywnej ochrony, która rzeczywiście działa.

**Szerszy obraz 🌍**
To nie paranoja na punkcie AI – to ewolucja naszego myślenia o bezpieczeństwie. Tak jak nauczyliśmy się sanityzować zapytania SQL i walidować dane użytkowników, potrzebujemy nowych wzorców bezpieczeństwa dla ery rozwoju wspomaganego przez AI.

**Moja złota zasada ✨**
Zawsze testuj narzędzia AI najpierw na projektach hobbystycznych. Poznaj ich supermoce i ślepe punkty w bezpiecznej piaskownicy 🏖️, gdzie błędy nie kosztują Cię snu (ani pracy).

Rewolucja asystentów AI jest niesamowita, ale pamiętaj: z wielką mocą wiąże się wielka odpowiedzialność – szczególnie z wrażliwymi danymi. 🦸‍♂️

**👇 Zostaw komentarz poniżej – mam gotowy gist do konfiguracji hooków bezpieczeństwa Claude Code!**

Jakie praktyki bezpieczeństwa przyjęliście w rozwoju wspomaganym przez AI? Podzielcie się sukcesami i porażkami! 🚀

#AI #CyberSecurity #SoftwareDevelopment #DataProtection #ClaudeCode
