**Spis treści**

[Architektura frameworka testowego - zasady](#architektura_frameworka_zasady)

[Hierarchia testów](#hierarchia_testów)


## Architektura frameworka testowego - zasady <a name="architektura_frameworka_zasady"></a>

Dwie podstawowe, bezwględne, zasady:

1. Przemyślana struktura organizacyjna testów.
2. Podział plików według ich przeznaczenia i technologii.


### Hierarchia testów - struktura drzewa <a name="hierarchia_testów"></a>

- Pojedynczy plik .robot to <em>Zestaw Testów (Test Suite)</em>.
- Wszystkie przypadki testowe (Test Cases) zapisane w jednym pliku tworzą automatycznie zestaw o nazwie tego pliku.
- Katalog z plikami .robot to <em>Wyższy Zestaw Testów (Parent Suite)</em>. 
  
<em>Przykład:</em> 
```text
Jeśli wrzucisz 3 pliki z testami do katalogu smoke_tests/, 
folder ten staje się nadrzędnym zestawem zawierającym 3 podzestawy.
```
- Zagnieżdżanie folderów bez limitu. 

<em>Przykład:</em>
```text
Możesz tworzyć podfoldery w podfolderach (np. tests/api/v1/auth/). 
Robot odwzoruje to w raportach HTML 1:1 jako drzewo testów.
```

- Plik inicjalizacyjny  ```(__init__.robot)``` 

Pozwala ustawić konfigurację dla całego folderu/modułu naraz.

<em>Przykładowo:</em> uruchama przeglądarkę przed wykonaniem jakiegokolwiek testu z tego folderu (Setup) i zamknąć ją na koniec (Teardown).

