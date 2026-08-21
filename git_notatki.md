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

***********************************************************************

## Git vs GitHub <a name="git-vs-github"></a>

- Git to software.
- GitHub to serwis, tak jak GitLab, Bitbucket itd.
- Git działa na localhost.
- GitHub działa na remote server.


## Version Control System <a name="vcs"></a>

- VCS przechowuje różne wersje tego samego pliku.
- Tworzy swego rodzaju "check pointy".
- Można przełączać się pomiędzy różnymi wersjami tego samego pliku.
- Standardowy cykl pliku:

  	  1. Write (w katalogu roboczym).
  	  2. Add (staging area).
  	  3. Commit (zapisz w historii repo).

## Repo <a name="repo"></a>

- Folder zawierający pliki.
- Folder ten jest śledzony ("trackowany") przez Git.


## Wersja Git-a <a name="git-version"></a>

*polecenie:*

`git --version`

- Git jest bardzo stabilnym programem.
- Członkowie zespołu mogą korzystać z różnych wersji Git-a i nie wpłynie to na funkcjonalność tego programu.


## Pluginy do VSCode <a name="vscode-pluginy"></a>

Poniższe pluginy wizualizują zmiany w lokalnym repo (liniowa historia commitów, branche itd.)

- Git Graph
- GitLens


## Inicjalizacja nowego repozytorium <a name="git-init"></a>

*polecenie:*

`git init`

- Powyższe polecenie tworzy nowe repozytorium (repo).
- Utworzony zostaje ukryty (*hidden*) folder .git


## Katalog .git <a name="git-dir-hidden"></a>

- Przechowuje informacje związane z utworzonym repozytorium m.in:
  * konfigurację repo
  * historię commit-ów
  * informacje o stage are
- Zasadniczo użytkownik nie dokonuje zmian w tym katalogu


## Pobieranie (pulling) istniejącego repo z remote serwera <a name="pulling-existing-repo"></a>

*polecenie:*

`git clone url_repozytorium`

- Git sam utworzy katalog .git
- Nie trzeba wpisywać git init


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


## Untracked files <a name="untracked-files"></a>

- Wpisując polecenie <em>git status</em> wewnątrz repo można znaleźć "untracked files".
- Git nie śledzi zmian w takich plikach.
- Polecenie <em>git add</em> zmienia status takich plików na "tracked".


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

## git commit <a name="git-commit"></a>

- Commit:
  	* Jest to swego rodzaju "check point" (snapshot/migawka) za pomocą którego zapisuę plik/pliki w danym stanie/danej wersji.
  	* Każdy commit ma unikalny id.

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

## git config <a name="git-config"></a>
