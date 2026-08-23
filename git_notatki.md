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

6. Utwórz branch i od razu przełącz się na niego/nią:
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
