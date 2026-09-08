**Spis treści**

[Architektura frameworka testowego - zasady](#architektura_frameworka_zasady)

[Hierarchia testów](#hierarchia_testów)

[Przykładowa struktura katalogów frameworka produkcyjnego](#test_framework_structure)


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

### Typy plików <a name="typy_plików"></a>

- <em><ins>Pliki przypadków testowych (.robot)</ins></em><br>
    - Składnia i format: Robot Framework

    - Miejsce, gdzie spisujesz kroki biznesowo-użytkowe konkretnych testów (np. login_tests.robot).

- <em><ins>Pliki zasobów (Resource files, .resource)</ins></em><br>
    - Składnia i format: Robot Framework

    - Reużywalne elementy - keywords oraz zmienne.<br> 
    Zamiast powtarzać te same kroki w 10 testach, tworzysz tu tzw. User Keywords (np. Zaloguj jako Admin) oraz wspólne zmienne.

- <em><ins>Pliki inicjalizacyjne</ins></em> ```(__init__.robot)```
    - Składnia i format: Robot Framework
    
    - Konfiguracja poziomu katalogu (tagi, setupy/teardowny dla grupy testów).

- <em><ins>Biblioteki testowe (Test libraries)</ins></em>
    - Składnia i format: Python albo inny język programowania
    
    - Gdy Robot nie ma gotowego słowa kluczowego do obsłużenia specyficznego API,<br> 
    bazy danych czy socketów, piszesz funkcję w Pythonie, a Robot widzi ją jako keyword.

- <em><ins>Pliki zmiennych (Variable files, .py files)</ins></em>
    - Składnia i format: Python (albo inny język programowania)
   
    - Używane, gdy zmienne są dynamiczne lub skomplikowane <br> 
    (np. pobieranie tokena z zewnętrznego API, parsowanie JSON-a konfiguracyjnego przed startem testów).


### Przykładowa struktura katalogów frameworka produkcyjnego <a name="test_framework_structure"></a>


```text

my-robot-framework/
│
├── config/                          # Konfiguracja środowiskowa
│   ├── dev.yaml
│   ├── stage.yaml
│   └── prod.yaml
│
├── libraries/                       # Twoje własne biblioteki w Pythonie (kod SDET)
│   ├── __init__.py
│   ├── DatabaseClient.py            # Logika zapytań SQL / NoSQL
│   └── AuthHelper.py                # Np. generowanie tokenów JWT, obsługa kryptografii
│
├── resources/                       # Reużywalne klocki Robot Framework (.resource)
│   ├── locators/                    # Selektory UI (oddzielone od akcji)
│   │   ├── login_locators.resource
│   │   └── checkout_locators.resource
│   │
│   ├── pages/                       # Warstwa Page Object Model (słowa kluczowe UI)
│   │   ├── LoginPage.resource
│   │   └── CheckoutPage.resource
│   │
│   ├── api/                         # Słowa kluczowe do obsługi endpointów
│   │   ├── UsersEndpoint.resource
│   │   └── OrdersEndpoint.resource
│   │
│   └── common.resource              # Globalne setupy, teardowny, wspólne akcje
│
├── tests/                           # Przypadki testowe (pliki .robot)
│   ├── __init__.robot               # Globalny setup przed całym przebiegiem testów
│   │
│   ├── ui/
│   │   ├── __init__.robot           # Konfiguracja przeglądarki (np. Browser Library / Selenium)
│   │   ├── auth_tests.robot
│   │   └── checkout_tests.robot
│   │
│   └── api/
│       ├── __init__.robot           # Konfiguracja sesji HTTP / nagłówków
│       ├── user_crud_tests.robot
│       └── payment_processing.robot
│
├── test_data/                       # Dane wejściowe do testów
│   ├── users.json
│   └── payloads/
│       └── create_order.json
│
├── results/                         # Folder wyjściowy na log.html, report.html, output.xml
│   └── .gitkeep
│
├── .gitignore
├── requirements.txt                 # Zależności Python (robotframework, requests, itp.)
└── README.md

```