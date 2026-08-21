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
  * informacja, że znaduję się w staging area
  * changes to be commited
 
- Dodanie całej zawartości katalogu roboczego do Staging Area:

```shell
	git add .
```

