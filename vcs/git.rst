=====
 Git
=====
------------------------------
 Systém pro správu verzí kódu
------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

Příkazem::

   $ sudo apt install git

Základní ovládání
=================

Nastavení
---------

Nezbytné pro běh Gitu.

config
^^^^^^

Zobraz nebo nastav nastavení Gitu.

config --global
"""""""""""""""

Nastav globálně identitu uživatele (povinné)::

   $ git config --global user.name "Davie Badger"
   $ git config --global user.email "davie.badger@gmail.com"

Nastav globálně editor pro práci s Gitem (nepovinné)::

   $ git config --global code.editor vim

.. note::

   Bez použítí volby ``--global`` bude nastavení platné jenom v daném
   repozitáři.

config --list
"""""""""""""

Zobraz veškerá nastavení Gitu::

   $ git config --list
   user.name=Davie Badger
   user.email=davie.badger@gmail.com
   core.editor=vim

Globální nastavení se ukládá do souboru ``~/.gitignore`` a lokální v repozitáři
v ``.git/config``.

.. tip::

   Zobraz jen konkrétní nastavení::

   $ git config user.name
   Davie Badger

Vytvoření repozitáře
--------------------

init
^^^^

Vytvoř Git repozitář v nějakém adresáři::

   $ cd project/
   $ git init

.. note::

   Při vytvoření repozitáře vznikne skrytý ``.git/`` adresář, kam se ukládájí
   informace o repozitáři.

clone
^^^^^

Zkopíruj odněkud již existující repozitář::

   $ ls
   $ git https://daviebadger@gitlab.com/daviebadger/notes.git
   $ ls
   notes

.. tip::

   Zkopíruj existující repozitář pod jiným jménem::

      $ git clone https://daviebadger@gitlab.com/daviebadger/notes.git poznamky
      $ ls
      poznamky

Zaznamenávání změn v repozitáři
-------------------------------

status
^^^^^^

Zobraz aktuální stav repozitáře::

   $ git status
   On branch master

   Initial commit

   nothing to commit (create/copy files and use "git add" to track)

Pokud není žádná zmíňka o souborech v adresáři, tak se aktuální obsah
repozitáře nijak neliší od předchozího uloženého stavu, respektive snímku
(commit).

.. note::

   V případě zkopírovaného adresáře by byl stav následující::

      $ git status
      On branch master
      Your branch is up-to-date with 'origin/master'.
      nothing to commit, working tree clean

Odbočka ke stavům souborů
"""""""""""""""""""""""""

Soubory v repozitářích se mohou nacházet v následujících stavech:

* Untracked

  * nový soubor, který není v předchozí snímku repozitáře a v aktuální stavu
    repozitáře není ještě sledován Gitem::

       $ ls
       $ touch file.txt
       $ git status
       On branch master

       Initial commit

       Untracked files:
         (use "git add <file>..." to include in what will be committed)

               file.txt

       nothing added to commit but untracked files present (use "git add" to track)

* Unmodified

  * soubor je sledován Gitem a nachází se v předchozím snímku repozitáře, ale
    od té doby se nezměnil jeho obsah

* Modified

  * soubor se nachází v předchozím snímku, ale v aktuálním stavu repozitáře
    došlo k jeho modifikaci (změna obsahu souboru, přejmenování, smazání atd.),
    přičemž tato modifikace není zaznamenána
  * taktéž se jedna o soubor, kde byla zaznamenána modifikace, ale v daném
    souboru došlo ještě k další modifikaci, která už není zaznamenána

* Staged

  * soubor, který je zaznamenán včetně jeho modifikace a je připraven pro
    uložení aktuálního stavu repozitáře (vytvoření snímku)::

       $ git status
       On branch master

       Initial commit

       Changes to be committed:
         (use "git rm --cached <file>..." to unstage)

               new file:   file.txt

add
^^^

Přesuň soubor(y) z ``Untracked`` nebo ``Modified`` stavu do ``Staged`` stavu::

   $ touch file.txt
   $ git add file.txt
   $ git status
   On branch master

   Initial commit

   Changes to be committed:
     (use "git rm --cached <file>..." to unstage)

           new file:   file.txt

V případě adresářů přesuň všechny soubory v daném adresáři::

   $ git add dir/

Taktéž jdou použít zástupné znaky::

   $ git add *

Odbočka k ignorování některých souborů
""""""""""""""""""""""""""""""""""""""

Defaultně se v ``Untracked`` stavu objeví všechny nové soubory v repozitáři
kromě prázdných adresářů. Tomuto chování lze pomocí souboru ``.gitignore``
v kořenu repozitáře, kde lze nadefinovat masky::

   # ignoruj všechny soubor s koncovkou .txt

   *.txt

   # u souborů s názvem file.txt udělej výjimku a neignoruj je

   !file.txt

   # ignoruj všechny složky s daným názvem

   __pycache__/

   # ignoruj všechny soubor v kořenovém adresáři

   /*

   # ignoruj všechny soubory s koncovkou .txt jenom v daném adresáři a jeho
   # vnořených adresářích

   doc/**/*.txt

.. note::

   V lokálním ``.gitignore`` souboru by měly být jen ty masky, které se budou
   aplikovat u každého člověka pracující s daným repozitářem.

   Pokud někdo používá editor X a ten vytváří v repozitáři soubory, které se
   u jiných uživatelů netvoří, tak je vhodné mít globální ``.gitignore``,
   např. ``~/.gitignore``::

      $ git config --global core.excludesfile ~/.gitignore
      $ echo "*.txt" > ~/.gitignore

diff
^^^^

Zobraz rozdíl mezi předchozím snímkem souboru (stav ``Unmodified``) nebo mezi
poslední zaznamenanou změnou (stav ``Staged``) a aktuálním stavem souboru
(stav ``Modified``)::

   $ touch file.txt
   $ git add file.txt
   $ echo Hello World! > file.txt
   $ git diff file.txt
   diff --git a/file.txt b/file.txt
   index e69de29..980a0d5 100644
   --- a/file.txt
   +++ b/file.txt
   @@ -0,0 +1 @@
   +Hello World!

Zobraz tyto rozdíly u všech souborů z daného adresáře::

   $ git diff dir/

Zobraz tyto rozdíly u všech souborů v daném repozitáři::

   $ git diff

diff --staged
"""""""""""""

Zobraz rozdíl mezi předchozím stavem souboru a aktuálním stavem souboru ve
``Staged`` stavu::

   $ rm file.txt
   $ echo Hello World! > file.txt
   $ git add file.txt
   $ git diff
   $ git diff --staged
   diff --git a/file.txt b/file.txt
   new file mode 100644
   index 0000000..980a0d5
   --- /dev/null
   +++ b/file.txt
   @@ -0,0 +1 @@
   +Hello World!

.. note::

   Pomocí ``--staged`` volby lze zjistit, jaké změny v souboru se uloží do
   snímku.

commit
^^^^^^

Ulož aktuální stav repozitáře, respektive vytvoř jeho snímek z těch souborů,
které jsou ve stavu ``Staged``::

   $ git commit

Vykonáním tohoto příkazu se otevře editor, kde je třeba napsat stručně zprávu,
která popisuje změny v repozitáři::

   Add file.txt

   # Please enter the commit message for your changes. Lines starting
   # with '#' will be ignored, and an empty message aborts the commit.
   # On branch master
   #
   # Initial commit
   #
   # Changes to be committed:
   #	new file:   file.txt
   #

Po uložení této zprávy a zavření editoru se vytvoří snímek (commit) repozitáře
jako opěrný bod v historii repozitáře, ke kterému se lze kdykoliv vrátit a
obnovit obsah adresáře zpětně do tohoto stavu.

commit -m
"""""""""

Vytvoř snímek repozitáře bez nutnosti otevření editoru a jako zprávu použij
argument pro volbu ``-m``::

   $ git commit -m "Add file.txt"
   [master (root-commit) 26b70d6] Add file.txt
    1 file changed, 1 insertion(+)
    create mode 100644 file.txt


commit -a
"""""""""

Přidej do ``Staged`` stavu i ty soubory, které jsou ve stavu ``Modified`` a
teprve pak vytvoř snímek::

   $ > file.txt
   $ git diff
   diff --git a/file.txt b/file.txt
   index 980a0d5..e69de29 100644
   --- a/file.txt
   +++ b/file.txt
   @@ -1 +0,0 @@
   -Hello World!
   $ git commit -am "Clear content of file.txt"
   [master 65a55c2] Clear content of file.txt
    1 file changed, 1 deletion(-)

rm
^^

Odstraň z Gitu daný soubor(y) a taktéž jej trvale smaž::

   $ ls
   file.txt
   $ git rm file.txt
   $ ls
   $ git status
   On branch master
   Changes to be committed:
     (use "git reset HEAD <file>..." to unstage)

           deleted:    file.txt

.. note::

   Ekvivalentní postup by byl::

      $ rm file.txt
      $ git add file.txt
      $ git status
      On branch master
      Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

              deleted:    file.txt

      $ ls
      $

.. tip::

   U tohoto příkazu jdou použít známé volby ``-f`` nebo ``-r``, jako u
   klasíckého ``rm`` příkazu.

rm --cached
"""""""""""

Odstraň z Gitu daný soubor(y), ale nechej jej existovat v adresáři::

   $ ls
   file.txt
   $ git rm --cached file.txt
   On branch master
   Changes to be committed:
     (use "git reset HEAD <file>..." to unstage)

           deleted:    file.txt

   Untracked files:
     (use "git add <file>..." to include in what will be committed)

           file.txt

   $ ls
   file.txt

mv
^^

Přejmenuj, respektive přesuň soubory v repozitáři na jiné místo tak, aby o tom
věděl Git::

   $ git mv file.txt f.txt
   $ git status
   On branch master
   Changes to be committed:
     (use "git reset HEAD <file>..." to unstage)

           renamed:    file.txt -> f.txt

.. note::

   Ekvivalentní postup by byl::

      $ mv file.txt f.txt
      $ git rm file.txt
      $ git add f.txt

TODO
====

* remote add origin + git pull origin master (existující repozitář)
* git difftool
* tvar commit zprávy
