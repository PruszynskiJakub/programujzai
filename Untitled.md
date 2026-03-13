

Kiedy używać podagenta a kiedy skilla ?






Jeżeli nie weźmiemy pod uwagę złożoności w projektowaniu narzędzi np gdy chcemy przerzucać pomiędzy narzędziami  pliki, wówczas biorąc uwagę ilość typów plików ich struktur wówczas nie jesteśmy w stanie w efektywny sposób tym zarządzić.

Budowanie sztywnych narzędzi dla modeli na przykładzie jak skutecznie wykonywać operacje na plikach ?

Aby nie marnować okna kontekstowego, oraz zwiększać ryzyka pomyłek oraz niwelować koszty - pliki oraz artefakty przekazujemy nie poprzez wartość ale poprzez referencję - w postaci identyfikatora lub ścieżki.

Obsługa plików poprzez agenta nie jest z pewnością czymś trywialnym.
Gdy dodamy również do tego transformację tych danych wówczas dostajemy kolejny poziom złożoności. 
Złożoność ta wynika z dowolności która możemy rozpatrywać przez dwie składowe:
1. dowolność formatów danych
2. dowolności struktur wewnątrz tych plików

#### Naiwne 
Innymi słowy projektujemy narzędzie obejmujące wyłącznie jeden proces, z góry znaną ograniczoną liczbą formatów plików oraz struktur.
Wówczas nasze narzędzia możemy organizować wyłącznie wokół tego i rozpatrując je z perspektywy ich miejsca oraz zastosowania w tym procesie.
Dla takiego przykładu prawdopodobnie nie potrzebujemy w ogóle agenta, zapewne wystarczy AI workflow.

#### Dojrzalsze
Tworzymy dedykowane narzędzie per format plików zachowując jednocześnie dowolność w ich strukturze. Wadą tego podejścia jest konieczność dodawania 
