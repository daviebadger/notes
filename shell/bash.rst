======
 Bash
======
--------------------------------------------------
 Unixový shell pro interpretaci příkazového řádku
--------------------------------------------------

.. contents:: Obsah:

Příkazový řádek
===============

Pro práci s příkazovým řádkem je třeba mít nějaký emulátor terminálu, kde je
Bash nainstalovaný a nastavený jako výchozí shell.

Popis příkazové řádku
---------------------

Po spuštení terminálu vypadá zpravidla první řádek následovně::

   davie@badger:~$ <příkaz>

Legenda:

========  ======
Text      Význam
========  ======
davie     název přihlášeného uživatele
badger    název počítače
~         aktuální poloha disku (``~`` je zkratka pro ``/home/davie``)
$         normální uživatel (``#`` je superuživatel alias root)
<příkaz>  prostor pro příkaz(y)
========  ======

.. note::

   Pro budoucí ukázky příkazů se bude používat zkrácený zápis::

      $ <příkaz>

Popis syntaxe příkazu
---------------------

V prvé radě se musí jednat o příkaz, který existuje. Pokud tomu tak není, Bash
vypíše chybovou hlášku::

   $ ahoj
   ahoj: command not found

V druhé řadě je třeba vědět, jak se daný příkaz používá a jaké jsou jeho
možnosti použití. Pokud to nevím, mohu si zobrazit manuál k danému příkazu
pomocí příkazu ``man``::

   $ man man

.. note::

   Příkaz ``man`` zobrazil manuál pro příkaz ``man``, tedy sám sobě. V
   zobrazeném manuálu lze stisknout písmenko ``h`` pro nápovědu, jak lze daný
   manuál ovládat a písmenko ``q`` naopak manuál zavře.

   Manuál má zpravidla každý Unixový příkaz. Nicméně v počítači mohou existovat
   i příkazy, které jsem si sám vytvořil nebo nainstaloval. U těchto příkazu
   nelze moc očekávat, že budou mít taktéž manuál, viz níže o nápovědě.

Další variantou je zobrazení nápovědy pomocí volby / přepínače / parametru
``--help``::

   $ man --help

Z nápovědy by mělo jít vyčíst, jaké jsou možnosti příkazu. Může se jednat o
tyto podoby::

1. příkaz samostatně::

   $ pwd

2. příkaz s argumentem::

   $ cd /home/davie

3. příkaz s vícero argumenty::

   $ mkdir dir1 dir2 dir3

4. příkaz s volbou::

   $ cp --version

5. příkaz s vícero volbami spolu s argumentem::

   $ rmdir dir/dir --parents --verbose

6. příkaz s vícero zkrácenými volbami::

   $ ls -l -a

Do budoucna je ještě vhodné vědět, že příkaz může mít subpříkazy, a že i
volbám lze někdy dát argument(y).

.. note::

   Význam jednotlivých příkazů bude vysvětlen později.

.. tip::

   Více zkrácených voleb lze sloučit do jedné velké volby, např. u příkazu
   ``ls`` to může být místo ``ls -l -a``::

      $ ls -la

Ovládání příkazového řádku
--------------------------

Šipkami vlevo a pravo lze pohybovat mezi napsanými znaky na řádku. Klávesa
``ENTER`` pak samotný příkaz spustí.

Šipkami nahoru a dolu lze procházet historii použitých příkazů. Nahoru dále
do minulosti a dolu zpátky do přítomnosti.

.. tip::

   Historii lze také zobrazit příkazem ``history``::

      $ history
          1  ahoj
          2  man
          3  man --help

   Příkazům je vždy přiřazeno číslo podle pořádí, ve kterém byly spušteny od
   začátku používání příkazového řádku. Pokud chci spustit znovu nějaký příkaz
   z historie, mohu napsat::

      $ !2

Pro ukončení práce s příkazovým řádkem (zavření terminálu) existuje příkaz
``exit``::

   $ exit

.. note::

   Další možností ovládání příkazového řádku lze najít v sekci
   `Klávesové zkratky`_.

   Pak ještě existují další klávesové zkratky, které používá samotný terminál.
   Může se jednat o kopírování a vkládání textu (klasické ``CTRL + C`` a
   ``CTRL + V`` nefunguje), zobrazení více oken terminálu najednou atd.

Příkazy
=======

Navigace
--------

pwd
^^^

Ukaž aktuální pracovní prostředí, ve kterém se nacházím::

   $ pwd
   /home/davie

Odbočka k souborovému systému
"""""""""""""""""""""""""""""

Pro práci se soubory a adresáři (složkami) je třeba vědět, kde na disku se
nacházejí, abych na mě mohl eventuálně zavolat nějaký příkaz.

Operační systémy postavené na Unixu, jako je třeba Linux, mají jeden velký
souborý systém nezávisle na počtu disků či připojených zařízení (rozdíl oproti
diskům C, D aj. ve Windows).

Tento souborový systém je nějakým způsobem hierarchicky uspořádaný a každý
soubor či adresář mají své patřičné místo. Nejvýše položenému místu se říka
kořen (root).

Ukázková struktura souborového systému::

   /           hlavní kořen (root)
     bin       binárky a skripty pro nastartování (boot) a běh (run) systému
     boot      soubory a adresáře pro Linoxé jádro (spojka mezi HW a SW)
     cdrom     prostor pro připojení obsahu CD disku
     dev       speciální místo, kde jádro spravuje zařízení (disk, USB aj.)
     etc       konfigurační soubory a skripty, které se pouštějí po bootování
     home/     domovské adresáře jednotlivých uživatelů mimo superužiatele
       davie   můj domovský adresář
     lib       dodatečné soubory (knihovny) pro běh systémových aplikací
     media     prostor, kam se automaticky připojí externí CD / USB aj
     mnt       prostor, kam lze manuálně připojit externí zařízení
     opt       prostor pro volitelné systéové balíčky a komerční programy
     proc      virtuální prostor, kam kernel ukládá info o systému (procesech)
     root      domovský adresář roota
     sbin      systémové binárky pro roota (pro administrativní účely)
     tmp       dočasný uložitě pro soubory a adresáře, které se maže po bootu
     usr/      místo pro programy nainstalované spolu s Linuxovou distribucí
       bin     spustitelné soubory pro běh předinstalovaných programů
       lib     dodatečné soubory (knihovny) pro běh předinstalovaných programů
       local   prostor pro programy, které jsou uživatelem nainstalované
       share   dokumentace k předinstalovaných programům
     var/      prostor pro aplikační data
       cache   místo pro ukládání cache paměti
       lib     prostor pro ukládání dynamických dat
       log     místo pro ukládání logů

ls
^^

Ukaž obsah adresáře, ve kterém se nacházím::

   $ ls
   Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos

.. note::

   Adresáře by měly být zpravidla barevně odlišeny a soubory mít nějakou
   koncovku.

Pro zobrazení obsahu obsah jiného adresáře musím uvést cestu do daného
adresáře::

   $ ls /home

Samozřejme si lze zobrazit obsah vícero adresářů najednou::

   $ ls /home /home/davie
   /home:
   davie

   /home/davie:
   Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos

ls -a
"""""

Ukaž obsah adresáře včetně skrytých souborů a adresářů (začínají na tečku)::

   $ ls -a
   .  ..  .bash_history

.. note::

   Samotná tečka znamená aktuální adresář a dvě tečky nadřazený adresář, viz
   níže v sekci `Odbočka k absolutním a relativním cestám`_.

ls -l
"""""

Ukaž delší (podrobnejší) obsah adresáře::

   $ ls -l
   drwxr-xr-x 8 davie davie 4096 dub 15 22:58 Documents

Legenda:

=========  ======
Text       Význam
=========  ======
d          zda se jedná o adresář (d), soubor (-) nebo symbolický odkaz (l)
rwxr-xr-x  oprávnění pro vlastníka, skupinu, ostatní uživatele
8          počet pevných odkazů na soubor nebo počet vnořených adresářů
davie      jméno uživatele, který vlastní daný objekt
davie      jméno skupiny, která vlastní daný objekt
4096       velikost objektu v bajtech
dub 15     datum poslední změny
22:58      čas poslední změny
Documents  jméno objektu
=========  ======

Odbočka k odkazům
"""""""""""""""""

Existují dva typy odkazů:

1. pevný odkaz (jen mezi soubory)

   * soubor může odkazovat na jiný soubor v jiném adresáři, příčemž jakákoliv
     změna obsahu v jednom z těchto souborů se projeví i v tom druhém
   * pokud se jeden soubor smaže, obsah druhého souboru zůstane stále zachován

2. symbolický odkaz (soubory i adresáře)

   * soubor nebo adresář může odkazovat na jiný zdrojový soubor nebo adresář
     na stejném či jiném místě na disku, což může vypadat při ``ls -l`` výpisu
     následovně::

        lrwxrwxrwx 1 davie davie 1 dub 29 20:22 Dokumenty -> /home/davie/Documents/

   * tento symbolický odkaz (prakticky soubor) v sobě uchovává jenom cestu do
     zdrojového souboru nebo adresáře
   * napr. při použítí příkazu ``ls`` na odkaz ke zdrojovému adresáři bude
     výstup úplně stejný, jako bych tento příkaz spustil v samotném zdrojovém
     adresáři
   * pokud se zdrojový soubor nebo adresář smaže, tak odkaz bude vést na
     neexistující místo

ls -lh
""""""

Ukaž v podrobnější obsahu adresáře lidsky srozumitelné velikosti objektů
(znatelné jen u souborů)::

   $ ls -lh
   -rw-r--r-- 1 davie davie 13K dub 27 21:39 bash.rst

Legenda::

* K == KB
* M == MB
* G == GB

.. note::

   Volbu ``-h`` nejde použít samostatně, musí být vždy užita s volbou ``-l``.

ls -lhS
"""""""

Ukaž podrobnejší obsah adresáře spolu s lidsky srozumitelnými velikostmi a
objekty seřaď od největší velikosti po nejmenší::

   $ ls -lhS
   -rw-r--r-- 1 davie davie  13K dub 27 21:39 bash.rst
   -rw-rw-r-- 1 davie davie 2,2K dub 24 21:55 tilix.rst

ls -lt
""""""

Ukaž podrobnější obsah adresáře a objekty seřaď podle poslední změny::

   $ ls -lt

cd
^^

Změn aktuální pracovní prostředí na jiné::

   $ cd /
   $ pwd
   /

Bez argumentů se změní pracovní prostředí zpátky na domovský adresář::

   $ cd
   $ pwd
   /home/davie

Do domovské adresáře se lze taky dostat pomocí vlnovky::

   $ cd ~
   $ pwd
   /home/davie

.. tip::

   Pokud se potřebuji vrátit do adresáře, ve kterém jsem byl předtím, tak jako
   argument použiju pomlčku::

      $ cd -
      $ pwd
      /

Odbočka k absolutním a relativním cestám
""""""""""""""""""""""""""""""""""""""""

* absolutní cesta

  * cesta se vypisuje od kořene (/) do cílové destinace::

       $ cd /home/davie

* relativní cesta

  * cesta se vypisuje od aktuální adresáře do cílové destinace
  * cesta do podřazeného adresáře začíná vždy názvem adresáře, který se
    nachází v aktuálním pracovním prostředí::

       $ cd Downloads

  * cesta do nadřazeného adresáře se provadí pomocí dvou teček (lze opakovat,
    pokud jsou tečky od sebe odděleny lomítkem)::

       $ cd ..

.. tip::

   Po vypsání nějaké částí cesty lze dvakrát stisknout ``TAB``, který pak
   zobrazí veškeré možnosti, kam mohu změnit adresář::

      $ cd D
            TAB TAB
      Desktop/ Documents/ Downloads/

   Taktéž se může stát, že po prvním stisknutí ``TAB`` se automaticky doplní
   cesta.

Práce s adresáři a soubory
--------------------------

mkdir
^^^^^

Vytvoř adresář(e) v aktuálním pracovním prostředí či na jiném místě::

   $ mkdir dir1
   $ mkdir dir2 dir3
   $ mkdir ~/dir4
   $ ls
   dir1  dir2  dir3  dir4

.. note::

   Vlastní adresáře a potažmo i soubory se zpravidla vytváří uvnitř domovského
   adresáře, neboť v tomto prostoru má uživatel téměř veškerá oprávnění a
   nepotřebují být rootem.

mkdir -p
""""""""

Vytvoř zárověň i nadřazené adresáře, pokud neexistují::

   $ mkdir -p ~/parent/child

.. note::

   Předchozí příkaz je zkrácený postup namísto těchto příkazů::

      $ cd
      $ mkdir parent
      $ cd parent
      $ mkdir child

rmdir
^^^^^

Smaž prázdný adresář(e)::

   $ rmdir dir1
   $ rmdir dir2 dir3

rmdir -p
""""""""

Smaž prázdný adresář(e) včetně nadřazených adresářů (ty zároveň nesmí obsahovat
žádné další adresáře a soubory)::

   $ rmdir -p parent/child

touch
^^^^^

Vytvoř prázdný soubor(y)::

   $ touch a.txt
   $ touch b.txt c.txt
   $ ls
   a.txt  b.txt  c.txt

Odbočka k souborům
""""""""""""""""""

Soubory jsou citlivé na malá a velká písmena, tudíž soubor ``file.txt`` není
to samé jako ``File.txt``, neboť se jedná o dva zcela odlišené soubory.

Koncovky jako ``.pdf`` aj. nejsou nezbytně nutné k pojmenování souborů. systém
si sám zjistí podle obsahu souboru, o jaký typ souboru se jedná. Nicméně
standardem je používat koncovky pro odlišení od adresářů.

V neposlední řádě je třeba vědět, že všechno v Unixu / Linuxu je soubor. I
adresáře jsou speciálním typem souboru. Lze se o tom přesvědčit příkazem
``file``::

   $ file bash.rst . ..
   bash.rst: UTF-8 Unicode text
   .:        directory
   ..:       directory

rm
^^

Smaž navždy soubor(y)::

   $ rm a.txt b.txt c.txt

rm -r
"""""

Smaž navždy i adresář(e) včetně jeho obsahu::

   $ rm -r dir1

.. note::

   Pokud vypisuji delší absolutní či relativní cestu, tak se smaže poslední
   vnořený adresář::

      $ rm -r ~/davie/parent/child/

   Zde se smaže adresář ``child`` a předchozí cesta ``~/davie/parent/`` bude
   stále existovat.

rm -rf
""""""

Smaž navždy soubor(y) i adresář(e) a ignoruj neexistující soubor(y) a
adresář(e)::

   $ rm -r dir1
   rm: cannot remove 'dir1': No such file or directory
   $ rm -rf dir1
   $

mv
^^

Přejmenuj soubor nebo adresář::

   $ mv bad.txt good.txt
   $ ls
   good.txt

Přesuň soubor nebo adresář na jiné místo::

   $ mv ~/good.txt .

Přesuň soubor nebo adresář na jiné místo a zároveň ho přejmenuj::

   $ mv dir/bad.txt good.txt

.. note::

   Bash umí sám vyhodnotit, zda došlo k přejmenování nebo přesunutí nebo k
   obojím najednou.

cp
^^

Zkopíruj soubor::

   $ cp origin.txt copy.txt

Zkopíruj soubor na jiné místo, a případně i přejmenuj, je-li to třeba::

   $ cp origin.txt ~/dir/
   $ cp origin.txt ~/dir/copy.txt

Zkopíruj soubory na jiné misto::

   $ cp a.txt b.txt c.txt dir/

cp -r
"""""

Zkopíruj celý adresář včetně jeho obsahu::

   $ cp -r dir1/ dir2/

cp -ru
""""""

Zkopíruj jen ty soubory a adresáře, které v cílové destinaci ještě neexistují
nebo naopak existují v zastaralé podobě::

   $ cp -ru dir1/* dir2/

O průběhu kopírování se moho přesvědčit pomocí volby ``-v``, která ukáže, jaké
soubory a adresáře se skutečně zkopírovaly::

   $ cp -ruv dir1/* dir2/
   'dir1/b.txt' -> 'dir2/b.txt'
   'dir1/dir3' -> 'dir2/dir3'

.. note::

   ``*`` je zástupný znak pro označení všech souborů a adresářů.

ln
^^

Vytvoř pevný odkaz mezi soubory::

   $ ln a.txt b.txt

.. note::

   Princip je stejný jako u kopírování.

ln -f
"""""

Vytvoř pevný odkaz navzdory tomu, že cílové jméno objektu už existuje::

   $ ln -f a.txt b.txt

ln -s
"""""

Vytvoř symbolický odkaz mezi soubory či adresáři::

   $ ln -s dir1/ ~/davie/Downloads

Čtení textových souborů
-----------------------

.. note::

   Jiné zakódováné či zkompilované (binární) soubory půjdou stěží přečíst,
   neboť budou absolutně nesrozumitelné.

cat
^^^

Vypiš obsah souboru(ů)::

   $ cat a.txt
   Toto je obsah souboru a.txt.
   $ cat b.txt
   Toto je obsah souboru b.txt.
   $ cat a.txt b.txt
   Toto je obsah souboru a.txt.
   Toto je obsah souboru b.txt.

Nevýhodou příkazu ``cat`` je, že je třeba vždy scrollovat nahoru do historie,
pokud je obsah souboru větší než samotná obrazovka terminálu.

Větší problém pak nastává v případě, kdy je obsah souboru tak velký, že
už se ani pomocí scrollování nedá dostat na jeho začátek, neboť brouzdání
do historie má své limity.

tac
^^^

Vypiš obráceně obsah souboru(ů)::

   $ cat file.txt
   První řádek.
   Druhý řádek.
   $ tac file.txt
   Druhý řádek.
   První řádel.

more
^^^^

Taktéž vypiš obsah souboru, nicméně ho vystránkuj, pokud je obsah větší než
velikost obrazovky::

   $ more bash.rst

Základní ovládání stránkovaného obsahu:

* ``h``

  * zobraz nápovědu k ovládání stránkovacího režimu

* ``SPACE`` (mezerník)

  * vypiš další stránku

* ``q``

  * ukonči stránkovací režim

Nevýhodou příkazu ``more`` je, že se nedají zobrazit předchozí stránky, pokud
není scrollováno nahoru do historie. U scrollování pak platí stejné limity jako
u příkazu ``cat``.

less
^^^^

Vystránkuj obsah souboru zvlášť ve čtecím režimu::

   $ less bash.rst

.. note::

   Na rozdíl od chování příkazu ``more`` se nebude nic vypisovat v terminálu.

Základní ovládání čtecího režimu:

* ``h``

  * zobraz nápovědu k ovládání čtecího režimu

* ``SPACE`` (mezerník) nebo ``f``

  * zobraz další stránku

* ``b``

  * zobraz předchozí stránku

* ``q``

  * ukonči čtecí režim

.. note::

   K ovládání lze použít i některé příkazy z textového editoru Vi(m), případně
   rovnou použít textový editor pro čtení souborů místo příkazu ``less``.

head
^^^^

Vypiš jen prvních deset řádků ze souboru::

   $ head numbers.txt
   1
   2
   3
   4
   5
   6
   7
   8
   9
   10

head -n
"""""""

Vypiš jen Ntý počet řádků ze souboru::

   $ head -3 numbers.txt
   1
   2
   3

tail
^^^^

Vypiš posledních deset řádků ze souboru::

   $ tail numbers.txt
   11
   12
   13
   14
   15
   16
   17
   18
   19
   20

tail -n
"""""""

Vypiše jen Ntý počet posledních řádků ze souboru::

   $ tail -3 numbers.txt
   18
   19
   20

TODO
====

* find
* grep
* kill
* ps
* tar
* wc
* < > |
* other:

   * cal
   * df
   * diff
   * which

Klávesové zkratky
=================

Kurzor
------

* ``CTRL + a``

  * skočí na začátek řádku::

       $ ls -l
         <-----

* ``CTRL + e``

  * skočí na konec řádku::

       $ ls -l
         ----->

* ``ALT + f``

  * skočí doprava o jedno slovo::

       $ ls --all --reverse
         -->
           ------>
                 ---------->
* ``ALT + b``

  * skočí doleva o jedno slovo::

       $ ls --all --reverse
                    <-------
              <------
         <----

Text
----

Záměna textu
^^^^^^^^^^^^

* ``CTRL + t``

  * zamění písmenko v místě kurzoru s předchozím::

       $ ls
         <--
       $ sl

* ``ALT + t``

  * zamění slovo v místě kurzoru s předchozím::

       $ ls -l
         <-----
       $ -l ls

* ``ALT + l``

  * zamění znaky od kurzoru po konec slova na malá písmena::

       $ ls --REVERSE
           ---------->
       $ ls --reverse

* ``ALT + u``

  * zamění znaky od kurzoru po konec slova na velká písmena::

       $ ls --all
           ------>
       $ ls --ALL

* ``ALT + c``

  * kapitalizuj (udělej větším) první písmo ve slově::

       $ ls
         -->
       $ Ls

Mazání textu
^^^^^^^^^^^^

* ``CTRL + k``

  * smaž text od kurzoru až na konec řádku::

       $ ls --all
           ------>
       $ ls

* ``CTRL + u``

  * smaž text od kurzoru až na začátek řádku::

       $ ls --all
         <--------
       $

* ``ALT + d``

  * smaž text od kurzoru až po konec slova, případně další slovo::

       $ ls --all --reverse
           ----->
       $ ls --reverse

* ``CTRL + w``

  * smaž text od kurzoru po začátek slova, případně předchozí slovo::

       $ ls --all --reverse
           <-----
       $ ls --reverse

Vkládání textu
^^^^^^^^^^^^^^

* ``CTRL + y``

  * vložení v místě kurzoru předchozí smazaný text, např. pomocí ``CTRL + u``::

       $ ls -l
         <-----
       $
       $ ls -l

Kontrola procesů
----------------

* ``CTRL + c``

  * ukončí daný proces::

       $ ping localhost
       PING localhost (127.0.0.1) 56(84) bytes of data.
       64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.075 ms
       ^C
       --- localhost ping statistics ---
       1 packets transmitted, 1 received, 0% packet loss, time 0ms
       rtt min/avg/max/mdev = 0.075/0.075/0.075/0.000 ms

* ``CTRL + z``

  * pozastaví běh procesu::

       $ python3 -q
       >>>
       ^Z
       [1]+  Stopped                 python3 -q

  * seznam pozastavených procesů lze zobrazit příkazem ``jobs`` a vrátit je do
    běhu pomocí příkazu ``fg``

* ``CTRL + d``

  * ukončí shell, pokud je nějaký další otevřen (např. Python interpret) nebo
    zavře samotný terminál

Ostatní
-------

* ``TAB``

  * dvě stisknutí tabulátoru zobrazí buď možnosti relativných cest, pokud je
    za příkazem ještě mezera nebo mezery další možné příkazy::

       $ cd
            TAB TAB
       a/ b/ c/
       $ cd
           TAB TAB
       cd                 cd-fix-profile     cd-it8
       cd-create-profile  cd-iccdump

  * jedno stisknutí se pak pokusí dokončit název souboru či adresáře, pokud
    to bude možné::

       $ cd Dow
              TAB
       $ cd Downloads

* ``CTRL + l``

  * vyčístí obrazovku od předchozích příkazů a jejich výstupů
  * stejného výsledku lze docílit příkazem::

       $ clear
