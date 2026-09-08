## Spis treści
1. [Architektura frameworka testowego - zasady](#architektura_frameworka_zasady)
1a. [Hierarchia testów](#hierarchia_testów)


## Architektura frameworka testowego - zasady <a name="architektura_frameworka_zasady"></a>

Dwie podstawowe, bezwględne, zasady:

1. <ins> Przemyślana struktura organizacyjna testów.</ins>
2. <ins> Podział plików według ich przeznaczenia i technologii.</ins>


### Hierarchia testów - struktura drzewa <a name="hierarchia_testów"></a>

- Pojedynczy plik .robot to Zestaw Testów (Test Suite).
- Wszystkie przypadki testowe (Test Cases) zapisane w jednym pliku tworzą automatycznie zestaw o nazwie tego pliku.