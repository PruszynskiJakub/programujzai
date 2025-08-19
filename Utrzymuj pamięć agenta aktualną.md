[[6 etapów programowania z AI#^1289c1|Etap 4 Trenuj asystenta]]
W nawiązaniu do tego etapu kluczowym jest aby wprowadzając nowe zmiany zastanawiać się czy są one zmianą w podejściu, i tym samym czy powinna ulec aktualizacja pamięć agenta.
#### Przykład 
Dodanie obok strumienia stanu w ViewModelu, strumienia eventów wpływa na zmianę w podejściu. Mianowicie trzeba jasno określić:
- gdzie leży granica pomiędzy stanem a zdarzeniami
- co rozumiemy przez zdarzenia - pojawienie się informacyjnego okna dialogowego vs okna dialogowego oznaczającego błąd

#### Rozwiązanie półautomatyczne w [[Claude Code]]
Można mianowicie wykorzystać hook

