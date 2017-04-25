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

   |     |      || |

   > název přihlášeného uživatele

         |      || |

         > název počítače

                || |

                > aktuální poloha disku (~ je zkratka pro "/home/davie")

                 | |

                 > normální uživatel (# je superuživatel alias root)

                   |

                   > prostor pro příkaz(y)

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

   /          Hlavní kořen (root).
    bin       Binárky a skripty pro nastartování (boot) a běh (run) systému.
    boot      Soubory a adresáře pro Linoxé jádro (spojka mezi HW a SW).
    cdrom     Prostor pro připojení obsahu CD disku.
    dev       Speciální místo, kde jádro spravuje zařízení (disk, USB aj.).
    etc       Konfigurační soubory a skripty, které se pouštějí po bootování.
    home/     Domovské adresáře jednotlivých uživatelů mimo superužiatele.
      david   Můj domovský adresář.
    lib       Dodatečné soubory (knihovny) pro běh systémových aplikací.
    media     Prostor, kam se automaticky připojí externí CD / USB aj.
    mnt       Prostor, kam lze manuálně připojit externí zařízení.
    opt       Prostor pro volitelné systéové balíčky a komerční programy.
    proc      Virtuální prostor, kam kernel ukládá info o systému (procesech).
    root      Domovský adresář roota.
    sbin      Systémové binárky pro roota (pro administrativní účely).
    tmp       Dočasný uložitě pro soubory a adresáře, které se maže po bootu.
    usr/      Místo pro programy nainstalované spolu s Linuxovou distribucí.
      bin     Spustitelné soubory pro běh předinstalovaných programů.
      lib     Dodatečné soubory (knihovny) pro běh předinstalovaných programů.
      local   Prostor pro programy, které uživatelem nainstalované.
      share   Dokumentace k předinstalovaných programům.
    var/      Prostor pro aplikační data.
      cache   Místo pro ukládání cache paměti.
      lib     Prostor pro ukládání dynamických dat.
      log     Místo pro ukládání logů.

pwd
^^^

Ukaž aktuální pracovní prostředí, ve kterém se nacházím::

   $ pwd
   /home/davie

cd
^^

Změn aktuální pracovní prostředí na jiné::

   $ cd /
   $ pwd
   /

Cestu do jiného adresáře lze uvést dvěmi způsoby:

1. absolutní cestou

   * cesta se vypisuje od kořene (roota) do cílové destinace::

        $ cd /home/davie

2. relativní cestou

   * cesta se vypisuje od aktuální adresáře do cílové destinace::

        $ cd /
        $ cd home/davie/

   * cesta do podřazeného / vnořeného / dětského začíná vždy názvem adresáře,
     který se nachází v aktuálním pracovním prostředí, viz předchozí příkaz
   * cesta do nadřazeného / rodičovského adresáře se provadí pomocí dvou
     teček::

        $ cd
        $ cd ..
        $ pwd
        /home
        $ cd ..
        $ pwd
        /
        $ cd
        $ cd ../../home/davie

     .. note::

        Není problém se dostat pomocí teček do nadřazeného adresáře a z něho
        do vedlejšího / sourozeneckého adresáře.

     .. tip::

        Další zkratkou vedle dvou teček je ~ (alias pro domovský adresář)::

           $ cd ~/Downloads
           $ pwd
           /home/davie/Downloads

Daná absolutní nebo relativní cesta musí existovat, jinak se vypíše chybová
hláška::

   $ cd /dneska/je/pondeli
   bash: cd: /dneska/je/pondeli: No such file or directory

Když nepoužiju žádnou cestou, tak se změní aktuální pracovní prostředí na
místo s domovským adresářem, což je i výchozí stav po zapnutí terminálu::

   $ pwd
   /
   $ cd
   $ pwd
   /home/davie

.. tip::

   Pokud se potřebuji vrátit do předchozí adresáře, ve kterém jsem byl, tak
   mohu napsat::

      $ cd -
      $ pwd
      /home/davie

ls
^^

Ukaž obsah adresáře::

   $ ls
   Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos

Pokud není "ls" příkazu zadaný argument, tak zobrazí obsah adresáře, ve kterém
se aktuálně nacházím. Avšak, jestliže uvedu nějakou platnou absolutní nebo
relativní cestu, tak ukáže obsah daného cílového adresáře::

   $ ls /home
   davie

Tento příkaz umí taky zobrazit obsah vícero adresářů najednou, stačí mu jen
zadat více argumentů::

   $ ls /home /home/davie
   /home:
   davie

   /home/davie:
   Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos

Také se může stát, že v daném adresáři nejsou žádné soubory a vnořené adresáře,
tak příkaz "ls" nic nezobrazí. Nicméně existují ještě skryté soubory, které
tento příkaz defaultně nezobrazí, pokud není k tomu vyzván.

Průzkum adresáře
----------------

ls (podrobněji)
^^^^^^^^^^^^^^^

Chování, respektive výstup "ls" příkazu lze ovlivnit pomocí přepínaču / voleb
(option). Ty jsou buď ve zkracené (pomlčka a písmenko) nebo zdlouhavé variantě
(dvě pomlčky a text)::

   $ ls -l
   total 36
   drwxr-xr-x 2 davie davie 4096 dub 13 21:34 Desktop
   drwxr-xr-x 8 davie davie 4096 dub 15 22:58 Documents
   drwxr-xr-x 2 davie davie 4096 dub 16 16:02 Downloads
   $ ls --help
   Usage: ls [OPTION]... [FILE]...
   List information about the FILEs (the current directory by default).
   Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Více zkracených přepínačů lze spojit do jednoho velkého přepínače::

   $ ls -l -a
   total 2136
   drwx------ 20 davie davie    4096 dub 17 13:35 .
   drwxr-xr-x  4 root  root     4096 dub 13 20:40 ..
   -rw-------  1 davie davie    7450 dub 16 22:51 .bash_history
   -rw-r--r--  1 davie davie     220 dub 13 20:40 .bash_logout
   -rw-r--r--  1 davie davie    3771 dub 13 20:40 .bashrc
   $ ls -la
   total 2136
   drwx------ 20 davie davie    4096 dub 17 13:35 .
   drwxr-xr-x  4 root  root     4096 dub 13 20:40 ..
   -rw-------  1 davie davie    7450 dub 16 22:51 .bash_history
   -rw-r--r--  1 davie davie     220 dub 13 20:40 .bash_logout
   -rw-r--r--  1 davie davie    3771 dub 13 20:40 .bashrc

Naopak zdlouhavé přepínače je třeba psát odděleně za sebou::

   $ ls -l --all --reverse
   total 2140
   -rw-------  1 davie davie 1886357 dub 17 14:11 .xsession-errors
   -rw-------  1 davie davie      51 dub 13 20:46 .Xauthority
   -rw-------  1 davie davie    2141 dub 16 16:33 .viminfo

.. note::

   Zkrácená varianta může, ale i nemusí mít zdlouhavou variantu. To samé platí
   i opačně. Seznam těchto možných přepínačů si lze zobrazit pomocí nápovědy
   k danému příkazu:

   * příkazem "man"::

        $ man ls

   * přepínačem "--help"::

        $ ls --help

.. note::

   Zdlouhavým přepínačům lze i zadat argumenty, pokud je to povoleno. Např.
   pro aktivaci / deaktivaci barevného rozlišení souborů, adresářů aj. by to
   bylo::

      $ ls -l --color=yes
      $ ls -l --color=no

   Pokud by se někdy v budoucnu stalo, že je třeba mít víceslovný argument
   nebo v něm použít speciální znaky, aniž by nezmočnili funkčnost příkazu,
   tak je vhodné argument (pokud se nejedná o číslo) zaobalit do složených
   či jednoducých závorek::

      $ ls -l --color="yes"

   To samé platí i pro argumenty bez použití přepínače.

ls -l
"""""

Zobrazí zdlouhavý výpis obsahu dané adresáře včetně dalších informací::

   $ ls -l
   drwxr-xr-x 8 davie davie 4096 dub 15 22:58 Documents
   ^^  ^  ^   ^ ^     ^     ^    ^            ^
   ||  |  |   | |     |     |    |            |
   ---> Zda se jedná o složku (d) nebo soubor (-) nebo link (l).
    |  |  |   | |     |     |    |            |
    |  |  |   | |     |     |    |            |
    ---> Oprávnění vlastníka objektu (rwx).
       |  |   | |     |     |    |            |
       |  |   | |     |     |    |            |
       ---> Opravnění pro členy skupiny, která vlastní daný objekt (r-x).
          |   | |     |     |    |            |
          |   | |     |     |    |            |
          ---> Opravnění ostatních uživatelů (r-x).
              | |     |     |    |            |
              | |     |     |    |            |
              ---> TODO.
                |     |     |    |            |
                |     |     |    |            |
                ---> Jméno vlastníka objektu (uživatele).
                      |     |    |            |
                      |     |    |            |
                      ---> Jméno skupiny, které vlastní daný objekt.
                            |    |            |
                            |    |            |
                            ---> Velikost objektu v bajtech.
                                 |            |
                                 |            |
                                 ---> Datum a čas poslední změny objektu.
                                              |
                                              |
                                              ---> Název objektu.

ls -a
"""""

Zobrazí obsah dané adresáře včetně skrytých souborů a adresářů, které začínají
tečkou::

   $ ls -a
   .
   ..
   .bash_history

Samotná tečka značí aktuální adresář a dvě tečky nadřazený adresář (hodně se
používá ve spojitosti s "cd" příkazem). Pokud nechci vidět tyto samostatné
tečky, použiju místo malého písmenka "a" velké::

   $ ls -A
   .bash_history
   .bash_logout
   .bashrc

Manipulace se soubory a adresáři
--------------------------------


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