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

.. note::

   Bez použítí volby ``--global`` bude nastavení platné jenom v daném
   repozitáři.

config --list
"""""""""""""

Zobraz lokální nastavení Gitu::

   $ git config --list
   user.name=Davie Badger
   user.email=davie.badger@gmail.com
   core.repositoryformatversion=0
   core.filemode=true
   core.bare=false
   core.logallrefupdates=true

.. note::

   Lokální nastavení se zobrazí jen v případě, kdy se aktuální pracovní
   adresář nachází uvnitř repozitáře. Mimo repozitář se zobrazí globální
   nastavení. To lze také zobrazit příkazem::

      $ git config --global --list
      user.name=Davie Badger
      user.email=davie.badger@gmail.com

Globální nastavení se ukládá do souboru ``~/.gitignore`` a lokální v rootu
repozitáře v ``.git/config``.

.. tip::

   Zobraz jen konkrétní nastavení::

   $ git config user.name
   Davie Badger

Vytvoření repozitáře
--------------------

init
^^^^

Vytvoř Git repozitář v nějakém adresáři::

   $ cd dir/
   $ git init

.. note::

   Při vytvoření repozitáře vznikne skrytý ``.git/`` adresář, kam se ukládájí
   informace o repozitáři.

clone
^^^^^

Zkopíruj odněkud již existující repozitář::

   $ git https://daviebadger@gitlab.com/daviebadger/notes.git
   $ ls
   notes
   $ cd notes

.. tip::

   Zkopíruj existující repozitář pod jiným jménem::

      $ git clone https://daviebadger@gitlab.com/daviebadger/notes.git poznamky
      $ ls
      poznamky

.. tip::

   Zkopíruj existující repozitář do aktuálního pracovní adresáře bez vytvoření
   stejnojmenné složky::

      $ git clone https://daviebadger@gitlab.com/daviebadger/notes.git .

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
repozitáře nijak neliší od předchozího uloženého stavu, respektive snímku.

.. note::

   V případě naklonovaného adresáře by byl stav následující::

      $ git status
      On branch master
      Your branch is up-to-date with 'origin/master'.
      nothing to commit, working tree clean

Odbočka ke stavům souborů
"""""""""""""""""""""""""

Soubory v repozitářích se mohou nacházet v následujících stavech:

* Untracked

  * nový soubor, který není v předchozím snímku repozitáře a v aktuální stavu
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
  * taktéž se jedná o soubor, kde byla zaznamenána modifikace, ale v daném
    souboru došlo ještě k další modifikaci, která už není zaznamenána

* Staged

  * soubor, který je zaznamenán včetně jeho modifikace a je připraven pro
    uložení stavu (vytvoření snímku)::

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
kromě prázdných adresářů. Tomuto chování lze zabránit pomocí souboru
``.gitignore`` v kořenu repozitáře, kde lze nadefinovat masky::

   # ignoruj všechny soubor s koncovkou .txt

   *.txt

   # u souborů s názvem file.txt udělej výjimku a neignoruj je

   !file.txt

   # ignoruj všechny složky s daným názvem

   __pycache__/

   # ignoruj všechny soubory v kořenovém adresáři

   /*

   # ignoruj všechny soubory s koncovkou .txt jenom v daném adresáři a jeho
   # vnořených adresářích

   doc/**/*.txt

.. note::

   V lokálním ``.gitignore`` souboru by měly být jen ty masky, které se budou
   aplikovat u každého člověka pracující s daným repozitářem.

   Pokud někdo používá editor X a ten vytváří v repozitáři soubory, které se
   u jiných uživatelů netvoří, tak je vhodné mít globální ``.gitignore``,
   např. v ``~/.gitignore``::

      $ git config --global core.excludesfile ~/.gitignore
      $ echo "*.txt" > ~/.gitignore

diff
^^^^

Zobraz rozdíly v souborech::

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

.. note::

   Rozdíly se zobrazí jen u těch souborů, které nejsou ve ``Staged`` módu a
   zároveň u nich existuje poslední zaznamenána změna nebo snímek, aby vůbec
   bylo možné nějaké rozdíly zobrazit.

Zobraz rozdíl jen u konkrétních složek::

   $ git diff dir/

Zobraz rozdíly jen u konkrétních souborů::

   $ git diff file.txt

diff --staged
"""""""""""""

Zobraz rozdíly u těch souborů, které jsou ve ``Staged`` módu::

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

diff HEAD
"""""""""

Zobraz rozdíly nezáležijích na stavu souborů::

   $ git diff HEAD

.. note::

   ``HEAD`` v Gitu odkazuje na poslední snímek ve větvi, kde se právě nacházím.

   Jinými slovy pomocí ``HEAD`` reference pro ``git diff`` příkaz půjdou vidět
   veškeré změny od posledního snímku, ať už se soubor nachází v jakémkoliv
   stavu.

.. tip::

   Rozdíly v souborech lze zobrazovat i pomocí nástrojů k tomu určených,
   které umí vedle sebe zobrazit obsah původního a změněného souboru. V případě
   editoru Vim lze použít následující konfiguraci::

      $ git config --global diff.tool vimdiff
      $ git config --global difftool.prompt false

   Poté je třeba místo ``git diff`` příkazu psát ``git difftool``::

      $ git difftool file.txt

   V případě vícero souborů se pro každý soubor pustí nová instance Vimdiffu.

commit
^^^^^^

Ulož aktuální stav repozitáře, respektive vytvoř jeho snímek z těch souborů,
které jsou ve stavu ``Staged``::

   $ git commit

Vykonáním tohoto příkazu se otevře výchozi editor, kde je třeba napsat stručně
zprávu, která popisuje změny v repozitáři::

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
obnovit obsah repozitáře zpětně do tohoto stavu.

.. tip::

   Nastavení konkrétního editoru pro Git::

      $ git config --global code.editor vim

Odbočka ke commit zprávám
"""""""""""""""""""""""""

Dobře formovaná commit zpráva se drží následující standardizované struktury::

   Předmět zprávy do 50 znaků (povinné)

   Předmět zprávy je jako předmět u emailu. Měl by stručně vyjádřit, k
   jaké změně v commitu došlo. Vyjadření by mělo být ve tvaru rozkazovacího
   způsobu, např. "Update API documentation".

   Předmět zprávy začíná velkým písmem a nekončí tečkou na konci. Na konci
   předmětu zprávy lze vložit odkaz na číslo issue na GitHubu / GitLabu, např.
   "Update API documentation (#123)".

   U rozsáhlejších projektů lze ještě použít prefixy, které vystihují oblast,
   které se týka commit, např. "doc: Update API documentation".

   Zkráceně:

   * předmět zprávy do 50 znaků s velkým prvním písmenem a bez tečky na konci,
     ve kterém je stručný popis změny v repozitáři v rozkazovacím způsobu
   * předmět je povinný, za kterým může následovat tělo zprávý, avšak mezi nimi
     musí být jedna prázdná mezera
   * v nepovinném tělu lze podrobně popsat, proč došlo k dané změně
   * vysvětlení lze strukturovat do odstavců a případně i použít nečíslované
     seznamy pomocí hvězdiček "*" a nebo pomlček "-"
   * délka řádku v těle by neměla překročit hranici 72 znaků

.. note::

   Předmět zprávy je velmi důležitý, neboť se s ním bude pracovat i v jiných
   příkazech.

commit -m
"""""""""

Vytvoř commit repozitáře bez nutnosti otevření editoru a jako zprávu použij
argument pro volbu ``-m``::

   $ git commit -m "Add file.txt"
   [master (root-commit) 26b70d6] Add file.txt
    1 file changed, 1 insertion(+)
    create mode 100644 file.txt

.. note::

   Volba ``-m`` je vhodná jen pro případy, kdy stačí jen předmět zprávy.

commit -a
"""""""""

Přidej do ``Staged`` stavu soubory, které jsou ve stavu ``Modified`` a vytvoř
commit::

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

.. note::

   Platí jen pro soubory, které byly před změnou ve stavu ``Unmodified``.

commit --amend
""""""""""""""

Zahrň do posledního commitu aktuální soubory ve stavu ``Staged``::

   $ touch another_file.txt
   $ git add another_file.txt
   $ git commit --amend

.. note::

   Pokud není žádný soubor ve ``Staged`` módu, tak lze upravit zprávu posledního
   commitu.

.. tip::

   Pří zahrnutí souborů do předchozí commitu se znovu otevře editor pro
   editaci zprávy. Pokud nechci editovat zprávu, tak lze použít ještě volbu
   ``--no-edit``::

      $ git commit --amend --no-edit

reset
^^^^^

Změn stav souboru z ``Staged`` zpět na ``Modified``, respektive na
``Untracked`` u nových souborů::

   $ touch new.txt
   $ git add new.txt
   $ git status
   On branch master
   Changes to be committed:
     (use "git reset HEAD <file>..." to unstage)

           new file:   new.txt

   $ git reset HEAD new.txt
   $ git status
   On branch master
   Untracked files:
     (use "git add <file>..." to include in what will be committed)

           new.txt

   nothing added to commit but untracked files present (use "git add" to track)

.. note::

   Pro změnu stavu z ``Modified`` na ``Unmodified`` (dojde k trvalému zahození
   změn) je třeba použít jiný příkaz a to ``git checkout --``::

      $ cat new.txt
      $ git add new.txt
      $ git commit -m "Add new.txt"
      $ echo new > new.txt
      $ cat new.txt
      new
      $ git checkout -- new.txt
      $ cat new.txt
      $

reset --hard
""""""""""""

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
   klasíckého Unixového``rm`` příkazu.

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

Historie commitů
----------------

log
^^^

Zobraz historii všech commitů::

   $ git log
   commit 239e88de07b21c1be080cc36be8a71ab6264b29f
   Author: Davie Badger <davie.badger@gmail.com>
   Date:   Sun May 21 19:56:34 2017 +0200

       Remove file.txt from Git

   commit 65a55c2b66d00ed6fc3137e307a975ad4e720711
   Author: Davie Badger <davie.badger@gmail.com>
   Date:   Sun May 21 15:19:35 2017 +0200

       Clear content of file.txt

   commit cb95d79e17f67de125688d875d3eda72760c541a
   Author: Davie Badger <davie.badger@gmail.com>
   Date:   Sun May 21 15:14:51 2017 +0200

       Add file.txt

.. note::

   Z commitů jsou vytažený jenom předměty zpráv.

log -N
""""""

Zobraz jen Ntý počet commitů::

   $ git log -1
   commit 239e88de07b21c1be080cc36be8a71ab6264b29f
   Author: Davie Badger <davie.badger@gmail.com>
   Date:   Sun May 21 19:56:34 2017 +0200

       Remove file.txt from Git
   $

log -p
""""""

Zobraz historii commitů spolu s rozdíly::

   $ git log -p -1
   commit 239e88de07b21c1be080cc36be8a71ab6264b29f
   Author: Davie Badger <davie.badger@gmail.com>
   Date:   Sun May 21 19:56:34 2017 +0200

       Remove file.txt from Git

   diff --git a/file.txt b/file.txt
   deleted file mode 100644
   index e69de29..0000000

log --stat
""""""""""

Zobraz u historie commitů i přehled souborů, které se změnily::

   $ git log --stat -1
   commit 239e88de07b21c1be080cc36be8a71ab6264b29f
   Author: Davie Badger <davie.badger@gmail.com>
   Date:   Sun May 21 19:56:34 2017 +0200

       Remove file.txt from Git

    file.txt | 0
    1 file changed, 0 insertions(+), 0 deletions(-)

log --oneline
"""""""""""""

Zobraz jednořádkově historii commitů, kde jsou jen hashe commitů (ID) a
předměty commitů::

   $ git log --oneline
   3cdddbb Add new.txt
   239e88d Remove file.txt from Git
   65a55c2 Clear content of file.txt
   cb95d79 Add file.txt

log --pretty
""""""""""""

Uprav výstup historie commitů podle vlastního formátu::

   $ git log --pretty=format:"%h - %s (%an, %cr)"
   239e88d - Remove file.txt from Git (Davie Badger, 3 hours ago)
   65a55c2 - Clear content of file.txt (Davie Badger, 7 hours ago)
   cb95d79 - Add file.txt (Davie Badger, 7 hours ago)

Legenda voleb ve formátování:

=====  ======
Volba  Význam
=====  ======
%h     zkrácený hash commitu
%s     předmět commitu
%an    jméno autora
%cr    relativní čas vytvoření commitu
=====  ======

.. note::

   Se zkráceným hashi commitů lze dále pracovat v ostatních Git příkazech, kde
   je třeba znát odkaz na konkrétní commit (jeho ID).

log --author
""""""""""""

Zobraz jen ty commity, které vytvořil daný autor::

   $ git log --author="Davie Badger"

log --grep
""""""""""

Zobraz jen ty commity, které mají ve zprávě daný text::

   $ git log --grep=file.txt

.. note::

   Grepů lze použít více najednou nebo také v kombinaci s volbou ``--author``,
   nicméně Git defaultně tyto podmínky nesčítá do jedné velké. Jinými slovy
   stačí, aby jedna z těchto podmínek byla platná.

   Pro sečtení těchto podmínek je třeba ještě použít volbu ``--all-match``::

      $ git log --grep=file.txt --author="Davie Badger" --all-match

.. tip::

   Defaultně je grep citlivý na velká a malá písmena. Pro vypnutí tohoto
   chování je třeba použít ještě volbu ``-i``::

      $ git log --grep=file.txt -i

log --before
""""""""""""

Zobraz jen ty commity, které byly vytvořeny před daným datem::

   $ git log --before=2017-05-21
   $ git log --before="2017-05-21 20:00"

.. note::

   Datum se píše ve formátu ``YYYY-MM-DD``.

log --after
"""""""""""

Zobraz jen ty commity, které byly vytvořeny po daném datu::

   $ git log --after=2017-05-20

.. note::

   Volby ``--before`` a ``--after`` jdou zkombinovat pro vytvoření rozsahu
   od - do.

show
^^^^

Ukaž poslední commit spolu s rozdíly::

   $ git show

.. note::

   Ekvivalentní postup by byl::

      $ git log -p -1

Ukaž konkrétní commit spolu s rozdíly::

   $ git show cb95d79
   commit cb95d79e17f67de125688d875d3eda72760c541a
   Author: Davie Badger <davie.badger@gmail.com>
   Date:   Sun May 21 15:14:51 2017 +0200

       Add file.txt

   diff --git a/file.txt b/file.txt
   new file mode 100644
   index 0000000..980a0d5
   --- /dev/null
   +++ b/file.txt
   @@ -0,0 +1 @@
   +Hello World!

Verzování
---------

Commity lze dále zaobalit do verze (tagu), která vytvoří další opěrný bod v
historii repozitáře.

tag
^^^

Zobraz všechny tagy, pokud nějaké existují::

   $ git tag
   v0.1.0

tag -a
""""""

Vytvoř nový tag::

   $ git tag -a v0.2.0

Stejně jako u vytvoření commitu, i zde se objeví editor pro vytvoří
zprávy popisující tag. Otevření editoru lze taktéž přeskočit přes volbu
``-m``::

   $ git tag -a v0.2.0 -m "v0.2.0"

.. note::

   U tagových zpráv lze aplikovat stejný formát jako u commit zpráv.

.. tip::

   Pomocí ``git show`` lze zobrazit detail tagu::

      $ git show v0.2.0
      tag v0.2.0
      Tagger: Davie Badger <davie.badger@gmail.com>
      Date:   Tue May 23 21:30:05 2017 +0200

      verze v0.2.0

      commit 3cdddbbaf75befae94ea03ef25c304a00a258ebe
      Author: Davie Badger <davie.badger@gmail.com>
      Date:   Mon May 22 20:54:39 2017 +0200

          Add new.txt

      diff --git a/new.txt b/new.txt
      new file mode 100644
      index 0000000..1385f26
      --- /dev/null
      +++ b/new.txt
      @@ -0,0 +1 @@
      +hey

Odbočka ke způsobu verzování
""""""""""""""""""""""""""""

Standardizovaným formátem verzování je sémantické verzování, které má
následující tvar::

   MAJOR.MINOR.PATCH

* MAJOR

  * číslo hlavní verze, kde změny nejsou zpětně kompatibilní z předešlou
    hlavní verzí

* MINOR

  * číslo vedlejší verze, kde při zachování zpětné kompatibility došlo k
    přídání další funkcionality

* PATCH

  * číslo aktualizační (záplatové) verze, kde došlo zejména k opravám chyb nebo
    taky k vylepšení algoritmů (zrychlení běhu programu) při zachování zpětné
    kompatibility

.. note::

   Zpravidla první tag začína na verzi ``0.1.0``, přičemž v rámci této nulové
   hlavní verze může dojít k nekompatibilitám mezi vedlejší verzemi, dokud
   se vývoj nedostatne do stabilní verze ``1.0.0``.

V případě potřeby lze vydat ještě předbězné verze, vyžaduje-li to situace,
např. maximální otestování softwaru. Tyto předběžné verze používájí následující
tvar::

   MAJOR.MINOR.PATCH-alpha|beta|rc[.číslo]

* alpha

  * zmražení vývoje nových funkcionalit, začátek testování softwaru od
    samotných vývojářů::

       0.3.0-alpha
       0.3.0-alpha.1
       0.3.0-alpha.2

* beta

  * začátek testování softwaru ze strany uživatelů::

       0.3.0-beta
       0.3.0-beta.1
       0.3.0-beta.2

* rc

  * konec testování a opravování kódu, pokud se nevyskytne nějaká závažnější
    chyba::

       0.3.0-rc
       0.3.0-rc.1
       0.3.1-rc.2

  * příprava na vydání finální verze (X.Y.Z)

tag -l
""""""

Zobraz všechny tagy nebo zobraz jen ty tagy, které vyhovují dané masce::

   $ git tag -l v0.1.*
   v0.1.0

tag -d
""""""

Smaž daný tag::

   $ git tag -d v0.2.0
   Deleted tag 'v0.2.0' (was a8519ff)

Pokročilé ovládání
==================

Větvení
-------

branch
^^^^^^

Zobraz seznam lokálních větví::

   $ git branch
   * master

Vytvoř novou lokální větev::

   $ git branch devel
   $ git branch
     devel
   * master

.. note::

   ``*`` indikuje aktuální větev, ve které se právě teď nacházím.

Odbočka k větvím
""""""""""""""""

Pomocí větví lze separovat kód pro vývoj nových funkcionalit nebo pro opravu
chyb, aniž by se nějak narušoval funkční kód. Větve umí automaticky vytvořit
kopii kódu, tudíž není třeba spravovat archívy nebo opouštět pracovní adresář.

Každý repozitář vždy začíná na větví zvane ``master``, od které lze odbočit
do jiné větve něco vyvinout nebo opravit a pak se vrátit zprátky. Tuto
odbočenou větev lze pak sloučit do ``master`` větve, aby se sjednotil kód.

::

   fix:           commit
                 /      \
   master: commit ------ commit ------------------------ commit
                               \                        /
   feature:                     commit - commit - commit

Taktéž větve slouží k tomu, aby mnoho lidí najednou neměnilo obsah repozitáře,
ale každý si vytvořil svoji vlastní kopii. V ní provedl svůj umýsl, nechal
otestovat a zkontrolovat kód, než se větev sloučí s ``master`` větví.

.. note::

   Větve se nemusí nutně slučovat, pokud je nutné udržovat různé verze
   projektu.

Zpravidla v ``master`` větvi se nachází kód pro vývoj. U uzavřených projektů je
větev ``stable``, která je nasazená v ostrém provozu (produkci). V případě
otevřených projektů mohou být větve podle vedlejšich verzí projektu, např.
``v2.1`` nebo ``v2.1.x``.

Ostatní větve lze pak různě pojmenovat a záleží jen na domluvě v týmu, jaký
standard se bude dodržovat.

Ukázky možných pojménování větví::

   bug-fix-imports
   bug/fix-imports
   bug-123-fix-imports
   bug/123/fix-imports

   feature-async-requests
   feature-123-async-requests
   feature/async-requests

   hotfix-memory-leak
   hotfix/memory-leak

   async-requests
   123-async-requests
   123/async-requests

   daviebadger-async-requests
   daviebadger/async-requests

.. note::

   ID čísla zpravidla výchazejí z nějakého trackovacího nástroje.

branch -r
"""""""""

Zobraz seznam větví ve vzdáleném repozitáři::

   $ git branch -r
     origin/HEAD -> origin/master
     origin/master

.. note::

   Je třeba mít zpravidla naklonovaný repozitář.

branch --merged
"""""""""""""""

Zobraz seznam větví, které už jsou sloučené do nějaké jiné větve::

   $ git branch --merged

.. note::

   Mergnuté větve je třeba pravidelně mazat, neboť už nemají žádný další užitek
   a svůj účel už naplnily, aby nedošlo k nepořádkům v repozitáři.

branch --no-merged
""""""""""""""""""

Zobraz seznam větví, které ještě nejsou mergnuté::

   $ git branch --no-merged

branch -m
"""""""""

Přejmenuj aktuální větev na jiné jméno::

   $ git status
   On branch devel
   nothing to commit, working tree clean
   $ git branch -m develop
   $ git status
   On branch develop
   nothing to commit, working tree clean

Přejmenuj nějakou větev na jiné jméno::

   $ git branch -m <staré_jméno_větve> <nové_jméno_větve>

branch -d
"""""""""

Smaž danou větev::

   $ git branch -d <jméno_větve>

.. note::

   Git může odmítnout smazání dané větve, neboť ještě nebyla mergnuta do jiné
   větve. Pro násilné smázání této větve je třeba použít ``-D`` volbu::

      $ git branch -D <jméno_větve>

checkout
^^^^^^^^

Přepni se na jinou větev::

   $ git checkout <název_větve>

.. note::

   Git může odmítnout přepnutí na jinou větev, pokud v aktuální větví došlo
   ke změně nějakého ``Unmodified`` souboru (změna není commitnuta), přičemž v
   jiné větvi by byl soubor bez dané změny (kolize).

      error: Your local changes to the following files would be overwritten by
      checkout:
              file.txt
      Please commit your changes or stash them before you switch branches.
      Aborting

   Pokud se v aktuální větvi nacházejí nové soubory, u kterých ještě neexistuje
   historie, tak se automaticky přenáší do dané větve.

checkout -b
^^^^^^^^^^^

Vytvoř novou větev a hned se na ni přepni::

   $ git checkout -b <název_větve>

Vytvoř novou větev z nějakého opěrného bodu a hned se na ni přepni::

   $ git checkout -b <název_větve> origin/master
   $ git checkout -b <název_větve> 509677f
   $ git checkout -b <název_větve> v0.1.0

stash
^^^^^

Ulož bokem aktuální stav větve bez ohledu na stav souborů::

   $ git status
   On branch master
   Changes to be committed:
     (use "git reset HEAD <file>..." to unstage)
     
           modified:   file.txt

   $ git stash
   $ git status
   On branch master
   nothing to commit, working tree clean

.. note::

   Při takovémto vyčištění aktuální větve se lze bez problému přepnout na
   jinou větev, aniž by došlo k nějaké kolizi.

.. tip::

   Při uložení stavu větve defaultně Git neumí schovat i ``Untracked`` soubory.
   Pro zamezení tohoto chování je třeba použít volbu ``-u``:

      $ git stash -u

stash list
""""""""""

Zobraz seznam uložených stavů::

   $ git stash list
   stash@{0}: WIP on master: 9172924 Add file.txt

stash pop
"""""""""

Vrať konkrétní uložený stav větve a zároveň smaž daný stash::

   $ git stash pop stash@{0}
   On branch master
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git checkout -- <file>..." to discard changes in working directory)

      modified:   file.txt

   no changes added to commit (use "git add" and/or "git commit -a")
   Dropped refs/stash@{0} (a0eaf5fd566b8093738316de94eaa43381a02e0d)

.. note::

   Při navrácení stavu větve defaultně Git neumí ponechat soubory i ve stavu
   ``Tracked``, neboť je vždy vrátí o úroveň níž. Pro zamezení tohoto chování
   je třeba použít volbu ``--index``::

      $ git stash pop stash@{0} --index
      On branch master
      Changes to be committed:
        (use "git reset HEAD <file>..." to unstage)

              modified:   file.txt

      Dropped refs/stash@{0} (dab54976af669f4933e4d5ac5441b5faed27d923)

.. tip::

   Bez uvedení reference na konkrétní stash se vrátí naposled uložený stav::

      $ git stash pop

stash drop
""""""""""

Odstraň konkrétní uložený stash::

   $ git stash drop stash@{0}

stash clear
"""""""""""

Odstraň všechny uložené stashe::

   $ git stash clear
   $ git stash list
   $

merge
^^^^^

Spoj obsah aktuální větve s nějakou jinou větví::

   $ git merge <název_větve>

Odbočka ke konfliktům
"""""""""""""""""""""

git mergetool vimdiff

git config --global merge.tool vimdiff

Vzdálené repozitáře
-------------------

remote
^^^^^^

Zobraz seznam vzdálených repozitářů::

   $ git remote
   origin

Odbočka ke vzdáleným repozitářům
""""""""""""""""""""""""""""""""

origin

remote -v
^^^^^^^^^

Zobraz podrobně seznam vzdálených repozitářů::

   $ git remote -v
   origin   https://daviebadger@gitlab.com/daviebadger/notes.git (fetch)
   origin   https://daviebadger@gitlab.com/daviebadger/notes.git (push)

remote add
""""""""""

Přidej vzdálený repozitář do Gitu::

   $ git remote add origin https://daviebadger@gitlab.com/daviebadger/notes.git

.. note::

   Příkaz se dá použít v situaci, kdy se nejprve vytvořil lokální repozitář
   bez klonování pomocí ``git init``. V tomto repozitáři už jsou nějaké soubory
   a je třeba mít vzdálený repozitář, kam se budou nahrávat změny.

remote show
"""""""""""

Zobraz informace o daném vzdáleném repozitáři::

   $ git remote show origin
   * remote origin
   Fetch URL: https://daviebadger@gitlab.com/daviebadger/configs.git
   Push  URL: https://daviebadger@gitlab.com/daviebadger/configs.git
   HEAD branch: master
   Remote branch:
     master tracked
   Local branch configured for 'git pull':
     master merges with remote master
   Local ref configured for 'git push':
     master pushes to master (up to date)

remote rename
"""""""""""""

remote remove
"""""""""""""

fetch
^^^^^

pull
^^^^

Stáhní ze vzdáleného repozitáře obsah dané větve a tu sluč s aktuální větví,
ve které se nacházím::

   $ git pull origin master

push
^^^^

Nahrej na vzdálený repozitář nějakou větev::

   $ git push origin master

Nahrej na vzdálený repozitář nějaký tag::

   $ git push origin v0.1.0

.. tip::

   Nahrávání master větve lze zkrátit příkazem ``git push -u origin master``,
   pomocí kterého půjde nahrávat master větev zkráceným způsobem::

      $ git push

   Ostatní větve bude třeba nahrávat standardním způsobem::

      $ git push origin <název_větve>

TODO
====

* git clean
* git log --graph u větví a merge requestů
* git reset HEAD~
* smazání remote tagu
* checkout tagů
* git reflog
* git branch --set-upstream master origin/master
* git rebase
* workflow
* blame
* změna zprávy u commitu a tagu
