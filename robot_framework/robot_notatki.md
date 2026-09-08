**Spis treści**

[Architektura frameworka testowego - zasady](#architektura_frameworka_zasady)

[Hierarchia testów](#hierarchia_testów)


## Architektura frameworka testowego - zasady <a name="architektura_frameworka_zasady"></a>

Dwie podstawowe, bezwględne, zasady:

1. Przemyślana struktura organizacyjna testów.
2. Podział plików według ich przeznaczenia i technologii.


### Hierarchia testów - struktura drzewa <a name="hierarchia_testów"></a>

- Pojedynczy plik .robot to Zestaw Testów (Test Suite).
- Wszystkie przypadki testowe (Test Cases) zapisane w jednym pliku tworzą automatycznie zestaw o nazwie tego pliku.
