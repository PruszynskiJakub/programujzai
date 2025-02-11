---
tags:
  - context
  - todo
---
Wyobraź sobie, że chcesz zaimplementować jakąś funkcjonalność, aby móc to zrobić potrzebujesz zrozumieć ją w pełni lub przynajmniej jakiś jej wycinek - zależy to od wielu czynników - wielkości czy skomplikowania zadania, Twojego doświadczenia czy obycia z domeną problemu. Wówczas mając już zrozumienie tego co jesteś w stanie objąć swoim rozumem, potrafisz zdefiniować zbiór pojęć, akcji, funkcji, klas czy relacji między nimi - właśnie to nazywamy kontekstem. Innymi słowy jest to wszystko to co stanowi badane zagadnienie oraz jego otoczenie.


User story as a context if properly written



The context from the llm perspective must be clear, everything should be logical, without understatements. In the human to human interaction a significant part of the context is hidden unspoken.

Think of context like a legal contract. Between humans, many terms are understood through common experience and cultural norms. But in a legal document, everything must be explicitly stated to be enforceable.

The context similarly to a legal contract has to be more precise the more taken action is complex or crucial. Moreover, Every form of communication is burdened with some level of imprecision.

Let me explain context hierarchy through an analogy: Think of building a house.

1. Foundation level (Project Context):

- Overall project goals
- Technical requirements
- Business constraints

2. Structural level (Domain Context):

- Specific business rules
- System interactions
- Data flows

3. Interior level (Implementation Context):

- Coding standards
- Security requirements
- Performance criteria

Just like you wouldn't discuss interior paint colors before ensuring the foundation is solid, context needs to be provided in a structured, layered way to LLMs.

When you are working on a feature, you should first present big picture (project context), then domain context and finally (the biggest part) implementation context

Consider this scenario: You're working on a feature that spans multiple domains in your system. For example, a payment processing feature that touches both user management and financial systems. How would you handle potentially conflicting contexts?

Always establish a protocol between the domains.
The having a protocol as read-only we can operate on each domain seperately.
The protocol should be always a part of the context. Moreover the types used by the protocol and methods' descriptions.


Jeśli potrzebujmy zmiennych środowiskowych wówczas nie dodajmy .env do kontekstu a jedynie klarownie podajemy nazwę zmiennej która nas interesuje.



