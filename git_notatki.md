# GIT - NOTATKI SZKOLENIOWE

**SPIS TREŚCI**́

[Git vs GitHub](#git-vs-github)

[Version Control System](#vcs)

[Repo](#repo)

[Wersja Git-a](#git-version)

[Inicjalizacja nowego repozytorium](#git-init)

[Katalog .git](#git-dir-hidden)

[Pobieranie (pulling) istniejącego repo z remote serwera](#pulling-existing-repo)

[Sprawdzenie bieżącego stanu repozytorium](#git-status)

[Git workflow](#git-workflow)

[Pluginy do VSCode](#vscode-pluginy)

[Untracked files](#untracked-files)

[git add](#git-add)

[git commit](#git-commit)

[Atomic commits](#atomic-commits)

[git log](#git-log)

[git config](#git-config)

[.gitignore](#gitignore)

[Branch](#branch)

[HEAD](#head)


***********************************************************************
<hr style="border:2px solid gray">

## Git vs GitHub <a name="git-vs-github"></a>

- Git to software.
- GitHub to serwis, tak jak GitLab, Bitbucket itd.
- Git działa na localhost.
- GitHub działa na remote server.


<hr style="border:2px solid gray">

## Version Control System <a name="vcs"></a>

- VCS przechowuje różne wersje tego samego pliku.
- Tworzy swego rodzaju "check pointy".
- Można przełączać się pomiędzy różnymi wersjami tego samego pliku.
- Standardowy cykl pliku:

  	  1. Write (w katalogu roboczym).
  	  2. Add (staging area).
  	  3. Commit (zapisz w historii repo).

<hr style="border:2px solid gray">

## Repo <a name="repo"></a>

- Folder zawierający pliki.
- Folder ten jest śledzony ("trackowany") przez Git.


<hr style="border:2px solid gray">

## Wersja Git-a <a name="git-version"></a>

*polecenie:*

`git --version`

- Git jest bardzo stabilnym programem.
- Członkowie zespołu mogą korzystać z różnych wersji Git-a i nie wpłynie to na funkcjonalność tego programu.


<hr style="border:2px solid gray">

## Pluginy do VSCode <a name="vscode-pluginy"></a>

Poniższe pluginy wizualizują zmiany w lokalnym repo (liniowa historia commitów, branche itd.)

- Git Graph
- GitLens


<hr style="border:2px solid gray">

## Inicjalizacja nowego repozytorium <a name="git-init"></a>

*polecenie:*

`git init`

- Powyższe polecenie tworzy nowe repozytorium (repo).
- Utworzony zostaje ukryty (*hidden*) folder .git


<hr style="border:2px solid gray">

## Katalog .git <a name="git-dir-hidden"></a>

- Przechowuje informacje związane z utworzonym repozytorium m.in:
  * konfigurację repo
  * historię commit-ów
  * informacje o stage are
- Zasadniczo użytkownik nie dokonuje zmian w tym katalogu


<hr style="border:2px solid gray">

## Pobieranie (pulling) istniejącego repo z remote serwera <a name="pulling-existing-repo"></a>

*polecenie:*

`git clone url_repozytorium`

- Git sam utworzy katalog .git
- Nie trzeba wpisywać git init


<hr style="border:2px solid gray">

## Sprawdzenie bieżącego stanu repozytorium <a name="git-status"></a>

*polecenie:*

`git status`

- Wyświetla obecny stan/status lokalnego repozytorum.
- Informacje zwracane przez git status:
  * na której jestem branch-y
  * które pliki zmieniono od czasu ostatniego commit-a
  * które pliki są staged
  * które pliki nie są staged
  * czy są "nie-trackowane" (nie śledzone) pliki


<hr style="border:2px solid gray">

## Git workflow <a name="git-workflow"></a>

```flow

      KATALOG_ROBOCZY --             
                        |
                        git add --    
                                  |
                                  STAGING AREA --
                                                 |             
                                                 git commit --
		   	    		   		                              |
		   	    		   	                                  (local) REPO --
 								                                             |
 								                                             git push --
 									                                                    |
 									                                                    GITHUB/GITLAB ETC.
```

Opis git worfklow:
1. <b>git add</b> - przenosi plik do staging area.
2. <b>staging area</b> - to swego rodzaju poczekalnia, w której znajdują się pliki gotowe do commita.
   * jeśli jednak uznam, że nie chcę robić commita pliku to mogę wyciągnąć plik ze staging area.
3. <b>git commit</b> - zapisuje zmiany z staging area na stałe w historii lokalnego repozytorium.
   * tworzy trwały punkt kontrolny (migawkę/snapshot) w lokalnej historii projektu. 


<hr style="border:2px solid gray">

## Untracked files <a name="untracked-files"></a>

- Wpisując polecenie <em>git status</em> wewnątrz repo można znaleźć "untracked files".
- Git nie śledzi zmian w takich plikach.
- Polecenie <em>git add</em> zmienia status takich plików na "tracked".


<hr style="border:2px solid gray">

## git add <a name="git-add"></a>

- Przeniesienie przykładowego pliku <em>fileone.txt</em> do Staging Area:

```shell
	git add fileone.txt
	git status
```
- Co zwróci polecenie <em>git status</em>?
  * Informacja, że znaduję się w staging area.
  * <em>Changes to be commited.</em>
 
- Dodanie całej zawartości katalogu roboczego do Staging Area:

```shell
	git add .
```

<hr style="border:2px solid gray">

## git commit <a name="git-commit"></a>

- Commit:
  	* Jest to swego rodzaju "check point" (snapshot/migawka) za pomocą którego zapisuę plik/pliki w danym stanie/danej wersji.
  	* Każdy commit ma unikalny id.
  	* Zasadniczo każdy commit jest powiązany z poprzednim (mechanizm śledzenia "tracking") - za wyjątkiem pierwszego commit-a.
  	* Powiązanie commit-ów umożliwia sprawdzenie co się zmieniło w czasie pomiędzy poszczególnymi commit-ami.

- Jak powiązane są commit-y?
	* 1 commit (hash, parent = null, info) <- 2 commit (hash, parent= 1 commit, info) <- 3 commit (hash, parent= 3 commit, info).
	* Hash kolejnego commit-a jest generowany na podstawie m.in.: hash-a poprzedniego commita (lub brak w przypadku pierwszego commita),
	wiadomość commit-a, danych o autorze (imię/nazwa, e-mail).
	* Hash jest to ciąg 40 znaków w systemie szesnastkowym (<em>heksadecymalny, HEX - do zapisu liczb używa się 16 symboli: cyfr 0–9 oraz pierwszych liter alfabetu A–F, które zastępują wartości od 10 do 15</em>).
	* Zmiana choćby jednej litery w commit message zmienia w wartość hash-a.

- Standardowe użycie polecenia git commit

  ```shell
  	git commit -m "lorem ipsum"
  ```

	* Plik zostaje zapisany w historii repozytorium (niektórzy mówią, że zostaje przeniesiony do przestrzenii repozytorium).
 	* Wykonując polecenie <em>git status</em> nie zobaczę już tego pliku ponieważ nie jest już w staging area.
 	* Dobrą praktyką są jednoznaczne wiadomości podawane po parametrze <em>-m</em>


- Otwarcie domyślnego edytora tekstowego:

 ```shell
	git commit BEZ MESSAGE
```

<hr style="border:2px solid gray">

## Atomic commits <a name="atomic-commits"></a>

- Jeden commit = jeden task/feature/component/fix ("<em>one thing at a time</em>").
- Tytuł commita powinien być krótki i jednoznaczny.
- Zaleca się aby tytuł commita składał się z 50–75 znaków.
- Tytuł commita powinien być pisany w tryb rozkazującym: „Add…”, „Fix…”, „Update…”, „Refactor…”, „Remove…”.
- Często nie stawia się kropki na końcu tytułu commita.
- <em>Body commita</em> pisze się, gdy commit wymaga kontekstu.
- Zalecenia dotyczące zawartości (<em>body</em>) commita:
  	+ pusta linia odstępu pomiędzy tytułem a body,
  	+ napisz dlaczego dokonujesz danego commita,
  	+ napisz co dany commit wnosi,
  	+ ewentualnie napisz co należy przetestować


<hr style="border:2px solid gray">

## git log <a name="git-log"></a>

1. Standardowe użycie polecenia:
   ```shell
   		git log
   ```

	+ Wyświetlone zostają następujące informacje:

		* Historia/lista commitów, które zostały wykonane do repo.
		* Commit hash (ID).
	  	* Autor commit-a.
		* Data commit-a.
		* Commit message.

2. Wyświetl 5 ostatnich commitów:
   ```shell
   		git log -n 5
   ```

3. Wyświetl tylko ID oraz tytuły commitów:
   ```shell
   		git log --oneline
   ```
<em>Przykład:</em>

```shell
lkldz@fedora:~/training_material/git_file$ git log --oneline
66247e0 (HEAD -> master, summer_branch) Modify bla and sunny files.
048895b Merge branch 'sunny_branch'
3fefe9c (sunny_branch) Edited sunny file. Added info about pies.
1af60c1 Edited: sunny file. Added info about kot.
e4231cb Merge branch 'sunny_branch'
4c2d1e6 Added test2 file.
00af6c4 Added sad file.
f1feafe Added funny file.
649c8cc Added placeholder in sunny file.
9436a5f Added sunny file.
feaaee5 (olive_branch) Add pending file and bla_file.txt
4ca14eb Added training files.
lukasz@fedora:~/TEST_AUTOMATION/gitone
```

4. Wyświetl w terminalu wizualizację historii commitów:
   
   ```shell
   git log --graph --decorate --all
   ```
<em>Przykład:</em>

```shell
* commit b569b889088afd5f24cea6b79a47b03639e53429
| Author: lkldz <lkldz@bleble.com>
| Date:   Mon Jan 26 06:05:54 2026 +0100
| 
|     Update git training materials
| 
* commit 2f52cd3f4243928e862d68f3c987f9abc1cd3946
| Author: lkldz <lkldz@bleble.com>
| Date:   Mon Jan 26 05:49:44 2026 +0100
| 
|     Add git training materials
|
```


<hr style="border:2px solid gray">

## git config <a name="git-config"></a>

1. Ustawienia globalne:
   
   ```shell
   	 git config --global ...
   ```
   - Zapisuje ustawienie dla danego użytkownika komputera.
   - Działa we wszystkich repozytoriach na danym komputerze.
   - Ustawiania globalne mogą zostać nadpisane przez lokalne.

2. Ustawienia lokalne:
   
   ```shell
   		git config --local ...
   ```
	- Zapisuje ustawienie tylko dla bieżącego repozytorium.
	- Działa tylko w ramach danego katalogu/foldera (repo).
 	- Nadpisuje ustawienia globalne dla danego repo.

3. Konfigurowanie nazwy oraz maila użytkownia git-a:
   
   ```shell
   git config --global user.name "Mona Lisa"
   git config --global user.email "mona.lisa@luvr.com"
   
   git config --local user.email "mona.lisa@paintings.com"
   ```
   
4. Konfigurowanie domyślnego edytora tekstowego:
   
   ```shell
   	git config --global core.editor "vi"
   ```

5. Wyświetlenie konfiguracji git-a:
   
   ```shell
   git config --list
   ```
<em>Przykład:</em>

```shell
lkldz@fedora:~/training_material/git_file$ git config --list
user.name=lkldz
user.email=lkldz@bleble.com
core.editor=vi
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
```

6. Plik <em>.gitconfig</em>
- Przechowuje informacje o konfiguracji git-a na danym komputerze.
- Znajduje się w katalogu "<em>home</em>".
- Katalog domowy na Linux: <em>/home/nazwa_uzytkownika</em>
- Katalog domowy na Windows: <em>C:\Users\NazwaUzytkownika</em>

<em>Przykład:</em>
```shell
lkldz@fedora:~# cat ~/.gitconfig
[user]
	name = lkldz
	email = lkldz@bleble.com
[core]
	editor = vi
```


<hr style="border:2px solid gray">

## .gitignore <a name="gitignore"></a>

1. Wprowadzenie:
- Tworzenie pliku .gitignore
```shell
touch .gitignore
```

- Jest to plik tekstowy w repozytorium Git-a.
- Informuje Git, które pliki lub katalogi mają być pomijane podczas śledzenia zmian.
- Pliki dopasowane do reguł w .gitignore nie pojawią się w git status i nie zostaną dodane do historii projektu.
- Plik .gitignore ignoruje wyłącznie pliki nieśledzone (untracked).
- Jeśli plik został już wcześniej dodany do Git-a i zatwierdzony (committed), dopisanie go do .gitignore nie sprawi, że przestanie być śledzony.
- Aby Git przestał śledzić plik bez usuwania go z dysku, należy wydać polecenie:
```shell
	git rm --cached nazwa_pliku
```
- .gitignore zapobiega przypadkowemu wysłaniu na serwer haseł, tokenów API czy plików konfiguracyjnych.

2. .gitignore - wzorce używane w pliku:
- Ignoruj wszystkie pliki z rozszerzeniem .log w całym projekcie:
```text
*.log
```
- Ignoruj katalog build wraz ze wszystkimi plikami i podfolderami:
```text
build/
```
- Ignoruj konkretny plik o nazwie config.json:
```text
config.json
```
- Ignoruj pliki .txt bezpośrednio w folderze docs (ale nie w podfolderach):
```text
docs/*.txt
```
- Dodaj wyjątek: śledź plik important.log, nawet jeśli *.log jest ignorowane:
```text
!important.log
```
- Linie zaczynające się od # traktuj jako komentarze:
```text
# komentarz
```
3. Generatory pliku .gitignore:
- Program, który tworzy szablon pliku .gitignore który może zostać użyty w ramach projektu w danej technologii.
- Dostępne w Internecie.


<hr style="border:2px solid gray">

## Branch <a name="branch"></a>

1. Wprowadzenie
	- Branch to swego rodzaju "alternatywna oś czasu".
	- Przykładowy schemat:
```shell  
  m
  |
  o
  |
  o
 /|\
| o o
o | |
| o o
o |
| o
o |
| o
 
m = master
```
2. Wyświetlenie, na której branchy jestem aktualnie:

```shell
	git branch
```

<em>Przykład:</em>

```shell
lkldz@fedora:~/training_material/git_file$ git branch
* master
```

3. Tworzenie nowej branch-y:

```shell
	git branch nazwa_nowe_branchy
```

<em>Przykład:</em>

```shell
lkldz@fedora:~/training_material/git_file$ git branch new_test_branch
lkldz@fedora:~/training_material/git_file$ git branch
* master
  new_test_branch
```

4. Przełączenie na nowy branch:

```shell
	git checkout nazwa_branchy
```

<em>Przykład:</em>

```shell
lkldz@fedora:~/training_material/git_file$ git checkout new_test_branch
Switched to branch 'new_test_branch'
lkldz@fedora:~/training_material/git_file$ git branch
  master
* new_test_branch

lkldz@fedora:~/training_material/git_file$ git status
On branch new_test_branch
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.gitignore
	index.html

nothing added to commit but untracked files present (use "git add" to track)

```

5. Alternatywne polecenie do przełączania pomiędzy branch-ami:
```shell
	git switch nazwa_branchy
```

<em>Przykład:</em>
```shell
lkldz@fedora:~/training_material/git_file$ git switch master
Switched to branch 'master'
lkldz@fedora:~/training_material/git_file$ git branch
* master
  new_test_branch
```

## HEAD <a name="head"></a>
