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

[Wycofanie pliku ze staging](#remove-from-staging)

[git commit](#git-commit)

[Atomic commits](#atomic-commits)

[git log](#git-log)

[git config](#git-config)

[.gitignore](#gitignore)

[Branch](#branch)

[HEAD](#head)

[Fast-forward merge](#fforward-merge)

[Not fast-forward merge](#not-fforward-merge)

[Rozwiązywanie konfliktów](#conflicts)

[Cherry pick](#cherry-pick)

[git stash](#git-stash)

[Detached HEAD](#detached-head)

[Cofanie zmian](#cofanie-zmian)

[Rebase](#rebase)

[Interaktywny rebase](#interactive-rebase)

[Standard rebase](#standard-rebase)

[Cofnięcie rebase](#cofniecie-rebase)

[git amend](#git-amend)

[git fetch vs git pull](#fetch-pull)


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

## Wycofanie pliku ze staging area. <a name="remove-from-staging"></a>

Polecenie
```shell
git restore --staged nazwa_pliku
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

<em>Przykład 2:</em>
```shell
lkldz@fedora:~/training_material/git_file$ git log --oneline --graph --all
* 66247e0 (HEAD -> master) Modify bla and sunny files.
*   048895b Merge branch 'sunny_branch'
|\  
| * 3fefe9c (sunny_branch) Edited sunny file. Added info about pies.
* | 1af60c1 Edited: sunny file. Added info about kot.
* | e4231cb Merge branch 'sunny_branch'
|\| 
| * 00af6c4 Added sad file.
| * f1feafe Added funny file.
* | 4c2d1e6 Added test2 file.
|/  
* 649c8cc Added placeholder in sunny file.
* 9436a5f Added sunny file.
* feaaee5 (olive_branch) Add pending file and bla_file.txt
| * 8fa1de1 (new_test_branch) Added new text file
|/  
* 4ca14eb Added training files.
lkldz@fedora:~/training_material/git_file$
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

1. <b>Wprowadzenie</b>
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
2. <b>Wyświetlenie, na której branchy jestem aktualnie:</b>

```shell
	git branch
```

<em>Przykład:</em>

```shell
lkldz@fedora:~/training_material/git_file$ git branch
* master
```

3. <b>Tworzenie nowej branch-y:</b>

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

4. <b>Przełączenie na nowy branch:</b>

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

5. <b>Alternatywne polecenie do przełączania pomiędzy branch-ami:</b>
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

6. <b>Utwórz branch i od razu przełącz się na niego/nią:</b>
```shell
	git checkout -b nazwa_branchy
```

<ins>Alternatywne polecenie:</ins>
```shell
	git switch -c nazwa_branchy
```

<em>Przykład:</em>

```shell
lkldz@fedora:~/training_material/git_file$ git checkout -b olive_branch
Switched to a new branch 'olive_branch'
lkldz@fedora:~/TEST_AUTOMATION/gitone$ git branch
  master
  new_test_branch
* olive_branch

lkldz@fedora:~/training_material/git_file$ git switch -c sunny_branch
Switched to a new branch 'sunny_branch'
lkldz@fedora:~/training_material/git_file$ git branch
  master
  new_test_branch
  olive_branch
* sunny_branch
```

7.<b><ins>Jak zmienić nazwę branch-a:</ins></b>

- Sposób zmiany nazwy gałęzi (brancha) zależy od tego, czy zmiana dotyczy tylko localhosta,<br>
  czy gałąź została już wysłana na serwer (np. GitHub/GitLab).

<ins><b>A. Zmiana nazwy lokalnego brancha.</b></ins>

<b>Opcja pierwsza </b>: Jesteś aktualnie na tym branchu

```shell
git branch -m nowa-nazwa-brancha
```

<b>Opcja druga</b>: Jesteś na innym branchu (np. na master)

```shell
git branch -m stara-nazwa nowa-nazwa
```

<ins><b>B. Zmiana nazwy brancha wysłanego na serwer (GitHub / GitLab).</b></ins>

Jeśli branch istnieje już na zdalnym repozytorium, musisz wykonać 3 kroki:<br> 

- zmienić nazwę lokalnie,
- wypchnąć nową gałąź
- usunąć starą z serwera.
Zmień nazwę brancha lokalnie

Krok 1. Będąc na gałęzi ze starą nazwą:
```shell
git branch -m nowa-nazwa-brancha
```

Krok 2. Wypchnij nową gałąź i ustaw śledzenie (upstream):
```shell
git push -u origin nowa-nazwa-brancha
```

Krok 3. Usuń starą gałąź ze zdalnego serwera:
```shell
git push origin --delete stara-nazwa-brancha
```

<b>Ważne</b>
Jeśli inna osoba w zespole miała pobraną starą gałąź,<br> 
może zaktualizować swoje lokalne repo (referencje do starej nazwy gałęzi) poleceniem:
```shell
git fetch --prune
```

<ins>Polecenie <b>git fetch --prune</b> (lub skrót git fetch -p)</ins> 

```shell
git fetch --prune
```

- Służy do posprzątania/zaktualizowania lokalnych referencji do zdalnych gałęzi (remote tracking branches),<br> 
które zostały już usunięte na serwerze (np. na GitHubie czy GitLabie).

- Kiedy ktoś z zespołu (lub Ty po zmergowaniu Pull Requesta) usunie gałąź na serwerze zdalnym, Twój lokalny Git o tym nie wie.<br>
Zwykłe polecenie git fetch pobiera nowe commity i nowe gałęzie, ale nie usuwa starych wskaźników.<br>
W efekcie, gdy wpiszesz git branch -r lub git branch -a, nadal widzisz "gałęzie-widma" typu origin/stara-funkcja, mimo że na serwerze one już nie istnieją.

- Polecenie git fetch --prune sprawdza zdalne repozytorium i kasuje lokalne wskaźniki origin/... dla gałęzi, których już tam nie ma.



<hr style="border:2px solid gray">

## HEAD <a name="head"></a>

- HEAD to główny wskaźnik Git-a określający, na jakim commicie lub gałęzi aktualnie pracujesz.

<em>Przykład:</em>
HEAD -> master

```shell
lkldz@fedora:~/training_material/git_file$ git log
commit 4ca14eb01dfb5f9933d963e35ca9bd96d3e9d1ef (HEAD -> master)
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 12:08:44 2026 +0200

    Add training files.
```

1. <ins>Przypadek:</ins> HEAD -> new_test_branch, master

```shell
gitone$ git log
commit 4ca14eb01dfb5f9933d963e35ca9bd96d3e9d1ef (HEAD -> new_test_branch, master)
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 12:08:44 2026 +0200

    Add training files.
```
- Zapis ten oznacza, że znajdujemy się obecnie na gałęzi <em>new_test_branch</em>, a gałąź <em>master</em>
  znajduje się dokładnie w tym samym miejscu (wskazuje na ten sam commit) w historii projektu.
- <em>-> new_test_branch</em>  strzałka oznacza, że HEAD jest przypięty do gałęzi <em>new_test_branch</em> (czyli jest to aktywna gałąź).
- <em>, master</em> – przecinek i druga nazwa oznaczają, że gałąź <em>master</em> wskazuje na ten sam commit co <em>new_test_branch</em>.
- Taki zapis (ten przypadek) oznacza, że dopiero co utworzono gałąź <em>new_test_branch</em> z poziomu <em>master</em> (lub przełączono się
	na nią) i nie zrobiono jeszcze na niej żadnego nowego commita.
- Wskaźniki HEAD oraz <em>new_test_branch</em> przesuną się do przodu na nowy commit.
- Gałąź <em>master</em> zostanie na dotychczasowym commicie (zostanie w tyle).

2. <ins>Przypadek:</ins> Dodano nowy commit do branchy testowej <em>new_test_branch</em>

```shell
lkldz@fedora:~/training_material/git_file$ git log
commit 8fa1de1ef18db10f204c88248538aafa1937fc18 (HEAD -> new_test_branch)
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 14:31:51 2026 +0200

    Add new text file

commit 4ca14eb01dfb5f9933d963e35ca9bd96d3e9d1ef (master)
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 12:08:44 2026 +0200

    Add training files

```


<hr style="border:2px solid gray">

## Fast-forward merge <a name="fforward-merge"></a>
- To najprostszy sposób łączenia gałęzi w Git.
- Występuje wtedy, gdy na gałęzi docelowej (np. master) nie powstały żadne nowe commit-y od momentu utworzenia gałęzi scalanej (np. feature branch).
- W takiej sytuacji Git nie tworzy nowego "commita scalającego" (merge commit), lecz po prostu przesuwa wskaźnik gałęzi docelowej na ostatni commit scalanej gałęzi.
- W przypadku merge do master/main najpierw przełącz na master/main (<em>git switch master</em>)
```shell
  git switch master --> git merge feature_branch
```

<ins>Wizualizacja:</ins>

1. Stan przed scaleniem:</em>
Gałąź feature wyszła z commita B. Od tamtej pory na main nie dodano żadnych nowych zmian.

```text	
	master:    A --- B
    	              \
	feature:           C --- D (HEAD)
```

2. Po wykonaniu git merge feature (fast-forward):
- Wskaźnik main zostaje po prostu przesunięty do przodu na commit D.

```text
master / feature: A --- B --- C --- D (HEAD)
```

<ins>Przykład z opisem:</ins>
```shell
lkldz@fedora:~/training_material/git_file$ git log --oneline
936175a (HEAD -> issue_fix) Add full content for test 2 file.
6855718 (master) Add test 2 file content.
d32a813 Add new test 3 file.

lkldz@fedora:~/training_material/git_file$ git checkout master
Switched to branch 'master'
lkldz@fedora:~/training_material/git_file$ git merge --ff-only issue_fix
Updating 6855718..936175a
Fast-forward
 test2_file.txt | 3 ++-
 testone.txt    | 1 +
 2 files changed, 3 insertions(+), 1 deletion(-)

lkldz@fedora:~/training_material/git_file$ git log --oneline
936175a (HEAD -> master, issue_fix) Add full content for test 2 file.
6855718 Add test 2 file content.
d32a813 Add new test 3 file.
0c94e4c New text to sad file
fc9efc1 Add text to sad file.
```

1. Branch <em>issue_fix</em> był bezpośrednio o jeden commit przed <em>master</em> (jest liniową kontynuacją),
   więc wystarczyło wykonać standardowe scalenie w trybie <em>fast-forward.</em>
2. W trybie <em>fast-forward</em> git nie tworzy żadnego nowego commita scalającego (merge commit),
   a jedynie przesuwa wskaźnik <em>master-a</em> do przodu na commit 936175a.
3. Polecenie:
```shell 
	git merge --ff-only
``` 
- Jest to swego rodzaju bezpiecznik.
- Jeśli nie da się zrobić fast-forward, git odmówi wykonania operacji i wyświetli błąd,
  dzięki czemu masz 100% pewności, że w historii nie pojawi się żaden commit scalający.


<hr style="border:2px solid gray">

## Not fast-forward merge <a name="not-fforward-merge"></a>
- To operacja scalania w Git, w wyniku której zawsze powstaje nowy commit scalający (tzw. <em>merge commit</em>).
- <em>Merge commit</em> ma dwóch rodziców (dwie gałęzie) i oficjalnie wiąże historię obu gałęzi.
- Not fast-forward merge występuje w dwóch typach (formach):
  	+ <em>Automatycznie:</em> gdy na <em>gałęzi docelowej</em> (np. <em>master</em>) powstały nowe commit-y od momentu utworzenia
  	  gałęzi scalanej (feature branch).
  	+ <em>Wymuszenie (--no-ff):</em> gdy zlecam Git-owi utworzenie commita scalającego, mimo że możliwy byłby zwykły fast-forward.

<ins>Wizualizacja:</ins>

1. <ins>Automatyczny not fast-forward merge:</ins><br>
Na <em>master</em> dodano commit E, a na <em>feature</em> commit-y C i D.<br>
Fast-forward jest niemożliwy, więc Git musi połączyć zmiany w nowym commicie M.
```shell
	git merge feature_branch
```
```text
master:    A --- B --- E ----------- M (Merge commit)
               	 \                 /
feature:          C --- D ────────┘
```	

<ins>Wizualizacja:</ins>

2. <ins>Wymuszony not fast-forward merge:</ins><br>
Nawet jeśli na <em>master</em> nie ma nowych zmian (możliwy byłby fast-forward),<br>
flaga <em>--no-ff</em> tworzy odgałęzienie i <em>commit scalający M</em>:
```shell
	git merge --no-ff feature_branch
```
```text
master:    A --- B ----------------- M (Merge commit)
               	 \                 /
feature:          C --- D ────────┘
```
Zalety wymuszonego not-fast-forward merge:
+ Czytelna dokumentacja nowej funkcjonalności tworzonej na feature branch:<br> 
	Graf historii (<em>git log --graph</em>) wyraźnie grupuje commity C i D jako jedną osobną funkcję/zadanie.<br>
	
+ Proste cofanie zmian (Revert):<br> 
	
	```shell
	git revert -m 1 <hash_M>
	```
	+ Jeśli nowa funkcja okaże się wadliwa, wystarczy cofnąć jeden commit scalający (git revert -m 1 <hash_M>), aby usunąć całą funkcję z main.<br> 
	W przypadku fast-forward trzeba by odkręcać każdy commit osobno.<br>
+ Współpraca w zespole:<br> 
	Pozwala zachować ślad, kiedy dana gałąź została dołączona do głównego kodu.

<ins>Przypadek:</ins> Na feature branch dodałem nowe pliki a po ich utworzeniu na master pojawił się nowy commit.

```shell
lkldz@fedora:~/training_material/git_file$ git log
commit e4231cb2bc453f3bfa9afe06e275e95234c58262 (HEAD -> master)
Merge: 4c2d1e6 00af6c4
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 15:15:40 2026 +0200

    Merge branch 'sunny_branch'

commit 4c2d1e6120bf4c783356c0c69180cef47bf677aa
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 15:15:12 2026 +0200

    Add test2 file.

commit 00af6c464329e14a2c3b4e3cb8dbe390300f8501 (sunny_branch)
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 15:14:36 2026 +0200

    Add sad file.

commit f1feafe7328c57d10632b959c476c764206c952b
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 15:14:11 2026 +0200

    Add funny file.
```


<hr style="border:2px solid gray">

## Rozwiązywanie konfliktów <a name="conflicts"></a>

- Jak wygląda konflikt?

```text
<<<<<<<<<<< HEAD
	line 1
	line 2       <- to jest branch na którym jestem i wykonuję merge (najczęściej master/main)
	line 3
===============
	line 4       <- to linie powodujące konflikt. Linie te występuję na innej branchy 
	line 5
```

- Jak rozwiązać konflikt?
1. Usuń linie których nie chcesz zachować.
2. Popraw błędy.
3. Usuń <<<<<<< oraz ======
4. Zapisz.

- Przykład konfliktu:
```shell
lkldz@fedora:~/training_material/git_file$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   sunny_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

lkldz@fedora:~/training_material/git_file$ cat sunny_file.txt 
Ala ma kota.
Kot ma Alę.

lkldz@fedora:~/training_material/git_file$ git add .

lkldz@fedora:~/training_material/git_file$ git commit -m "Edited: sunny file. Added info about kot."
[master 1af60c1] Edited: sunny file. Added info about kot.
 1 file changed, 1 insertion(+)

lkldz@fedora:~/training_material/git_file$ git switch sunny_branch 
Switched to branch 'sunny_branch'

lkldz@fedora:~/training_material/git_file$ vi sunny_file.txt 

lkldz@fedora:~/training_material/git_file$ git status
On branch sunny_branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   sunny_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

lkldz@fedora:~/training_material/git_file$ cat sunny_file.txt 
Ala ma kota.
Ala ma też psa.

lkldz@fedora:~/training_material/git_file$ git add .

lkldz@fedora:~/training_material/git_file$ git commit -m "Edited sunny file. Added info about pies."
[sunny_branch 3fefe9c] Edited sunny file. Added info about pies.
 1 file changed, 1 insertion(+)

lkldz@fedora:~/training_material/git_file$ git switch master 
Switched to branch 'master'

lkldz@fedora:~/training_material/git_file$ git branch

* master
  new_test_branch
  olive_branch
  sunny_branch

lkldz@fedora:~/training_material/git_file$ git merge sunny_branch 
Auto-merging sunny_file.txt
CONFLICT (content): Merge conflict in sunny_file.txt
Automatic merge failed; fix conflicts and then commit the result.

lkldz@fedora:~/training_material/git_file$ cat sunny_file.txt 
Ala ma kota.
<<<<<<< HEAD  <-- Tzw. current change (najczęściej master/main)
Kot ma Alę.
=======
Ala ma też psa.  <--- tzw. incoming change (feature branch)
>>>>>>> sunny_branch

lkldz@fedora:~/training_material/git_file$ vi sunny_file.txt

lkldz@fedora:~/training_material/git_file$ cat sunny_file.txt 
Ala ma kota.
Kot ma Alę.
Ala ma też psa.

lkldz@fedora:~/training_material/git_file$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   sunny_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

lkldz@fedora:~/training_material/git_file$ git add sunny_file.txt 

lkldz@fedora:~/training_material/git_file$ git commit
[master 048895b] Merge branch 'sunny_branch'

lkldz@fedora:~/training_material/git_file$ git log
commit 048895bf6acf5dc6b30b4aec46528163472e99d7 (HEAD -> master)
Merge: 1af60c1 3fefe9c
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 16:39:58 2026 +0200

    Merge branch 'sunny_branch'

commit 3fefe9cf50d3af1f854e4919de6880201f32dee7 (sunny_branch)
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 15:56:44 2026 +0200

    Edited sunny file. Added info about pies.

commit 1af60c1b020ab0b01840ae25c4f256d66cd37b41
Author: lkldz <lkldz@bleble.com>
Date:   Mon Aug 17 15:54:45 2026 +0200

    Edited: sunny file. Added info about kot.
```


<hr style="border:2px solid gray">

## Cherry pick <a name="cherry-pick"></a>

- Cherry-pick to polecenie, które pozwala wybrać jeden konkretny commit z dowolnej gałęzi i zaaplikować zawarte w nim zmiany na aktualną gałąź.

- Kiedy używać cherry-pick?

  + Szybka poprawka błędu (tzw. hotfix):<br>
    naprawiono krytyczny błąd na długiej gałęzi rozwijanej funkcji (feature branch),<br>
    ale poprawka musi trafić na produkcję (master) natychmiast, bez niegotowej reszty kodu.
  
  + Commit na złej gałęzi:<br>
    zrobiono commit na gałęzi master zamiast feature-branch.<br>
    Należy zrobić cherry-pick na właściwej gałęzi, a z master usunąć niechciany commit.
  
  + Wyciąganie przydatnych zmian:<br>
    inny programista napisał na swojej gałęzi gotowy moduł, który jest nam potrzebny do dokończenia zadania.

<ins>Polecenie:</ins>
```shell
git cherry-pick <hash_commita>
```
<ins>Wizualizacja:</ins><br>
Stan początkowy:
```text

master:    A --- B (HEAD)
                
feature: C --- D --- E (chcę przenieść tylko commit D)
```
Po wykonaniu <em>git cherry-pick <hash_commita_D></em>
```text
master:    A --- B --- D' (HEAD)
                
feature: C --- D --- E
```

<ins>Cherry-pick krok po kroku:</ins>
1. Znajdź hash commita: Przejdź na gałąź źródłową i skopiuj hash potrzebnego commita:<br>
    <em>git log --oneline</em><br>
    Przykład wyniku: a1b2c3d feat: dodano walidację emaila<br>

2. Przełącz się na gałąź docelową:<br>
   <em>git switch main</em><br>

3. Uruchom cherry-pick:<br>
    <em>git cherry-pick a1b2c3d</em><br>

4. Jeśli przenoszony commit zmienia te same linie co kod na gałęzi docelowej, nastąpi konflikt.
5. Rozwiąż konflikty w plikach i dodaj je do staging area:<br>
   <em>git add .</em><br>
7. Kontynuuj operację:<br>
   <em>git cherry-pick --continue</em></br>
9. (Opcjonalnie) Jeśli chcesz całkowicie wycofać się z operacji:<br>
    <em>git cherry-pick --abort</em><br>


<hr style="border:2px solid gray">

## git diff <a name="git-diff"></a>

- Pokazuje różnice pomiędzy dwiema wersjami tego samego pliku.

- Jak czytać output git diff-a?
``` text
a -> file 1 & b -> file 1 (inna wersja tego samego pliku)
--- file 1   <- "myślniki" będą wskazywać na treść file 1
+++ file 2 <- "plusy" będą wskazywać na treść file 2
```

<ins>Przykład:</ins><br>
```shell
lkldz@fedora:~/training_material/git_file$  git diff --staged
diff --git a/bla_file.txt b/bla_file.txt
index e69de29..353adb7 100644
--- a/bla_file.txt
+++ b/bla_file.txt
@@ -0,0 +1 @@
+New text was added.
```
1. <em>git diff --staged</em><br>
   polecenie sprawdzające różnice między stanem przygotowanym do commita (staging area / index) a ostatnim zatwierdzonym commitem.<br>
2. <em>diff --git a/bla_file.txt b/bla_file.txt</em><br>
   git porównuje stary stan pliku (a/) z nowym stanem (b/).<br>
3. <em>index e69de29..353adb7 100644</em><br>
	wewnętrzne hasze obiektów Gita.<br>
4. <em>--- a/bla_file.txt oraz +++ b/bla_file.txt</em><br>
   oznaczenie symboli: - dla starej wersji, + dla nowej.<br>
6. <em>@@ -0,0 +1 @@:</em><br>
   -0,0: w starej wersji plik był pusty (0 linii od linii 0).<br>
    +1: w nowej wersji pojawia się 1 linia tekstu od linii 1.<br>
   +New text was added. — faktyczna zmiana: do pliku dopisano linijkę New text was added..

<ins>Przykład 2:</ins><br>
```shell
diff --git a/sunny_file.txt b/sunny_file.txt
index 84f4ee3..bd04e4a 100644
--- a/sunny_file.txt
+++ b/sunny_file.txt
@@ -1,3 +1,4 @@
 Ala ma kota.
-Kot ma Alę.
-Ala ma też psa.
+Kot ma Alę!
+A poza tym:
+Ala ma też psa...
```
1. <em>Ala ma kota. (linijka bez znaku + ani -):</em><br>
   linia bez zmian – stanowi kontekst dla Gita.
2. <em>@@ -1,3 +1,4 @@</em>:
   * -1,3 — w starej wersji ten fragment zaczynał się od 1. linii i liczył 3 linie;
   * +1,4 — w nowej wersji ten fragment zaczyna się od 1. linii i po zmianach liczy 4 linie


- Porównianie dwóch commit-ów:<br>
	+ Polecenie:
```shell
 git diff hash_commit1...hash_commit2
```
<ins>Przykład 3:</ins><br>
```shell
lkldz@fedora:~/training_material/git_file$ git log --oneline
66247e0 (HEAD -> master) Modify bla and sunny files.
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

lkldz@fedora:~/training_material/git_file$ git diff 1af60c1...66247e0
diff --git a/bla_file.txt b/bla_file.txt
index e69de29..353adb7 100644
--- a/bla_file.txt
+++ b/bla_file.txt
@@ -0,0 +1 @@
+New text was added.
diff --git a/sunny_file.txt b/sunny_file.txt
index 5d49bff..bd04e4a 100644
--- a/sunny_file.txt
+++ b/sunny_file.txt
@@ -1,2 +1,4 @@
 Ala ma kota.
-Kot ma Alę.
+Kot ma Alę!
+A poza tym:
+Ala ma też psa...
lkldz@fedora:~/training_material/git_file$
```

- Porównianie dwóch branch-y:<br>
	+ Polecenie:
```shell
 git diff branch1_nazwa...branch2_nazwa
```
<ins>Przykład 3:</ins><br>
```shell
lkldz@fedora:~/training_material/git_file$ git branch
* master
  new_test_branch
  olive_branch
  sunny_branch

lkldz@fedora:~/training_material/git_file$ git diff new_test_branch...master 
diff --git a/.gitignore b/.gitignore
new file mode 100644
index 0000000..e69de29
diff --git a/bla_file.txt b/bla_file.txt
new file mode 100644
index 0000000..353adb7
--- /dev/null
+++ b/bla_file.txt
@@ -0,0 +1 @@
+New text was added.
diff --git a/funny_file.txt b/funny_file.txt
new file mode 100644
index 0000000..e69de29
diff --git a/index.html b/index.html
new file mode 100644
index 0000000..e69de29
diff --git a/sad_file.txt b/sad_file.txt
new file mode 100644
index 0000000..e69de29
diff --git a/sunny_file.txt b/sunny_file.txt
new file mode 100644
index 0000000..bd04e4a
--- /dev/null
+++ b/sunny_file.txt
@@ -0,0 +1,4 @@
+Ala ma kota.
+Kot ma Alę!
+A poza tym:
+Ala ma też psa...
diff --git a/test2_file.txt b/test2_file.txt
new file mode 100644
index 0000000..e69de29
lkldz@fedora:~/training_material/git_file$
```
1. <em>new file mode 100644</em><br>
plik wcześniej w ogóle nie istniał w punkcie rozgałęzienia.<br>
2. <em>--- /dev/null</em><br>
   w starej wersji źródło było puste (plik nie istniał).


<hr style="border:2px solid gray">

## git stash <a name="git-stash"></a>

- Stash jest to schowek na pliki nad którymi pracuję ale muszę odłożyć je na chwilę na bok aby zająć się czymś innym.
- Pozwala tymczasowo zdjąć wszystkie niezacommitowane zmiany z katalogu roboczego (zarówno ze strefy staged, jak i unstaged), zapisać je na specjalnym stosie i przywrócić projekt do stanu czystego (z ostatniego commita).
- Po użyciu stasha mogę przepiąć się na inny branch (bo np. ktoś mnie poprosił o szybką zmianę na innej branchy).
- <em>git stash</em> działa jak stos (LIFO – Last In, First Out) – można chować kolejne zestawy zmian,
  a najnowszy zawsze ląduje na samej górze z indeksem stash@{0}.

<ins>Zastosowanie:</ins>
+ Hotfix: pracuję nad nową funkcją i masz rozgrzebany kod (który jeszcze się nie kompiluje/nie działa),<br>
  ale muszę natychmiast przełączyć się na gałąź main/hotfix, by naprawić pilnego buga.<br>

+ Zmiana gałęzi bez robienia śmieciowego commita.<br>
  Tzn. git często blokuje <em>git checkout</em>/<em>git switch</em>, jeśli mam lokalne modyfikacje w tych samych plikach.<br>

+ Aktualizacja gałęzi (<em>git pull</em>):<br>
  tj. chcę pobrać najnowsze zmiany ze zdalnego repozytorium na czysty stan roboczy, a dopiero potem nałożyć swoje poprawki.<br>

<ins>Przykład:</ins><br>
```shell
lkldz@fedora:~/training_material/git_file$ git branch
* master
  new_test_branch
  olive_branch
  sunny_branch

lkldz@fedora:~/training_material/git_file$ git checkout -b summer_branch
Switched to a new branch 'summer_branch'

lkldz@fedora:~/training_material/git_file$ git branch
  master
  new_test_branch
  olive_branch
* summer_branch
  sunny_branch

lkldz@fedora:~/training_material/git_file$ ls
bla_file.txt  funny_file.txt  index.html  sad_file.txt  sunny_file.txt  test2_file.txt  testone.txt  testtwo.txt

lkldz@fedora:~/training_material/git_file$ vi bla_file.txt 

lkldz@fedora:~/training_material/git_file$ git status
On branch summer_branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   bla_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

lkldz@fedora:~/training_material/git_file$ git switch olive_branch 
error: Your local changes to the following files would be overwritten by checkout:
	bla_file.txt
Please commit your changes or stash them before you switch branches.
Aborting

lkldz@fedora:~/training_material/git_file$ git checkout olive_branch 
error: Your local changes to the following files would be overwritten by checkout:
	bla_file.txt
Please commit your changes or stash them before you switch branches.

lkldz@fedora:~/training_material/git_file$ git stash
Saved working directory and index state WIP on summer_branch: 66247e0 Modify bla and sunny files.

lkldz@fedora:~/training_material/git_file$ git switch olive_branch 
Switched to branch 'olive_branch'

lkldz@fedora:~/training_material/git_file$ git branch
  master
  new_test_branch
* olive_branch
  summer_branch
  sunny_branch
```
<b><ins>GIT STASH LIST</ins></b>

- Wyświetla listę wszystkich zapisanych w schowku (stash) zmian w lokalnym repozytorium.

```text
stash@{0}: On master: poprawki w formularzu logowania
stash@{1}: WIP on feature/login: 5002e67 dodano nową podstronę
stash@{2}: WIP on master: 049d948 początkowa konfiguracja
```

<ins>Przykład:</ins><br>
```shell
lkldz@fedora:~/training_material/git_file$ git switch sunny_branch 
Switched to branch 'sunny_branch'
lkldz@fedora:~/training_material/git_file$ git stash list
stash@{0}: WIP on summer_branch: 66247e0 Modify bla and sunny files.
```
<b><ins>GIT STASH POP</ins></b>
- Nakłada zmiany, które zostały wcześniej zapisane poleceniem <em>git stash</em>,<br>
  z powrotem na obecny obszar roboczy (working directory).<br>
- W przeciwieństwie do polecenia <em><ins>git stash apply</ins></em> (które tylko kopiuje zmiany, zostawiając je w schowku),<br>
  <em>git stash pop</em> usuwa te dane ze stosu stash po ich pomyślnym zastosowaniu.<br>
- Stash można rozpakować na masterze albo innym branch, dlatego należy uważać, a najlepiej robić <em>git stash list</em>.<br>

<ins>Nałożenie określonej pracy (wskazanie indeksu):</ins>
```shell
git stash pop stash@{<indeks>}
```



<ins>Przykład konfliktu po stash-u:</ins>

```shell
lkldz@fedora:~/training_material/git_file$  git stash pop
Auto-merging bla_file.txt
CONFLICT (content): Merge conflict in bla_file.txt
On branch sunny_branch
Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
	both modified:   bla_file.txt

no changes added to commit (use "git add" and/or "git commit -a")
The stash entry is kept in case you need it again.
```
<ins>Przypadki użycia git stash-a:</ins>
- <b>git stash</b> (lub <b>git stash push</b>) - chowa <ins>wszystkie śledzone</ins>, niezacommitowane zmiany i czyści katalog roboczy.
- <b> git stash -u</b> (lub <b>--include-untracked</b>) - chowa także <ins>nowo utworzone pliki, których git jeszcze nie śledził</ins>.
- <b>git stash save "opis zmian"</b> - chowa zmiany i nadaje im czytelny opis.
- <b>git stash list</b> - wyświetla listę wszystkich zapisanych schowków.
- <b>git stash pop</b> - przywraca najnowszy schowek (stash@{0}) do katalogu roboczego i usuwa go ze schowka.
- <b>git stash apply</b> - przywraca najnowszy schowek, ale pozostawia jego kopię w schowku.
- <b>git stash drop stash@{0}</b> - trwale usuwa konkretny wpis ze schowka.
- <b>git stash clear</b> - usuwa wszystkie zapisane schowki.


<hr style="border:2px solid gray">

## Detached HEAD <a name="detached-head"></a>

- Stan <em>detached HEAD</em> oznacza, że HEAD wskazuje bezpośrednio na konkretny commit lub tag, a nie na branch.
- Można tego użyć aby "cofnąć się w czasie" i zobaczyć jak wyglądał dany
  plik w przeszłości albo co zawierała dana branch.<br>
- W tym stanie możesz swobodnie przeglądać kod, budować projekt i testować,<br>
  ale wszelkie nowe commity nie będą przypisane do żadnej gałęzi<br>
  i zostaną docelowo usunięte przez mechanizm czyszczenia Gita (garbage collection),<br>
  gdy przełączysz się gdzie indziej.<br>
- Następuje przesunięcie HEAD-a na dany commit.<br>
- Aby powrócić do "teraźniejszości" czyli przestawić HEAD na początek: <em>git checkout master</em> 

<ins>Przykład:</ins>

```shell
lkldz@fedora:~/training_material/git_file$ git log
commit f1feafe7328c57d10632b959c476c764206c952b (HEAD)

lkldz@fedora:~/training_material/git_file$ git log --oneline --graph --all
* 66247e0 (summer_branch, master) Modify bla and sunny files.
*   048895b Merge branch 'sunny_branch'
|\  
| * 3fefe9c (sunny_branch) Edited sunny file. Added info about pies.
* | 1af60c1 Edited: sunny file. Added info about kot.
* | e4231cb Merge branch 'sunny_branch'
|\| 
| * 00af6c4 Added sad file.
| * f1feafe (HEAD) Added funny file.   <-- tu jest HEAD
* | 4c2d1e6 Added test2 file.
|/  
* 649c8cc Added placeholder in sunny file.
* 9436a5f Added sunny file.
* feaaee5 (olive_branch) Add pending file and bla_file.txt
| * 8fa1de1 (new_test_branch) Added new text file
|/  
* 4ca14eb Added training files.

lkldz@fedora:~/training_material/git_file$ git switch master
Previous HEAD position was f1feafe Added funny file.
Switched to branch 'master'

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
```

<ins>Przypadek 1 - Chcę zachować commity zrobione w stanie detached HEAD:</ins>
+ Tworzę nową gałąź w bieżącym miejscu:
```shell
git switch -c nazwa_nowej_gałęzi
```
<ins>Przypadek 2 - Chcę porzucić zmiany i wrócić do swojej pracy::</ins>
+ Przełączam się z powrotem na istniejącą gałąź (np. master(main) lub develop):

<ins>Przypadek 3 - Chcę dołączyć swoje commity do istniejącej gałęzi:</ins>
+ Zapisuję zmiany na tymczasowej gałęzi:
```shell
git switch -c temp_branch
```
+ Przechodzę na docelową gałąź i scalam zmiany:
```shell
git switch main
git merge temp_branch
git branch -d temp_branch
```

<ins>Przypadek 4 - Jestem na master i chcę cofnąć się o 2 commity:</ins>
```shell
git checkout HEAD~2
```


<hr style="border:2px solid gray">

# Cofanie zmian <a name="cofanie-zmian"></a>

- Sposób wycofania zmian w zależy od tego, na jakim etapie znajduje się zmiana<br>
  tj. czy jest jeszcze niezatwierdzona, czy dodana do indeksu, czy już zacommitowana lub wysłana na serwer.

<ins>Polecenia używane najczęściej do cofania zmian:</ins> 
1. Etap - katalog roboczy (przed <em>git add</em>):<br>
```shell
git restore plik.txt	<-- cofa zmiany w pliku do stanu z ostatniego commita
```
2. Etap - staging area (po <em>git add</em>):<br>
```shell
git restore --staged plik.txt	<--- usuwa plik ze staging area (zostawia zmiany w pliku).
```

3. Etap - ostatni lokalny commit ale przed wysłaniem na zdalny serwer (po <em>git commit</em> ale przed <em>git push</em>):
```shell
git reset --soft HEAD~1	  <-- cofa commit, ale zachowuje zmiany w kodzie jako przygotowane do commita.
```
Zacommitowane i wypchnięte (git push)	git revert <hash_commita>	Bezpiecznie tworzy nowy commit odwracający wybraną zmianę.

<ins>Przypadek 1 - Cofnięcie zmian we wszystkich plikach w projekcie:</ins>

```shell
git restore .
```
<ins>Przypadek 2 - Usunięcie nowo utworzonych, nieśledzonych plików (untracked):</ins>

```shell
git clean -fd
```
W praktyce:
```shell
lkldz@fedora:~/training_material/git_file$ git status
On branch new_test_branch
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	abc.txt

nothing added to commit but untracked files present (use "git add" to track)
lkldz@fedora:~/training_material/git_file$ git clean -fd
Removing abc.txt
```

<ins>Przypadek 3 - Całkowite usunięcie ostatniego commita wraz ze zmianami w plikach:</ins>
+ To polecenie bezpowrotnie usuwa kod z tego commita z dysku.
```shell
git reset --hard HEAD~1
```

<ins>Przypadek 4 - Zmiany wysłane już do zdalnego repozytorium (po <em>git push</em>):</ins>
+ Jeśli zmiany trafiły na zdalny serwer np. GitHub/GitLab i inni programiści mogli je pobrać, nie należy przepisywać historii za pomocą reset.<br>
+ Bezpieczne odwrócenie zmian to <em>git revert</em>:
+ Git utworzy nowy commit, który jest dokładnym lustrzanym przeciwieństwem wybranego commita (usuwa dodany kod, przywraca usunięty).
```shell
git revert <hash_commita>
git push
```


<hr style="border:2px solid gray">

# Rebase <a name="rebase"></a>

<ins>1. Wprowadzenie:</ins>
   
- Rebase pozwala "przepisać" commity z "feature branch" tak, jakby powstały na bazie najnowszej wersji gałęzi master,<br>
  dzięki czemu historia projektu zostaje czysta i liniowa, bez dodatkowych commitów scalających.
- Są programiści, których irytuje w git log widok merge commita - bo ich zdaniem nic nie wnosi.
- Używa się go głównie do porządkowania historii przed wysłaniem zmian do zespołu (np. przed pull requestem).
- Rebase nadpisuje historię commitów.
- <ins>Nie używa się rebase będąc na main/master</ins> (jest to wręcz zakazane).
- Rebase robi się będąc na feature branch.

<ins>2. Jak to działa wizualnie?:</ins><br>
Rozwijam gałąź <em>feature</em>, a w międzyczasie na <em>master</em> pojawiły się nowe commit-y (C3, C4).:
```text	
          C1 --- C2 (feature) <- HEAD 
         /
--- C0 -
         \
          C3 --- C4 (master)
```

<ins>Opcja 1 - <em>git merge master</em></ins><br>
Po wykonaniu <em>git merge master</em> na gałęzi <em>feature</em><br>
git tworzy tzw. <em>Merge Commit (M)</em>, który łączy historię z obu gałęzi.
```text
         C1 --- C2 ------ M (feature) <- HEAD
         /               /
--- C0 -                /
         \             /
          C3 -------- C4 (master)
```
Zalety tej opcji:
- Zachowuje dokładny przebieg pracy w czasie (drzewiasta struktura).
- Tworzy dodatkowy commit scalający (<em>merge commit</em>).
- Bezpieczny dla wspólnych gałęzi publicznych.

---

<ins>Opcja 2 - <em>git rebase master</em></ins><br>
Po wykonaniu <em>git rebase master</em> na gałęzi <em>feature</em><br>
git „odpina” commity C1 i C2, przewija feature do C4, a następnie aplikuje zmiany C1 i C2 na nowo jako nowe commity C1' i C2'.
```text
				     C0---C3---C4---C1'---C2' (feature) <- HEAD
                    /
--- C0 --- C3 --- C4 (master)
```
Zalety tej opcji:
- Tworzy czystą, prostą, liniową historię.
- Nie tworzy commita scalającego - przepisuje hashe commitów.
- Może powodować problemy, w przypadku przepisywania commit-ów wysłane już na serwer.

<ins><b>Dwa główne tryby użycia <em>git rebase</em></b></ins>
- Standardowy rebase (aktualizacja gałęzi)
- Interaktywny rebase (git rebase -i)

<ins><b>Standardowy rebase (wprowadzenie)</b></ins>
+ Służy do pobrania najnowszego kodu z main/master do gałęzi roboczej (feature) przed wystawieniem Pull Requesta.

```shell
git switch feature
git rebase master
```
+ Jeśli wystąpi konflikt:
	- Rozwiąż konflikt w plikach ręcznie.
    - Dodaj pliki: <em>git add <plik>.</em>
    - Kontynuuj: <em>git rebase --continue</em><br> 
	(lub wycofaj cały proces: <em>git rebase --abort</em>).

<ins><b>Interaktywny rebase (wprowadzenie)</b></ins>
+ Służy do sprzątania historii na lokalnej gałęzi przed jej opublikowaniem<br>
  (np. łączenie małych commitów w jeden, zmiana opisów, usuwanie niepotrzebnych zmian):

<ins>Przykładowe opcje interaktywnego rebase:</ins>

- <b>git rebase -i HEAD~3</b>  <- pozwala edytować ostatnie 3 commity
- <b>pick</b> – zachowaj commit.
- <b>squash</b> (lub s) – połącz ten commit z poprzednim i połącz ich opisy.
- <b>fixup</b> (lub f) – połącz z poprzednim, ale odrzuć opis tego commita.
- <b>reword</b> (lub r) – zmień tylko treść wiadomości commita.
- <b>drop</b> (lub d) – całkowicie usuń ten commit.

<ins><b>"Złota zasada" rebase:</b></ins>
  
  <em>Nigdy nie rób rebase na gałęziach publicznych/współdzielonych (takich jak main/master czy develop)</em>,<br>
  z których korzystają inni programiści.<br>
  Rebase tworzy nowe hashe commitów, czym zmusza innych do ponownego synchronizowania historii i może doprowadzić do bałaganu w repozytorium!

<ins><b>Rebase w codzinnej praktyce:</b></ins>

1. Upewnij się, że masz czysty stan na feature branch.
	
	+ Przed zmianą gałęzi:

		1. Zacommituj swoją aktualną pracę lub tymczasowo ją schowaj:
			```shell
   			git stash
			```

2. Pobierz najnowsze zmiany na main/master.

3. Przełącz się na gałąź główną i zaktualizuj ją ze zdalnego serwera:
```shell
git switch main
git pull
```

4. Przejdź na swój feature branch i zrób rebase:

Przenieś punkt startowy swojego brancha na najświeższy commit z main:

```shell
git switch moj-feature-branch
git rebase main
```

5. Jeśli wcześniej robiłeś <em>git stash</em>, teraz przywróć zmiany poleceniem <em>git stash pop</em>.



  <hr style="border:2px solid gray">

# Interaktywny rebase <a name="interactive-rebase"></a>

<ins><b>Scenariusz przykładowy:</b></ins><br>
1. Pracuję na gałęzi <em>feature-login</em> i zrobiłem 3 małe, robocze ("bałaganiarskie") commit-y:<br>
a1b2c3d (HEAD) fix typo in test<br>
f4e5d6c add login form validation<br>
9a8b7c6 add login button<br>

2. Cel: Chcę połączyć te 3 commity w jeden czysty commit o nazwie "Implement user login flow with validation".


<ins><b>Osiągnięcie celu krok-po-kroku:</b></ins><br>

<ins><b>Krok 1. Uruchom interaktywny rebase</b></ins>

- Wskaż, ile commitów wstecz chcesz edytować (w tym przypadku 3):
```shell
git rebase -i HEAD~3
```

<ins><b>Krok 2. Wybierz operacje w edytorze tekstu</b></ins>

Git otworzy domyślny edytor (np. Nano, Vim lub VS Code) z listą commitów w kolejności od najstarszego (u góry) do najnowszego (na dole):
```shell
pick 9a8b7c6 add login button
pick f4e5d6c add login form validation
pick a1b2c3d fix typo in test

# Commands:
# p, pick  = use commit
# s, squash  = use commit, but meld into previous commit
# f, fixup  = like "squash", but discard this commit's log message
```

<ins><b> Krok 3. Zmień pick na squash (lub skrót s) przy commitach, które chcesz wchłonąć w pierwszy:</b></ins>
```shell
pick 9a8b7c6 add login button
squash f4e5d6c add login form validation
squash a1b2c3d fix typo in test
```

<ins><b> Krok 4. Zapisz plik i zamknij edytor.</b></ins>

<ins><b> Krok 5. Zredaguj ostateczną wiadomość commita: </b></ins>
```shell
# This is a combination of 3 commits.
# This is the 1st commit message:
add login button

# This is the commit message #2:
add login form validation

# This is the commit message #3:
fix typo in test
```

Usuń stare teksty i wpisz jedną czystą wiadomość:
```text
Implement user login flow with validation
```
- Zapisz plik i zamknij edytor.

<ins><b>Krok 6. Efekt końcowy</b></ins>

Po sprawdzeniu historii za pomocą <em>git log --oneline</em>
```shell
7e8d9c0 (HEAD -> feature-login) Implement user login flow with validation
```
Trzy rozdrobnione commity zostały połączone w jeden elegancki commit z nowym hashem.

<ins><b>Przydatne polecenia awaryjne:</b></ins>

Gdy coś poszło nie tak:
```shell
git rebase --abort
```
Przywraca gałąź dokładnie do stanu sprzed uruchomienia rebase.

<ins><b>Gdy commity były już wcześniej wysłane na zdalne repozytorium (GitHub/GitLab):</b></ins>

Zwykły git push zostanie odrzucony, ponieważ historia uległa zmianie. 

Użyj bezpiecznego wymuszenia:
```shell
git push --force-with-lease
```


<hr style="border:2px solid gray">

## Standard rebase <a name="standard-rebase"></a>

<ins>Scenariusz 1:</ins>

1. Na bazie <em>master</em> branch utworzyłem nowy branch.

2. W masterze zedytowałem plik <em>sad_file.txt</em>.

3. Następnie na nowym branchu też zedytowałem plik <em>sad_file.txt</em> ale wstawiłem inną zawartość. Plik dodałem do stage i zrobiłem commit.

4. Będąc na feature branch zrobiłem rebase. W efekcie dostałem <em>rebase konflikt</em>.

```shell
lkldz@fedora:~/training_material/git_file$ vi sad_file.txt 

lkldz@fedora:~/training_material/git_file$ git status
On branch issue_fix
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   sad_file.txt

no changes added to commit (use "git add" and/or "git commit -a")

lkldz@fedora:~/training_material/git_file$ git add .

lkldz@fedora:~/training_material/git_file$ git commit -m "New text to sad file"
[issue_fix 6fe7fc7] New text to sad file
 1 file changed, 2 insertions(+)

lkldz@fedora:~/training_material/git_file$ git rebase master
Auto-merging sad_file.txt
CONFLICT (content): Merge conflict in sad_file.txt     <---- KONFLIKT
error: could not apply 6fe7fc7... New text to sad file
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
hint: Disable this message with "git config set advice.mergeConflict false"
Could not apply 6fe7fc7... # New text to sad file


lkldz@fedora:~/training_material/git_file$ cat sad_file.txt 
<<<<<<< HEAD
There is the beginning.
Some fix.
And ble.
And sth else.
That is what we expect.
=======
My version of this file.
And sth else.
>>>>>>> 6fe7fc7 (New text to sad file)
lkldz@fedora:~/training_material/git_file$
```

- W vi usunąłem konflikty

```shell
lkldz@fedora:~/training_material/git_file$ vi sad_file.txt  <-- USUWAM KONFLIKTY 

lkldz@fedora:~/training_material/git_file$ git add sad_file.txt   <-- POPRAWIONY PLIK DODAJĘ DO STAGING AREA

lukasz@fedora:~/TEST_AUTOMATION/gitone$ git rebase --continue    <--- KONTYNUUJĘ REBASE
[detached HEAD 0c94e4c] New text to sad file
 1 file changed, 1 insertion(+)
Successfully rebased and updated refs/heads/issue_fix.

lkldz@fedora:~/training_material/git_file$ git log --oneline   
0c94e4c (HEAD -> issue_fix) New text to sad file
fc9efc1 (master) Add text to sad file.
66247e0 (summer_branch) Modify bla and sunny files.
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

lkldz@fedora:~/training_material/git_file$  cat sad_file.txt 
There is the beginning.
My version of this file.
Some fix.
And ble.
And sth else.
That is what we expect.

lkldz@fedora:~/training_material/git_file$ git switch master
Switched to branch 'master'

lkldz@fedora:~/training_material/git_file$ cat sad_file.txt   <--- na gałęzi master jest wersja pliku która nie zawiera zmiany z feature branch
There is the beginning.     <---- Na feature branch druga linia jest inna
Some fix.
And ble.
And sth else.
That is what we expect.

lkldz@fedora:~/training_material/git_file$ git branch
  issue_fix
* master
  new_test_branch
  olive_branch
  summer_branch
  sunny_branch

lkldz@fedora:~/training_material/git_file$ git merge issue_fix
Updating fc9efc1..0c94e4c
Fast-forward
 sad_file.txt | 1 +
 1 file changed, 1 insertion(+)

lkldz@fedora:~/training_material/git_file$ cat sad_file.txt 
There is the beginning.
My version of this file.
Some fix.
And ble.
And sth else.
That is what we expect.
lukasz@fedora:~/TEST_AUTOMATION/gitone$
```

<ins>Scenariusz 2: Na master pojawił się nowy plik - chcę go na swojej feature branch</ins>

```shell
lkldz@fedora:~/training_material/git_file$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	test3_file.txt

nothing added to commit but untracked files present (use "git add" to track)

lkldz@fedora:~/training_material/git_file$ git add .

lkldz@fedora:~/training_material/git_file$ git commit -m "Add new test 3 file."
[master d32a813] Add new test 3 file.
 1 file changed, 1 insertion(+)
 create mode 100644 test3_file.txt

lkldz@fedora:~/training_material/git_file$ git switch issue_fix
Switched to branch 'issue_fix'

lkldz@fedora:~/training_material/git_file$ ls
bla_file.txt  funny_file.txt  index.html  sad_file.txt  sunny_file.txt  test2_file.txt  testone.txt  testtwo.txt

lkldz@fedora:~/training_material/git_file$ git rebase master
Successfully rebased and updated refs/heads/issue_fix.

lkldz@fedora:~/training_material/git_file$ ls
bla_file.txt  funny_file.txt  index.html  sad_file.txt  sunny_file.txt  test2_file.txt  test3_file.txt  testone.txt  testtwo.txt
lkldz@fedora:~/training_material/git_file$
```


<ins>Scenariusz 3 ("conflict case"):</ins>

1. Pracuję na feature branch.

2. Na master w zdalnym repo pojawiły się zmiany.

3. Na feature branch robię stash.

4. Przełączam się na master, robię pull.

5. Przełączam się z powrotem na feature branch.

6. Robię rebase.

7. Robię stash pop - pojawiają się konflikty. 

<em>Jak rozwiązać taki konflikt?</em>

Krok 1. Identyfikuję pliki z konfliktami.

```shell
git status
```

Pliki wymagające uwagi będą oznaczone w sekcji <em>Unmerged paths</em> jako <em>both modified</em>.

Krok 2. Rozwiązuję konflikty w edytorze.

Krok 3. Po rozwiązaniu konfliktów dodaję pliki do <em>staging area</em>.

```shell
git add
```
Krok 4. Czyszczę schowek (<em>stash</em>):

```
git stash list
git stash drop stash@{0} <-- OPCJA BEZPIECZNA
ALBO
git stash drop <-- Opróżnienie całego schowka
```

Krok 5. Mogę kontynuować pracę albo mogę zrobić commit.

Aby uniknąć tego typu konfliktów często robi się commit na feature branch, zanim<br>
przełączy się na master w celu pobrania najnowszych zmian.



<hr style="border:2px solid gray">

## Cofnięcie rebase <a name="cofniecie-rebase"></a>

- Git przechowuje historię operacji w tzw. <em>reflog</em>, dzięki czemu można wrócić do stanu sprzed rebase'a.

- Ale są warunki:
  	+ jeszcze niczego nie usunąłem
  	+ nie minęło zbyt dużo czasu
- Reflog domyślnie trzyma wpisy tylko około 90 dni (i tylko lokalnie, nie trafia do zdalnego repo).

- Jeśli zdążyłeś zrobić <em>git push --force</em> po rebase, lokalne cofnięcie nie naprawi automatycznie zdalnej gałęzi.<br>
  Trzeba będzie zrobić kolejny push --force, żeby zsynchronizować zdalne repo ze starym stanem.

<ins><b>Cofnięcie rebase krok-po-kroku:</b></ins>

1. Sprawdzam zawartość <em>reflog</em>

```shell
git reflog
```

Przykładowy output:
```text
a1b2c3d HEAD@{0}: rebase finished: returning to refs/heads/main
e4f5g6h HEAD@{1}: rebase: commit "poprawka X"
i7j8k9l HEAD@{5}: commit: ostatni commit przed rebase
```

2. Odnajduję ostatni commit tuż przed rebase.

3. Wracam do ostatniego commita dokonanego przed rebase:
```shell
git reset --hard HEAD@{5} <--- (zamień 5 na właściwy numer z reflogu)
```

<ins>Uwaga:</ins>

<b>git reset --hard</b> kasuje zmiany w working directory.<br>
Upewnij się, że nie masz niezapisanych zmian, które chcesz zachować.

<ins>Przykład: usuwam test3_file.txt które zostało dodane na skutek rebase.</ins>

```shell
lkldz@fedora:~/training_material/git_file$ ls
bla_file.txt  funny_file.txt  index.html  sad_file.txt  sunny_file.txt  test2_file.txt  test3_file.txt  testone.txt  testtwo.txt

lkldz@fedora:~/training_material/git_file$ git reflog
0c94e4c (HEAD -> issue_fix) HEAD@{0}: reset: moving to HEAD~1
d32a813 (master) HEAD@{1}: rebase (finish): returning to refs/heads/issue_fix
d32a813 (master) HEAD@{2}: rebase (start): checkout master
0c94e4c (HEAD -> issue_fix) HEAD@{3}: checkout: moving from master to issue_fix
d32a813 (master) HEAD@{4}: commit: Add new test 3 file.

lkldz@fedora:~/training_material/git_file$ git reset --hard HEAD@{3}
HEAD is now at 0c94e4c New text to sad file

lkldz@fedora:~/training_material/git_file$ ls
bla_file.txt  funny_file.txt  index.html  sad_file.txt  sunny_file.txt  test2_file.txt  testone.txt  testtwo.txt

lkldz@fedora:~/training_material/git_file$ git log --oneline
0c94e4c (HEAD -> issue_fix) New text to sad file
```


<hr style="border:2px solid gray">

## git amend <a name="git-amend"></a>


- Flaga <em>--amend</em> przy poleceniu git commit służy do poprawienia lub uzupełnienia ostatniego commita zamiast tworzenia nowego.

- <em>git amend</em> Pozwala dokleić zapomniane pliki lub zmienić treść wiadomości commita.<br>
  W praktyce Git usuwa ostatni commit i tworzy w jego miejsce nowy (z nowym identyfikatorem hash).

<ins>Dwa najczęstsze zastosowania:</ins>

1. <em>Zapomniałeś dodać pliku lub drobnej poprawki</em>

Zrobiłeś commit, ale po chwili zauważyłeś literówkę albo pominięty plik:

```shell
git add zapomniany_plik.txt
git commit --amend --no-edit
```

Flaga <b>--no-edit</b> mówi Gitowi, aby zachował dotychczasową wiadomość commita bez otwierania edytora tekstu.

2. <em>Chcesz zmienić tylko treść ostatniej wiadomości</em>

Zrobiłeś commit ze złą nazwą i chcesz ją tylko poprawić

```shell
git commit --amend -m "Nowy, poprawny opis commita"
```

- Hash ostatniego commita - Ostatni hash zostaje zastąpiony nowym

- Nie używaj --amend na commitach, które zostały już wysłane na serwer (git push) do współdzielonej gałęzi.
Ponieważ --amend przepisuje hash ostatniego commita, zwykły git push zostanie odrzucony i będzie wymagał git push --force-with-lease, co może namieszać w pracy innym osobom korzystającym z tej samej gałęzi.


<hr style="border:2px solid gray">

## git fetch vs git pull <a name="fetch-pull"></a>

- Główna różnica: <b>git pull = git fetch + git merge</b>

<b><ins>git fetch</b></ins> 

- Pobiera zmiany ze zdalnego serwera (np. GitHub/GitLab) tj. wszystkie nowe commity, gałęzie i tagi do lokalnego repo.

- Nie zmienia plików w katalogu roboczym ani nie przesuwa znacznika aktualnej gałęzi.

- Pobiera historię ze zdalnego serwera.

- Aktualizuje jedynie zdalne wskaźniki (tzw. remote tracking branches, np. origin/main).

- Jest całkowicie bezpieczne ponieważ nie wywoła konfliktów ani nie nadpisze pracy w toku.

- Pozwala sprawdzić, co zmienili inni, zanim zdecydujemy się to scalić (sprawdzamy zmiany za pomocą <em>git log origin/master</em> lub <em>git diff origin/master</em>).

- Bezpieczny podgląd zmian.

- <em>git fetch</em> mogę użyć aby upewnić się czy zmiany które niedawno ktoś wypchnął do zdalnego repo nie psują tego nad czym teraz pracuję na swojej feature branch.

<br>
<b><ins>git pull</ins></b> 

- Pobiera zmiany ze zdalnego serwera a następnie natychmiast próbuje scalić (merge) pobrane zmiany do gałęzi, na której aktualnie się znajdujesz.
  
- Pobiera historię ze zdalnego serwera.

- Bezpośrednio modyfikuje Twoje lokalne pliki.

- Jeśli na serwerze i localhost zmieniono te same linie, polecenie od razu wyrzuci merge conflict.

- Spore ryzyko konfliktów.

- Szybka aktualizacja bieżącej pracy.

<br>
<ins><b>Praktyczne uwagi:</b></ins>

- <ins>Używaj <em>git pull</em>, gdy masz <em>"czysty stan repozytorium"</em></ins>,<br>
  tj. wiesz, co zostało wypchnięte na serwer i chcesz po prostu zaktualizować swój projekt do najnowszego stanu.

- <ins>Używaj <em>git fetch</em>, gdy pracujesz nad czymś lokalnie</ins><br>
  i chcesz najpierw sprawdzić historię zdalną bez ryzyka zepsucia bieżącej gałęzi<br>
  lub gdy chcesz zaktualizować bazę przed wykonaniem git rebase origin/main.

- <b><em>git fetch origin main</em></b> używać wtedy gdy chcę mieć na feature branch kod zgodny ze zdalnym <em>main-em.</em><br>

-  Kiedy chcę zrobić merge mojej feature branchy do main, to najpierw zrobić pull na main i wtedy merge.


<ins><b>Przypadek 1: Chcę zaktualizować swój feature-branch o najnowszy kod ze zdalnego serwera,<br>
a następnie wciągnąć gotowy feature-branch do lokalnego main</b></ins>

<b>FAZA 1:</b>

```shell
git fetch origin main 
git rebase origin/main
```
- <em>git fetch origin main</em> NIE zaktualizuje lokalnego brancha main.<br>
Zaktualizuje jedynie ukryty wskaźnik zdalny origin/main.<br>
Lokalny branch main pozostanie dokładnie w takim stanie, w jakim był.

<b>Co dokładnie robi <em>git fetch origin main</em>?</b>

Krok 1: Łączy się ze zdalnym serwerem (origin).

Krok 2: Pobiera nowe commity z gałęzi main.

Krok 3: Zapisuje je lokalnie pod wskaźnikiem origin/main.

Krok 4: Nie dotyka lokalnego brancha main ani żadnych plików na dysku.

<b>Dlaczego to wystarcza do rebase?</b>

1. Gdy jesteś na swoim feature-branch, nie potrzebujesz aktualizować lokalnego main. 
Możesz zrobić rebase bezpośrednio na pobrany wskaźnik zdalny:
```shell
git rebase origin/main
```
W ten sposób Twój feature-branch ma najświeższy kod z serwera, a Ty nie musiałeś nawet przełączać się na lokalny main.

<b> FAZA 2:</b> 

Zakończenie pracy - lokalny merge.

Wciągnięcie gotowego feature-branch do lokalnego main:

```shell
git switch main 
git pull 
git merge feature-branch 
git push
```

<ins> Dlaczego w FAZIE 2 trzeba zrobić pull na main?</ins>

Jeśli nie zrobimy git pull, lokalny main będzie przestarzały<br> 
i przy próbie git push serwer odrzuci zmiany.


<ins><b>PRAKTYCZNA UWAGA</b></ins>

W większości firm i zespołów programistycznych nie merguje się gałęzi lokalnie na swoim komputerze.

1. Kończysz pracę na feature-branch.

2. Wypychasz go na serwer: <em>git push origin feature-branch</em>

3. Otwierasz Pull Request (PR) na GitHubie / GitLabie.

4. Klikasz przycisk Merge w przeglądarce po przejściu code review.

5. Dopiero wtedy u siebie na komputerze robisz<br>
   <em>git switch main && git pull</em>, żeby pobrać finalny stan projektu.
