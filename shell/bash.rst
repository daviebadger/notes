======
 Bash
======
--------------------------------------------------
 Unixový shell pro interpretaci příkazového řádku
--------------------------------------------------

.. contents:: Obsah:

Příkazový řádek
===============

Pro práci s příkazovým řádkem je třeba mít nějaký terminálový emulátor (dále
jen terminál).

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
~         aktuální poloha disku (~ je zkratka pro "/home/davie")
$         normální uživatel (# je superuživatel alias root)
<příkaz>  prostor pro příkaz(y)
========  ======

.. note::

   Pro budoucí ukázky příkazů se bude používat zkrácený zápis::

      $ <příkaz>

Popis syntaxe příkazu
---------------------

V prvé radě se musí jednat o příkaz, který existuje. Pokud tomu tak není,
Bash vypíše chybovou hlášku::

   $ ahoj
   ahoj: command not found

V druhé řadě je třeba vědět, jak se daný příkaz používá a jaké jsou jeho
možnosti použití. Pokud to nevím, mohu si zobrazit manuál k danému příkazu
pomocí příkazu "man"::

   $ man man

.. note::

   Příkaz "man" zobrazil manuál pro příkaz "man", tedy sám sobě. V zobrazeném
   manuálu lze stisknout písmenko "h" pro nápovědu, jak lze daný manuál
   ovládat a písmenko "q" naopak manuál zavře.

   Manuál má zpravidla každý Unixový příkaz. Nicméně v počítači mohou existovat
   i příkazy, které jsem si sám vytvořil nebo nainstaloval. U těchto příkazu
   nelze moc očekávat, že budou mít taktéž manuál, viz níže o nápovědě.

Další variantou je zobrazení nápovědy pomocí volby / přepínače / parametru
"--help"::

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

Do budoucna je ještě vhodné vědět, že příkaz může mít subpříkazy a že i
volbám lze někdy dát argument.

.. note::

   Význam jednotlivých příkazů bude vysvětlen později.

.. tip::

   Více zkrácených voleb lze sloučit do jedné velké volby, např. u příkazu
   "ls" to může být místo "ls -l -a":

      $ ls -la

Ovládání příkazového řádku
--------------------------

Šipkami vlevo a pravo lze pohybovat mezi napsanými znaky na řádku. Klávesa
ENTER pak samotný příkaz spustí.

Šipkami nahoru a dolu lze procházet historii použitých příkazů. Nahoru dále
do minulosti a dolu zpátky do přítomnosti.

.. tip::

   Historii lze také zobrazit příkazem "history"::

      $ history
          1  ahoj
          2  man
          3  man --help

   Příkazům je vždy přiřazeno číslo podle pořádí, ve kterém byly spušteny od
   začátku používání příkazového řádku. Pokud chci spustit znovu nějaký příkaz
   z historie, mohu napsat::

      $ !2

Pro ukončení práce s příkazovým řádkem (zavření terminálu) existuje příkaz
"exit"::

   $ exit

.. note::

   Další možností ovládání příkazového řádku lze najít v sekci
   `Klávesové zkratky`_.

   Pak ještě existují další klávesové zkratky, které používá samotný terminál.
   Může se jednat o kopírování a vkládání textu (klasické CTRL + C / CTRL + V
   nefunguje), zobrazení více oken terminálu najednou atd.

Příkazy
=======

Navigace
--------

Odbočka k souborovému systému
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pro práci se soubory a adresáři (složkami) je třeba vědět, kde na disku se
nacházejí, abych na mě mohl eventuálně zavolat nějaký příkaz.

Operační systémy postavené na Unixu, jako je třeba Linux mají jeden velký
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
       david   můj domovský adresář
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
       local   prostor pro programy, které uživatelem nainstalované
       share   dokumentace k předinstalovaných programům
     var/      prostor pro aplikační data
       cache   místo pro ukládání cache paměti
       lib     prostor pro ukládání dynamických dat
       log     místo pro ukládání logů

pwd
^^^

Ukaž aktuální pracovní prostředí, ve kterém se nacházím::

   $ pwd
   /home/davie

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

ls -a (ls --all)
""""""""""""""""

Ukaž obsah adresáře včetně skrytých souborů a adresářů (začínají na tečku)::

   $ ls -a
   .  ..  .bash_history

.. note::

   Samotná tečka znamená aktuální adresář a dvě tečky nadžený adresář (viz níže
   v sekci `Odbočka k absolutním a relativním cestám`_.

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
8          TODO
davie      jméno uživatele, který vlastní daný objekt
davie      jméno skupiny, která vlastní daný objekt
4096       velikost objektu v bajtech
dub 15     datum poslední změny
22:58      čas poslední změny
Documents  jméno objektu
=========  ======

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

   Volbu "-h" nejde použít samostatně, musí být vždy užita s volbou "-l".

ls -lhS
"""""""

Ukaž podrobnejší obsah adresáře spolu s lidsky srozumitelnými velikostmi a
objekty seřaď od největší velikosti po nejmenší::

   $ ls -lhS
   -rw-r--r-- 1 davie davie  13K dub 27 21:39 bash.rst
   -rw-rw-r-- 1 davie davie 2,2K dub 24 21:55 tilix.rst

.. note::

   Volbu "-S" lze použít samostatně.

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

   Po vypsání nějaké částí cesty lze dvakrát stisknout TAB, který pak zobrazí
   veškeré možnosti, kam mohu změnit adresář::

      $ cd D
      Desktop/ Documents/ Downloads/

   Taktéž se může stát, že po prvním stisknutí TAB se automaticky doplní cesta.

TODO
====

* less

Klávesové zkratky
=================

Kurzor
------

* CTRL + a

  * skočí na začátek řádku::

       $ ls -l
         <-----

* CTRL + e

  * skočí na konec řádku::

       $ ls -l
         ----->

* ALT + f

  * skočí doprava o jedno slovo::

       $ ls --all --reverse
         -->
           ------>
                 ---------->
* ALT + b

  * skočí doleva o jedno slovo::

       $ ls --all --reverse
                    <-------
              <------
         <----

Text
----

Záměna textu
^^^^^^^^^^^^

* CTRL + t

  * zamění písmenko v místě kurzoru s předchozím::

       $ ls
           ^
       $ sl

* ALT + t

  * zamění slovo v místě kurzoru s předchozím::

       $ ls -l
              ^
       $ -l ls

* ALT + l

  * zamění znaky od kurzoru po konec slova na malá písmena::

       $ ls --REVERSE
           ^
       $ ls --reverse

* ALT + u

  * zamění znaky od kurzoru po konec slova na velká písmena::

       $ ls --all
           ^
       $ ls --ALL

* ALT + c

  * kapitalizuj (udělej větším) první písmo ve slově::

       $ ls --all --reverse
         -->
            ----->
                 ---------->
       $ Ls --All --Reverse

Mazání textu
^^^^^^^^^^^^

* CTRL + k

  * smaž text od kurzoru až na konec řádku::

       $ ls --all --reverse
                 ^
       $ ls --all

* CTRL + u

  * smaž text od kurzoru až na začátek řádku::

       $ ls --all --reverse
                           ^
       $

* ALT + d

  * smaž text od kurzoru až po konec slova, případně další slovo::

       $ ls --all --reverse
           ^
       $ ls --reverse

* CTRL + w

  * smaž text od kurzoru po začátek slova, případně předchozí slovo::

       $ ls --all --reverse
                 ^
       $ ls --reverse

Vkládání textu
^^^^^^^^^^^^^^

* CTRL + y

  * vložení v místě kurzoru předchozí smazaný text::

       $ ls -l
              ^
       $
       $ ls -l

Kontrola procesů
----------------

* CTRL + c

  * ukončí daný příkaz::

       $ ping localhost
       PING localhost (127.0.0.1) 56(84) bytes of data.
       64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.075 ms
       ^C
       --- localhost ping statistics ---
       1 packets transmitted, 1 received, 0% packet loss, time 0ms
       rtt min/avg/max/mdev = 0.075/0.075/0.075/0.000 ms

* CTRL + d

  * ukončí shell (zavře okno terminálu)
  * to samé jako příkaz::

       $ exit

* CTRL + Z

  * pozastaví běh příkazu::

       $ python3 -q
       >>>
       ^Z
       [1]+  Stopped                 python3 -q

  * seznam pozastavených příkazů lze zobrazit příkazem "jobs" a vrátit je do
    běhu pomocí "fg"

Ostatní
-------

* TAB

  * dvě stisknutí tabulátoru zobrazí možnosti, které lze použít jako argument::

       $ cd
            TAB TAB
       .cache/
       .config/
       .dbus/

  * jedno stisknutí se pak pokusí dokončit název souboru či adresáře, pokud
    to bude možné::

       $ cd Dow
              TAB
       $ cd Downloads

* CTRL + L

  * vyčístí obrazovku od předchozích příkazů a jejich výstupů
  * to samé jako příkaz::

       $ clear
