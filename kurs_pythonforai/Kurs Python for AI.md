
## Sprawdzenie wersji Python w terminalu

`python3 --version`


---


## Visual Studio Code (VS Code)

- na bazie VS Code zbudowano Cursor;
- Cursor to AI-powered coding assistant;
- Microsoft is the owner and developer;
- core source code is open-source under the MIT License and hosted on GitHub


---


## Why I need to add VS Code app to the PATH?

- PATH is an environment variable;
- Allows you to run its executable commands from any directory without typing the full file path;


--- 


## VS Code Extensions

### Python

  ![Pasted image 20260717141032.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717141032.png)


- developed by Microsoft;
- transforms VS Code into a comprehensive Python development environment;
- bridge between the VS Code editor and the local Python interpreter;
- enabling code execution, testing, and environment management;
- installing the extension automatically triggers the installation of Python Debugger and Pylance


---

### Pylance

![Pasted image 20260717150756.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717150756.png)


- high-performance language server extension;
- provides advanced Python language support;
- runs as a background process that analyzes your code to provide real-time feedback and assistance;
- code completion and error detection;
- works alongside the Python extension;


---

### Jupyter

![Pasted image 20260717151203.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717151203.png)



---


## Configure Python execution in VSCode


- in Settings type in: _Python Terminal Execute In File Dir_  

![Pasted image 20260717144145.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717144145.png)


- VS Code will execute Python script from the file's directory instead of workspace root;
- prevents common path-related errors;
- if your script reads a file with `open('data.csv')`, it will look for the file in the same folder as your script, which is usually what you want. Without this setting, it would look in your project root instead, causing “file not found” errors;


---


## Struktura Projektu

![Screenshot From 2026-09-02 11-50-47.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Screenshot%20From%202026-09-02%2011-50-47.png)


- przykład: PythonProjects ---> python-for-ai
- use lowercase letters with dashes (called “kebab-case”) like `python-for-ai` or `my-first-project`. This matches how projects appear on GitHub.


![Pasted image 20260717153005.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717153005.png)


---


## Stwórz Workspace 


- po otwarciu folderu, w którym zamierzam przechowywać projekt należy zapisać ten folder jako workspace;
- workspace is like a bookmark for your project;
- workspace saves your project settings and makes it easy to return to your project later;
- it remembers:
	- which folder you’re working in;
	- your editor settings for this project;
	- which files you had open;
	- your debugging configuration.

![Pasted image 20260717154808.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717154808.png)

![Pasted image 20260717154850.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717154850.png)

![Pasted image 20260717155138.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717155138.png)

- po ustawieniu "workspace" mogę zamknąć VS Code, następnie przejść do katalogu w którym zapisałem workspace i zrobić double-click na skrót - VS Code otworzy się samo w miejscu, w którym ostatnio pracowałem


---


## Ustaw tree indent

- zwiększa czytelność struktury drzewa katalogów

![Pasted image 20260717161942.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717161942.png)

![Pasted image 20260717162026.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717162026.png)

- zwiększenie do 20 pixeli:

![Pasted image 20260717162127.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717162127.png)

![Pasted image 20260717162158.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717162158.png)


---

## Uruchamianie kodu z terminala

![Pasted image 20260717160306.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260717160306.png)


---
## Virtual Environment

- wyizolowane środowisko wirtualne dla konkretnego projektu

### Po co to jest?

Wyobraź sobie, że pracujesz nad dwoma projektami:

- Projekt A potrzebuje `django==3.2`
- Projekt B potrzebuje `django==4.2`

Jeśli instalujesz pakiety globalnie (na cały system), masz problem — nie możesz mieć dwóch wersji tego samego pakietu naraz. **venv** rozwiązuje to, tworząc osobny, odizolowany "folder" z własnym interpreterem Pythona i własnymi pakietami dla każdego projektu.


### Tworzenie virtual environment z poziomu VSCode

- CTRL+SHIFT+P --- otwiera "command palette"

![Screenshot From 2026-09-02 12-07-25.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Screenshot%20From%202026-09-02%2011-50-47.png)

![Pasted image 20260902120946.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260902120946.png)

![Pasted image 20260902121432.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260902121432.png)

- Po uruchomieniu nowego terminala venv powinien zostać aktywowany przez VSCode

![Pasted image 20260902121539.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260902121539.png)



### Tworzenie venv z poziomu terminala

```shell
python -m venv nazwa_srodowiska
```

Najczęściej nazywa się je po prostu `venv` lub `.venv`.

**2. Aktywacja:**

<em>Linux/Mac:</em>

```bash
source venv/bin/activate
```

<em>Windows:</em>


```bash
venv\Scripts\activate
```


**3. Instalacja pakietów (tylko wewnątrz venv):**


```bash
pip install requests pandas
```

**4. Dezaktywacja:**


```bash
deactivate
```

![Pasted image 20260902133214.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260902133214.png)

- Instaluję paczkę requests

![Pasted image 20260902141324.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260902141324.png)

![Pasted image 20260902141437.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260902141437.png)

- instaluję robotframework

![Pasted image 20260902141522.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260902141522.png)

![Pasted image 20260902141556.png](https://github.com/lkldz/tutoriale/blob/main/kurs_pythonforai/Screeny/Pasted%20image%2020260902141556.png)


### Dlaczego warto używać virtual environment ?

- **Izolacja** — pakiety jednego projektu nie kolidują z innymi
- **Czystość** — nie zaśmiecasz globalnej instalacji Pythona
- **Reprodukowalność** — możesz łatwo odtworzyć środowisko na innym komputerze (np. przez `requirements.txt`)
- **Bezpieczeństwo** — nie musisz mieć uprawnień administratora, żeby instalować pakiety



### Typowy workflow



```bash
# Tworzysz projekt
mkdir moj_projekt
cd moj_projekt

# Tworzysz środowisko
python -m venv venv

# Aktywujesz
source venv/bin/activate

# Instalujesz zależności
pip install flask

# Zapisujesz listę zależności
pip freeze > requirements.txt

# Ktoś inny (albo ty na innym komputerze) odtwarza środowisko:
pip install -r requirements.txt
```

- folder `venv` **nie powinien** być commitowany do gita — dodaje się go do `.gitignore`, bo można go zawsze odtworzyć z `requirements.txt`.

- tworzę plik requirements.txt

![[Pasted image 20260902141926.png]]

- instaluję plik requirements.txt w nowym środowisku

![[Pasted image 20260902142825.png]]

### Pełna kolejność kroków odtwarzających środowisko projektowe



```bash
# 1. Tworzysz nowe środowisko wirtualne
python -m venv venv

# 2. Aktywujesz je
source venv/bin/activate        # Linux/Mac
# albo
venv\Scripts\activate           # Windows

# 3. DOPIERO TERAZ instalujesz zależności z pliku
pip install -r requirements.txt
```

- `pip install -r requirements.txt` to zwykłe polecenie `pip`, które instaluje pakiety **tam, gdzie aktualnie "jesteś"**:
- Jeśli venv jest aktywne → pakiety trafią do venv (stan oczekiwany!)
- Jeśli venv **nie** jest aktywne → pakiety trafią globalnie do systemowego Pythona (czego zwykle nie chcesz)

## Robot Framework - zdecydowanie w venv!

- Robot Framework instaluj w wirtualnym środowisku, prawie zawsze i bez wyjątków.

### Dlaczego akurat w przypadku Robot Framework to szczególnie ważne?

**1. Duża liczba zależności i bibliotek**

Robot Framework rzadko działa sam — zwykle dochodzą do tego:

```bash
pip install robotframework
pip install robotframework-seleniumlibrary
pip install robotframework-requests
pip install robotframework-databaselibrary
# ... i tak dalej
```

Każdy projekt testowy może potrzebować innego zestawu bibliotek i innych wersji.

**2. Konflikty wersji między projektami**

Przykład z życia:

- Projekt testowy A (stary) → `robotframework-seleniumlibrary==5.1.3` + Selenium 3.x
- Projekt testowy B (nowy) → `robotframework-seleniumlibrary==6.2.0` + Selenium 4.x

Bez venv — katastrofa. Z venv — każdy projekt ma swoje, izolowane wersje.

**3. Reprodukowalność w CI/CD**

Testy automatyczne (a Robot Framework głównie do tego służy) muszą działać identycznie:

- na Twoim laptopie
- na laptopie kolegi
- na serwerze CI/CD (Jenkins, GitLab CI, GitHub Actions)

Venv + `requirements.txt` gwarantuje, że wszędzie zainstaluje się dokładnie to samo.

## Typowy setup projektu z Robot Framework



```bash
mkdir moj_projekt_testowy
cd moj_projekt_testowy

python -m venv venv
source venv/bin/activate

pip install robotframework
pip install robotframework-seleniumlibrary

pip freeze > requirements.txt
```

Struktura projektu:

```
moj_projekt_testowy/
├── venv/                    # (w .gitignore!)
├── tests/
│   └── test_login.robot
├── requirements.txt
└── .gitignore
```

### Kiedy globalna instalacja mogłaby mieć sens?

Szczerze — praktycznie nigdy w kontekście pracy zespołowej/produkcyjnej. Jedyny scenariusz to:

- szybki, jednorazowy test "czy to w ogóle działa" na Twoim prywatnym komputerze
- ale i wtedy lepiej wyrobić sobie nawyk venv, żeby nie zaśmiecać systemu


## Przykładowy .gitignore dla projektu Python z venv

Oto typowy plik `.gitignore`, którego użyłbym dla projektu z venv (np. z Robot Framework):


```gitignore
# Wirtualne środowisko
venv/
.venv/
env/
ENV/

# Cache Pythona
__pycache__/
*.py[cod]
*$py.class

# Pliki dystrybucyjne / instalacyjne
*.egg-info/
dist/
build/

# Zmienne środowiskowe (jeśli używasz .env)
.env
.env.local

# IDE
.vscode/
.idea/

# Logi
*.log

# System operacyjny
.DS_Store          # Mac
Thumbs.db          # Windows
```

### Najważniejsza linijka dla Twojego pytania

To właśnie **pierwsze cztery linijki** odpowiadają za venv:


```gitignore
venv/
.venv/
env/
ENV/
```

Dodałem kilka wariantów nazw, bo różni developerzy nazywają folder z venv różnie — Ty prawdopodobnie użyjesz tylko jednej z tych nazw (np. `venv/`), więc możesz spokojnie usunąć te, których nie potrzebujesz.

### Dla projektu z Robot Framework dodałbym jeszcze



```gitignore
# Robot Framework - wyniki testów
results/
output.xml
log.html
report.html
*.png
```

Te pliki (`output.xml`, `log.html`, `report.html`) to raporty generowane po każdym uruchomieniu testów — nie mają sensu w repozytorium, bo są tworzone od nowa przy każdym przebiegu.

### Jak to sprawdzić w praktyce?


```bash
# Utwórz .gitignore PRZED pierwszym commitem (albo od razu na początku projektu)
touch .gitignore

# Sprawdź, czy venv faktycznie jest ignorowany
git status
# folder venv/ nie powinien się pojawić na liście
```

### Ważna uwaga ⚠️

Jeśli **już** wcześniej dodałeś folder `venv` do repozytorium (przez pomyłkę, zanim stworzyłeś `.gitignore`), samo dodanie go do `.gitignore` **nie usunie go z historii Gita**. Musisz go najpierw ręcznie usunąć ze śledzenia:


```bash
git rm -r --cached venv/
git commit -m "Remove venv from repository"
```


## Kompletny .gitignore dla projektu Robot Framework + Python


```gitignore
# ============================================
# Wirtualne środowisko
# ============================================
venv/
.venv/
env/
ENV/

# ============================================
# Cache i skompilowane pliki Pythona
# ============================================
__pycache__/
*.py[cod]
*$py.class
*.pyc

# ============================================
# Pliki dystrybucyjne / instalacyjne
# ============================================
*.egg-info/
dist/
build/
*.egg

# ============================================
# Robot Framework - wyniki testów
# ============================================
results/
output/
*.xml
log.html
report.html
selenium-screenshot-*.png
geckodriver.log
chromedriver.log

# ============================================
# Zmienne środowiskowe i dane wrażliwe
# ============================================
.env
.env.local
secrets.yaml
config_local.py

# ============================================
# IDE / edytory
# ============================================
.vscode/
.idea/
*.swp
*.swo

# ============================================
# System operacyjny
# ============================================
.DS_Store
Thumbs.db
desktop.ini

# ============================================
# Coverage / raporty testów jednostkowych
# ============================================
.coverage
htmlcov/
.pytest_cache/
```

### Kilka wyjaśnień do sekcji specyficznych dla Robot Framework

**`*.xml`** — uważaj z tą regułą! Jeśli w projekcie trzymasz jakieś dane testowe w XML (np. pliki wejściowe do testów), ta reguła je też zignoruje. W takim wypadku lepiej być bardziej precyzyjnym:


```gitignore
output.xml
```

zamiast generycznego `*.xml`.

**`selenium-screenshot-*.png`** — Robot Framework + SeleniumLibrary domyślnie robi zrzuty ekranu przy niepowodzeniu testu i nazywa je właśnie w ten sposób.

**`secrets.yaml` / `config_local.py`** — jeśli trzymasz dane logowania do testowanej aplikacji (loginy, hasła, tokeny) w osobnym pliku konfiguracyjnym, koniecznie dodaj go do `.gitignore` i zamiast tego commituj plik `config_example.yaml` jako szablon.



## pip i paczki (pakiety) w Pythonie

### Co to jest pip?

**pip**  to **menedżer pakietów** dla Pythona. To narzędzie, które pozwala:

- **instalować** gotowy kod napisany przez innych
- **usuwać** niepotrzebne paczki
- **aktualizować** paczki do nowszych wersji
- **zarządzać** wersjami i zależnościami

Pip jest domyślnie dołączony do Pythona (od wersji 3.4+), więc zwykle nie musisz go osobno instalować.

### Co to jest "paczka" (pakiet)?

**Paczka** to gotowy, spakowany kawałek kodu — biblioteka napisana przez kogoś innego, którą możesz wykorzystać w swoim projekcie, zamiast pisać wszystko od zera.

#### Analogia z życia

Wyobraź sobie, że budujesz dom:

- Możesz **wypalić własne cegły** od zera (napisać cały kod samemu)
- Albo **kupić gotowe cegły** w sklepie budowlanym (zainstalować paczkę)

Nikt rozsądny nie wypala cegieł od zera, jeśli może je kupić — to samo z kodem. Po co pisać własną bibliotekę do wysyłania requestów HTTP, skoro ktoś już napisał świetną paczkę `requests`?

### Skąd biorą się paczki?

Paczki są publikowane na **PyPI** (Python Package Index) — to takie centralne "repozytorium" / "sklep" ze wszystkimi publicznymi paczkami Pythona.

🔗 [https://pypi.org](https://pypi.org)

Kiedy robisz:


```bash
pip install requests
```

pip łączy się z PyPI, znajduje paczkę `requests`, pobiera ją i instaluje w Twoim środowisku (systemowym albo venv).

### Podstawowe komendy pip


```bash
# Instalacja paczki
pip install requests

# Instalacja konkretnej wersji
pip install requests==2.31.0

# Instalacja z pliku requirements.txt
pip install -r requirements.txt

# Odinstalowanie paczki
pip uninstall requests

# Lista zainstalowanych paczek
pip list

# Sprawdzenie szczegółów paczki
pip show requests

# Zapisanie aktualnych paczek do pliku
pip freeze > requirements.txt

# Aktualizacja paczki
pip install --upgrade requests
```

### Przykład z wcześniejszych czynności

Gdy instalowałeś Robot Framework, robiłeś dokładnie to:


```bash
pip install robotframework
pip install robotframework-seleniumlibrary
```

Tutaj:

- `robotframework` — to **paczka** zawierająca cały silnik do uruchamiania testów
- `robotframework-seleniumlibrary` — to **kolejna paczka**, dodająca możliwość sterowania przeglądarką

Zamiast pisać framework do testów automatycznych od zera (miesiące pracy!), instalujesz gotową paczkę w kilka sekund.

### Zależności — paczki potrzebują innych paczek

Paczki często **zależą** od innych paczek. Przykład:

```
robotframework-seleniumlibrary
    └── wymaga: selenium
            └── wymaga: urllib3
                    └── wymaga: ...
```

Kiedy instalujesz jedną paczkę, pip automatycznie instaluje też wszystkie jej zależności — nie musisz robić tego ręcznie.

### Jak sprawdzić, co dana paczka faktycznie robi?



```bash
pip show robotframework-seleniumlibrary
```

Wyświetli m.in.:

```
Name: robotframework-seleniumlibrary
Version: 6.2.0
Summary: Web testing library for Robot Framework
Requires: robotframework, selenium, ...
```
