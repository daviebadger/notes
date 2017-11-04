======
 Bash
======
--------------------------------------------------
 Unixový shell pro interpretaci příkazového řádku
--------------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Příkazový řádek
===============

Pro práci s příkazovým řádkem je třeba mít nějaký emulátor terminálu, kde je
Bash nainstalovaný a nastavený jako výchozí shell (platí pro většinu OS
postavených na Unixu).

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
tyto podoby:

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

.. note::

   Některé příkazy níže jsou dostupné ve všech operačních systémech vycházejích
   z Unixu, jiné jen v Linuxu a jiné jen v konkrétní Linuxové distribuci
   (např. Ubuntu).

   Samotné Bash příkazy lze zobrazit příkazem ``help``::

      $ help

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
     etc       konfigurační soubory a skripty, které se spouštějí po bootování
     home/     domovské adresáře jednotlivých uživatelů mimo superužiatele
       davie   můj domovský adresář
     lib       dodatečné soubory (knihovny) pro běh systémových aplikací
     media     prostor, kam se automaticky připojí externí CD / USB aj.
     mnt       prostor, kam lze manuálně připojit externí zařízení
     opt       prostor pro volitelné systémové balíčky a komerční programy
     proc      virtuální prostor, kam kernel ukládá info o systému (procesech)
     root      domovský adresář roota
     sbin      systémové binárky pro roota (pro administrativní účely)
     tmp       dočasné uložiště pro soubory a adresáře, které se mažou po bootu
     usr/      místo pro programy nainstalované spolu s Linuxovou distribucí
       bin     spustitelné soubory pro běh předinstalovaných programů
       lib     dodatečné soubory (knihovny) pro běh předinstalovaných programů
       local   prostor pro programy, které jsou uživatelem nainstalované
       share   dokumentace k předinstalovaných programům
     var/      prostor pro aplikační data
       cache   místo pro ukládání cache paměti
       lib     prostor pro ukládání dynamických dat
       log     místo pro ukládání logů
       spool   místo pro ukládání front (tisk, emaily)

ls
^^

Ukaž obsah adresáře, ve kterém se nacházím::

   $ ls
   Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos

.. note::

   Adresáře by měly být zpravidla barevně odlišeny a soubory mít nějakou
   koncovku (ne vždy tomu tak musí být).

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
   * při použítí příkazu ``ls`` na odkaz ke zdrojovému adresáři bude výstup
     úplně stejný, jako bych tento příkaz spustil v samotném zdrojovém
     adresáři
   * pokud se zdrojový soubor nebo adresář smaže, tak odkaz bude vést na
     neexistující místo

ls -lh
""""""

Ukaž v podrobnější obsahu adresáře lidsky srozumitelné velikosti objektů
(znatelné jen u souborů)::

   $ ls -lh
   -rw-r--r-- 1 davie davie 13K dub 27 21:39 bash.rst

Legenda:

* K (KB)
* M (MB)
* G (GB)

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

.. note::

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

  * cesta se vypisuje od aktuální adresáře do cílové destinace bez ``/`` na
    začátku
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
   cesta, neboť žádná jiná alternativa neexistuje.

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

Koncovky jako ``.pdf`` aj. nejsou nezbytně nutné k pojmenování souborů. Systém
si sám zjistí podle obsahu souboru, o jaký typ souboru se jedná, nicméně
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

Odbočka k zástupným znakům
""""""""""""""""""""""""""

Při mazání lze vyfiltrovat, které soubory a adresáře se mají smazat. V rámci
této filtrace se používají zástupné znaky:

* ``*``

  * shoda s jakoukoliv kombinací znaků, přičemž ``*`` užita samostatně vezme
    všechny soubory a adresáře::

       $ rm -rfv *
       removed 'a'
       removed 'b'
       removed 'c'

  * další varianty:

    * ``d*``

      * jen ty soubory a adresáře, které začínají na písmenko ``d``

    * ``*d``

      * jen ty soubory a adresáře, které končí na písmenko ``d``

    * ``d*.txt``

      * jen ty soubory a adresáře, které začínají na písmenko ``d`` a končí na
        koncovku ``.txt``

* ``?``

  * zastoupí jakýkoliv znak, respektive znaky, pokud je použito více otazníků::

       $ rm -rf file.tx?
       removed 'file.txa'
       removed 'file.txb'
       removed 'file.txc'

* ``[]``

  * zastoupí jednou jen ty znaky, které jsou definované v hranatých závorkách::

       $ rm -rfv file.[abc]
       removed 'file.a'
       removed 'file.b'
       removed 'file.c'

  * pokud je za otevřenou hranatou závorkou ``!``, tak se zastoupí jakékoliv
    znaky vyjma znaků za ``!``::

       $ rm -rfv file.[!a]
       removed 'file.b'
       removed 'file.c'

  * ``[]`` lze několikrát opakovat za sebou::

       $ rm -rfv file.[ab][ab]
       removed 'file.aa'
       removed 'file.ab'
       removed 'file.ba'
       removed 'file.bb'

  * pro zastoupení abecedy se používá zkratka ``[a-z]``, respektive ``[A-Z]``
    a pro čísla ``[0-9]`` (lze je všechny kombinovat uvnitř jedných hranatých
    závorek, např. ``[a-zA-Z0-9]``)

.. note::

   Tato filtrace pomocí zástupných znaků lze použít i u jiných příkazů, jako
   je třeba ``ls``, ``mv`` či ``cp``.

mv
^^

Přejmenuj soubor nebo adresář::

   $ mv old.txt new.txt
   $ ls
   new.txt

Přesuň soubor nebo adresář na jiné místo::

   $ mv ~/new.txt .

Přesuň soubor nebo adresář na jiné místo a zároveň ho přejmenuj::

   $ mv dir/old.txt new.txt

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
výška terminálu::

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
   rovnou použít nějaký textový editor pro čtení souborů místo příkazu
   ``less``.

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

Přesměrování
------------

>
^

Přesměruj standardní výstup někam do souboru::

   $ ls
   a.txt  b.txt  c.txt
   $ ls > file.txt
   $ cat file.txt
   a.txt
   b.txt
   c.txt

.. note::

   Pokud už soubor ``file.txt`` existuje, tak přesměrovaný výstup přepíše obsah
   tohoto souboru.

   Pozor však na případ, kdy je přesměrován prázdný (žádný) výstup. V tomto
   případě se smaže celý obsah souboru, ale samotný soubor bude dále
   existovat::

      $ cat test.txt
      Hello
      $ > test.txt
      $ cat test.txt
      $

Odbočka ke standardním vstupům, výstupům a errorům
""""""""""""""""""""""""""""""""""""""""""""""""""

Standardním výstupem (stdout, 1) se rozumí nějaký výsledek, který se zobrazí
uživateli v terminálu. Typickém příkladem je výstup z příkazu ``ls`` z nějakého
existujícího adresáře::

   $ ls
   a.txt  b.txt  c.txt

Standardním errorem (stderr, 2) se rozumí nějaká chybová hláška, která se
taktéž zobrazí uživateli v terminálu. Typickým příkladem je použití neznámého
příkazu::

   $ blabla
   blabla: command not found

Standardním vstupem (stdin, 0) se pak rozumí nějaký text, který zadal uživatel
z klávesnice po vyzvání nějaké programu.

>>
^^

Přesměruj standardní výstup na konec souboru::

   $ cat file.txt
   Hello!
   $ echo Hi! >> file.txt
   $ cat file.txt
   Hello!
   Hi!

.. note::

   Příkaz ``echo`` pošle na standardní výstup daný text.

2>
^^

Přesměruj standardní error někam do souboru::

   $ cat blabla
   cat: blabla: No such file or directory
   $ cat blabla 2> /dev/null
   $

.. note::

   ``/dev/null`` je taková červí díra, kam když se cokoliv přesměruje, tak se
   nikdy neuloží::

      $ cat /dev/null
      $

Toto chybové přesměrování se nejčastěji používá spolu s ``>`` či ``>>``
přesměrováním::

   $ cat /etc/passwd > ~/passwords.txt 2> /dev/null

<
^

Přesměruj na standardní vstup obsah nějakého souboru::

   $ cat number.txt
   3
   $ cat print_number.py
   print(input("Number: "))
   $ python3 print_number.py < number.txt
   Number: 3

.. note::

   Pro více vyzvání (inputů) je třeba mít taktéž připraveno více hodnot
   v souboru (každá hodnota zvlášť na řádek).

<<
^^

Přesměruj na standardní vstup hodnotu(y), které sám manuálně napíšu::

   $ cat print_date.py
   print(input("Day: "))
   print(input("Month: "))
   print(input("Year: "))
   $ python3 print_date.py << EOF
   > 4
   > 5
   > 2017
   > EOF
   Day: 4
   Month: 5
   Year: 2017

.. note::

   Za ``>>`` je třeba napsat nějaký oddělovač, pomocí kterého půjde ukončit
   psaní hodnot. V tomto případě se jedná o text ``EOF`` (end of file). Taktéž
   lze použít klávesovou zkratku ``CTRL + d``.

Filtry
------

grep
^^^^

Zobraz jen ty řádky, na kterých se vyskytuje zadaný text::

   $ ls ~ | grep Doc
   Documents

.. note::

   ``grep`` příkaz lze použít i samostatně, nicméně je třeba mít nějaký
   soubor po ruce::

      $ grep Bash bash.rst
      Bash

Odbočka k rourám
""""""""""""""""

Roury ``|`` umí vzít standardní výstup nějakého příkazu a ten použít jako
standardní vstup pro jiný příkaz, např.::

   $ ls -l ~ | less

Alternativní zápis místo roury by zřejmě vypadal následovně::

   $ ls -l > output.txt
   $ less output.txt
   $ rm file.txt

grep -n
"""""""

Zobraz jen ty řádky, na kterých se vyskytuje zadaný text spolu s čísly řádků::

   $ grep -n Bash bash.rst
   2: Bash

grep -i
"""""""

Zobraz jen ty řádky, na kterých se vyskytuje zadaný text a nerozlišuj malá
a velká písmena::

   $ grep -i bAsH bash.rst
   Bash
   BASH

tee
^^^

Ulož standardní výstup z předchozí roury do souboru::

   $ ls -l ~ | tee output.txt | cat

S uloženými výstupy pak lze opětovně pracovat::

   $ cat output.txt

sort
^^^^

Seřaď abecedně řádky ze standardního vstupu či souboru::

   $ cat alphabet.txt
   c
   b
   a
   $ cat alphabet.txt | sort
   a
   b
   c
   $ sort alphabet.txt

uniq
^^^^

Odstraň duplicitu ze standardního vstupu či souboru::

   $ cat duplicity.txt
   car
   car
   $ cat duplicity.txt | uniq
   car
   $ uniq duplicity.txt

wc
^^

Zobraz počet řádku, slov a znaků ze standardního vstupu či souboru::

   $ cat file.txt | wc
    1  5 20 file.txt
   $ wc file.txt

wc -l
"""""

Zobraz jen počet řádků::

   $ wc -l file.txt
   1 file.txt

wc -w
"""""

Zobraz jen počet slov::

   $ wc -w file.txt
   5 file.txt

wc -c
"""""

Zobraz jen počet znaků::

   $ wc -c file.txt
   20 file.txt

Vyhledávání
-----------

find
^^^^

Vyhledej všechny soubory v nějakém adresáři včetně jeho vnořených adresářů::

   $ find ~

.. note::

   Často se ve spojení s příkazem ``find`` používá přesměřování pro standardní
   errory, aby se nenarušoval standardní výstup, pokud je někdě problém s
   oprávněním::

      $ find / 2> /dev/null

find -type
""""""""""

Vyhledej jen určité typy souborů v nějakém adresáři::

   $ find ~ -type d

Legenda:

===========  ======
Typ souboru  Význam
===========  ======
d            adresář
f            soubor
l            symbolický link
===========  ======

find -name
""""""""""

Vyhledej jen ty soubory, které odpovídájí danému jménu (patternu)::

   $ find ~ -type f -name "*.rst"

.. note::

   Při používání zástupných znaků je vhodné vždy celý pattern zaobalit do
   uvozovek, aby se příkaz ``find`` choval podle očekování.

find -size
""""""""""

Vyhledej soubory podle velikosti (``+`` vetší než, ``-m`` menší než)::

   $ find ~/Downloads -type f -size +1M

.. note::

   Pro vyhledání shodné velikosti se nepoužije žádný znak::

      $ find ~/Downloads -type f -size 45M

Legenda:

========  ======
Velikost  Význam
========  ======
k         KB
M         MB
G         GB
========  ======

find -exec
""""""""""

Spusť nějaký příkaz pro každý nalezený soubor::

   $ find . -exec rm -rf {} \; 2> /dev/null

.. note::

   Na místo ``{}`` se automaticky vloží cesta nalezeného souboru a ``\;`` značí
   konec řádku pro daný příkaz za ``-exec`` volbou.

.. tip::

   Pokud chci smazat jenom soubory jako takové, tak mohu použít zkratku a to
   volbu ``-delete``::

      $ find . -type f -delete

which
^^^^^

Najde spustitelný soubor, který je zodpovědný za daný příkaz::

   $ which python3
   /usr/bin/python3

Komprese a archivace
--------------------

gzip
^^^^

Zkompresuj rychle a snadno nějaký soubor::

   $ ls -lh
   -rw-r--r-- 1 davie davie  30K kvě  6 19:46 bash.rst
   $ gzip bash.rst
   $ ls -lh
   -rw-r--r-- 1 davie davie 9,9K kvě  6 19:46 bash.rst.gz

.. tip::

   Obsah zkompresovaných ``*.gz`` souborů lze přečíst příkazy ``zcat``,
   ``zmore`` nebo ``zless``.

gunzip
^^^^^^

Dekompresuj zkompresovaný ``.gz`` soubor::

   $ ls -lh
   -rw-r--r-- 1 davie davie 9,9K kvě  6 19:46 bash.rst.gz
   $ gunzip bash.rst.gz
   $ ls -lh
   -rw-r--r-- 1 davie davie  30K kvě  6 19:46 bash.rst

bzip2
^^^^^

Zkompresuj pomaleji, ale lépe nějaký soubor::

   $ ls -lh
   -rw-r--r-- 1 davie davie  30K kvě  6 19:46 bash.rst
   $ bzip2 bash.rst
   $ ls -lh
   -rw-r--r-- 1 davie davie 9,4K kvě  6 19:46 bash.rst.bz2

.. tip::

   Obsah zkompresovaných ``*.bz2`` souborů lze přečíst příkazy ``bzcat``,
   ``bzmore`` nebo ``bzless``.

bunzip2
^^^^^^^

Dekompresuj zkompresovaný ``.bz2`` soubor::

   $ ls -lh
   -rw-r--r-- 1 davie davie 9,4K kvě  6 19:46 bash.rst.bz2
   $ bunzip2 bash.rst.gz
   $ ls -lh
   -rw-r--r-- 1 davie davie  30K kvě  6 19:46 bash.rst

tar
^^^

Vytvoř archív s nebo bez komprese pro soubor(y) a adresář(e)::

   $ ls
   dir
   $ tar -cf dir.tar dir
   $ ls
   dir  dir.tar

Legenda:

=====  ======
Volba  Význam
=====  ======
c      vytvoř archív
f      archív jako soubor
j      bzip2 komprese / dekomprese
t      zobraz obsah archívu
x      rozbal archív
z      gzip komprese / dekomprese
=====  ======

.. note::

   Zkompresované archívy používají následující koncovky:

   * ``.tar.gz`` nebo ``.tgz``
   * ``.tar.bz2`` nebo ``.tbz``

Možnosti použití:

* vytváření archívů:

  * ``tar -cf dir.tar dir``
  * ``tar -czf dir.tgz dir``
  * ``tar -cjf dir.tbz dir``

* zobrazení obsahu archívů (soubory a adresáře):

  * ``tar -tf dir.tar``
  * ``tar -tf dir.tgz``
  * ``tar -tf dir.tbz``

* rozbalení archívů:

  * ``tar -xf dir.tar``
  * ``tar -xzf dir.tgz``
  * ``tar -xjf dir.tbz``

Vlastnictví a oprávnění k souborům
----------------------------------

chmod
^^^^^

Změn práva k souboru či adresáři::

   $ ls -l
   -rw-rw-r-- 1 davie davie     0 kvě  7 14:28 file.txt
   $ chmod 777 file.txt
   $ ls -l
   -rwxrwxrwx 1 davie davie     0 kvě  7 14:28 file.txt

.. note::

   ``777`` znamená, že vlastník, skupina a ostatní uživatelé (přesně v tomto
   pořadí) mají veškeré prává k souboru, tj. součet vah pro čtení (r), zápis
   (w) a průchod (x).

Odbočka k právům
""""""""""""""""

Práva k souborům obecně jsou rozdělena postupně do tří skupin:

1. oprávnění uživatele (vlastník souboru)
2. oprávnění skupiny (skupina vlastnící soubor)
3. oprávnění ostatních uživatelů, kteří nejsou ve vlastnické skupině

Každá tato skupinu může mít přidělena následující práva:

* ``r`` (váha 4)

  * možnost otevřít soubor a přečíst jeho obsah
  * v případě adresáře možnost zobrazit obsah adresáře

* ``w`` (váha 2)

  * možnost provést změny v souboru
  * v případě adresáře možnost vytvářet soubory, přejmenovávat je či mazat

* ``x`` (váha 1)

  * možnost spustit soubor jako program, pokud má požadovanou hlavičku
    (shebang)::

       $ cat hello.py
       #!/usr/bin/env python3
       print("Hello world!")
       $ python3 hello.py
       Hello world!
       $ ./hello.py
       Hello world!

  * v případě adresáře možnost procházet adresáři

Kromě vah lze práva měnit i slovním způsobem. U skupin se používá toto
pojmenování:

* ``u`` (uživatel)
* ``g`` (skupina)
* ``o`` (ostatní)
* ``a`` (všichni)

Ukázky:

* ``$ chmod a+x file.txt``

  * všichni budou mít právo pro průchod

* ``$ chmod o-w file.txt``

  * ostatní uživatelé nebudou mít právo pro zápis

* ``$ chmod u=rwx,o= file.txt``

  * uživatel (vlastník) bude mít maximální práva, ostatní žádné

chmod -R
""""""""

Zmeň rekurzivně práva v daném adresáří včetně jeho souborů a vnořených
adresářů::

   $ chmod -R a+x dir

chown
^^^^^

Změn vlastníka souboru::

   $ sudo chown root file.txt

Změn vlastnickou skupinu souboru::

   $ sudo chown :root file.txt

Změn uživatele i skupinu::

   $ sudo chown davie:davie file.txt

Odbočka k právům superuživatele
"""""""""""""""""""""""""""""""

Pro vykonání některých činností, např. změna vlastníka souboru nebo instalace
nového softwaru, je třeba mít taková práva, které mají jen privilegování
uživatele (root).

V tomto případě je třeba se buď přihlásit na roota, pokud znám jeho heslo,
vykonat danou činnost a pak se vrátit zpátky::

   $ su -
   Password:
   # chown root:root file.txt
   # exit
   $

Nebo použít prefix ``sudo`` před příkazem a dočasně si půjčit vyšší práva.
Právo použít ``sudo`` mají jen ti uživatelé, kteřým bylo toto právo přiděleno
rootem. U běžného PC může ``sudo`` používat první vytvořený uživatel.

.. note::

   Příkaz ``su`` slouží k přihlášení na jiného uživatele, pokud znám jeho
   heslo. Pokud není zmíněn žádný uživatel, tak se za uživatele považuje
   automaticky root. Volba ``-`` zároveň přepne i shell.

   Možnosti použití:

   * ``su``
   * ``su -``
   * ``su davie``
   * ``su - davie``

chown -R
""""""""

Změn rekurzivně vlastníka či skupinu v daném adresáři, včetně jeho souborů
a vnořených adresářů::

   $ sudo chown -R root:root dir

Procesy
-------

ps
^^

Zobraz seznam spuštěných procesů v daném terminálu::

   $ ps
     PID TTY          TIME CMD
    4061 pts/1    00:00:00 ps
   31540 pts/1    00:00:01 bash

Legenda:

=======  ======
Sloupec  Význam
=======  ======
PID      ID procesu
TTY      číslo terminálu (terminálů může být spuštěno více najednou)
TIME     kolik času potřeboval procesor pro vykonávání procesu
CMD      příkaz, který spustil daný proces
=======  ======

ps -u
"""""

Zobraz seznam všech procesů, které uživatel sám spustil, s podrobnějšími
informacemi::

   $ ps -u
   USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
   davie     4297  0.0  0.0  46992  3268 pts/1    R+   22:29   0:00 ps -u
   davie    31500  0.0  0.0  30220  2992 pts/0    Ss   19:38   0:00 -/bin/bash
   davie    31540  0.0  0.1  30356  4580 pts/1    Ss   19:38   0:01 -/bin/bash
   davie    31573  0.3  0.2  65808 10964 pts/0    S+   19:38   0:35 vim bash.rst

Legenda:

=======  ======
Sloupec  Význam
=======  ======
USER     pod kterým uživatelem běží daný proces
%CPU     na kolik % vytežuje daný proces procesor
%MEM     kolik % paměti spotřebovává proces
VSZ      velikost virtuální paměti v KB
RSS      reálná velikost použité paměti v KB
STAT     status procesu
START    od kdy proces běží
=======  ======

ps -ax
""""""

Zobraz seznam všech spuštěných procesů na počítači::

   $ ps -ax

jobs
^^^^

Zobraz procesy (joby) v rámci terminálu, které běží v popředí nebo pozadí
či jsou pozastavené::

   $ python3 -q
   >>>
   ^Z
   $ jobs
   [1]+  Stopped                 python3

.. note::

   Místo ``^Z`` je třeba zmáčknout klávesovou zkratku ``CTRL + z``, pomocí
   které se pozastaví proces.

fg
^^

Přesuň do popředí job na pozadí, případně obnov pozastavený job::

   $ fg
   x = 1
   >>> x
   1

.. note::

   Do popředí se přesune ten job, u kterého je znaménko ``+`` za ID jobu, např.
   ``[1]+``.

Pro ukončení Python konzole, což je další shell, je třeba stisknout klávesovou
zkratku ``CTRL + d``.

fg n
""""

Přesuň do popředí Ntý job::

   $ fg 1
   x = 1
   >>> x
   1

bg
^^

Přesuň pozastavený job na pozadí, čímž se job obnoví::

   $ ping localhost
   PING localhost (127.0.0.1) 56(84) bytes of data.
   64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.074 ms
   ^Z
   $ jobs
   [1]+  Stopped                 ping localhost
   $ bg
   64 bytes from localhost (127.0.0.1): icmp_seq=11 ttl=64 time=0.071 ms

Pokud job běží na pozadí, tak lze normálně psát příkazy jako obvykle, akorát
výsledek příkazu může skončít v záplavě standardních výstupů z procesu
běžícího na pozadí::

   64 bytes from localhost (127.0.0.1): icmp_seq=11 ttl=64 time=0.071 ms
   ls
   a.txt b.txt c.txt
   64 bytes from localhost (127.0.0.1): icmp_seq=11 ttl=64 time=0.071 ms

Nejrychlejší postup pro ukončení procesu na pozadí je přesunout ho na popředí
pomocí příkazu ``fg`` a následně použít klávesovou zkratku ``CTRL + c`` pro
ukončení procesu.

.. note::

   Příkaz ``ping`` slouží pro ověřování, že počítač může komunikovat s jiným
   počítačem. Počítač umí komunikovat i sám se sebou, pokud na místě IP adresy
   či domény je použito slovo ``localhost`` nebo IP ``127.0.0.1``.

.. tip::

   Proces v pozadí lze také spustit pomocí ``&`` na koncí řádku::

      $ ping localhost &

bg n
""""

Přesuň na pozadí Ntý job::

   $ bg 1

kill
^^^^

Ukonči daný proces::

   $ ps
     PID TTY          TIME CMD
    5131 pts/1    00:00:00 python3
    5142 pts/1    00:00:00 ps
   31540 pts/1    00:00:02 bash
   $ kill 5131

kill -9
"""""""

Ukonči násilně daný proces::

   $ kill -9 5131

.. note::

   V tomto případě program nebude mít šanci vykonát kód jako po běžném
   ukončení programu, např. uložení nějaké stavu.

Správa balíčku
--------------

Balíčky jsou speciální soubory (archívy) s koncovkou ``.deb`` (platí
pro Linuxové distribuce odvozené z Debianu), pomocí kterých
lze nainstalovat nový software.

apt
^^^

Příkaz do práci s balíčky v oficiálním repozitáři či uživatelsky spravovaným
repozitářích někde na internetu.

apt update
""""""""""

Vytáhní z repozitářů aktuální stav balíčků a případně informuj o možném
upgradu::

   $ sudo apt update

apt search
""""""""""

Vyhledej v repozitáři balíček(y), které odpovídájí danému názvu::

   $ apt search vim

apt show
""""""""

Zobraz informace o nějakém balíčku::

   $ apt show vim

apt install
"""""""""""

Nainstaluj nějaký baliček(y)::

   $ sudo apt install vim

.. tip::

   Balíček ``tree`` umí přehledněji zobrazit adresářovou strukturu::

      $ tree shell/
      shell/
      └── bash.rst

      0 directories, 1 file

apt upgrade
"""""""""""

Upgraduj nějaký balíček(y) na novou verzi::

   $ sudo apt upgrade vim

.. note::

   Pokud neni zmíněn žádný balíček, tak se systém pokusí upgradovat všechny
   balíčky, které je možné povýšit na vyšší verzi.

.. tip::

   Nejčastěji se upgrade používá v kombinaci s updatem::

      $ sudo apt update; sudo apt upgrade
      $ # nebo
      $ sudo apt update && sudo apt upgrade

   Pomocí středníku lze na jednom řádku spustit více příkazů za sebou, aniž by
   záleželo, jak dopadl předchozí příkaz. Pokud se příkazy spojují pomocí
   ``&&``, tak se další příkaz spustí jen tehdy, pokud příkaz předchozí proběhl
   v pořádku.

   ``#`` pak značí komentář, který Bash bude ignorovat. Pokud bude komentář či
   jakýkoliv jiný příkaz začínat s jednou mezerou na začátku jako prefix, tak
   se nebude ukládat do historie::

      $ # test
      $  # test
      $ history

apt remove
""""""""""

Odinstaluj nějaký balíček(y)::

   $ sudo apt remove vim

apt autoremove
""""""""""""""

Odinstaluj balíčky, které jsou nepotřebné::

   $ sudo apt autoremove

.. note::

   Jako nepotřebné balíčky se považují ty, které žádný z jiných balíčků
   nepotřebuje pro svůj běh.

dpkg
^^^^

Příkaz pro práci s balíčky, které jsou lokálně na disku.

dpkg -i
"""""""

Nainstaluj lokální balíček(y)::

   $ sudo dpkg -i vivaldi-stable_1.8.770.56-1_amd64.deb

.. note::

   Jakmile je balíček nainstalovaný, lze ho odstranit pomocí ``apt`` příkazu,
   je-li to třeba.

add-apt-repository
^^^^^^^^^^^^^^^^^^

Zaregistruj další repozitář s balíčky::

   $ sudo apt-add-repository ppa:user/repository

Místo ``user`` bude název uživatele či týmu, který spravuje svůj archív
repozitářů a místo ``repository`` bude konkrétní název repozitáře.

.. note::

   Po přidání repozitáře (PPA) je třeba zavolat ``apt update`` pro zjištění
   obsahu daného repozitáře.

add-apt-repository -r
"""""""""""""""""""""

Odstraň přidaný repozitář::

   $ sudo apt-add-repository -r ppa:user/repository

Vzdálený přístup
----------------

Na dálku se mohu připojit k nějakému počítači a přihlásit se pod uživatelem,
který v něm existuje. To vše za předpokladu, že vzdálený počítač má povolenou
danou komunikaci.

ftp
^^^

Nešifrovaný protokol pro přenos souborů::

   $ ftp ftp.ubuntu.com

.. note::

   Pro autentizaci uživatele se zpravidla používá jméno ``anonymous`` a
   libovolné heslo, jestli je vyžadováno.

Na vzdáleném počítači se pro navigaci používájí klasické příkazy ``pwd``,
``cd`` či ``ls``. Pro ukončení spojení pak ``exit``.

.. note::

   Seznam všech možných příkazů v rámci ftp lze zobrazit pomocí příkazu
   ``help``::

      ftp> help

get
"""

Zkopíruj soubor ze vzdáleného počítače ke mě::

   ftp> get file.txt

.. note::

   Soubor se zkopíruje na místo, kde jsem se nacházel před navázáním ftp
   spojení. Pokud potřebuji zkopírovat jinam, tak změnim u sebe aktuální
   pracovní prostředí pomocí ``lcd`` příkazu::

      ftp> lcd ~

mget
""""

Zkopíruj více souboru najednou ke mě::

   ftp> mget a.txt b.txt c.txt

put
"""

Zkopíruj soubor ode mě na vzdálený počítač::

   ftp> put file.txt

mput
""""

Zkopíruj více souborů ode mě na vzdálený počítač::

   ftp> mput a.txt b.txt c.txt

wget
^^^^

Stáhni soubor(y) odněkud::

   $ wget ubuntu.com
   $ ls
   $ index.html

ssh
^^^

Šifrovaně se připoj na vzdálený počítač pod stejným jménem::

   $ ssh x.x.x.x  # místo x.x.x.x bude platná IP adresa nebo název domény

Připoj se šifrovaně pod jiným jménem::

   $ ssh user@x.x.x.x

Na vzdáleném počítači pak provádím příkazy, které potřebuji. Pokud chci
vykonat jen jeden příkaz, tak ho mohu provést zkráceně::

   $ ssh user@x.x.x.x <příkaz>

Příkazem ``exit`` se pak odpojím.

.. note::

   Některé nakonfigurované SSH servery používájí místo hesel ssh klíče. Ty
   se vytvoří následujícím příkazem (výzvy stačí ignorovat)::

      $ ssh-keygen -t rsa
      $ # nebo náročněji a bezpečněji, jak je tomu u GitLabu
      $ ssh-keygen -t rsa -C "můj_email" -b 4096

   Ve složce ``~/.ssh`` pak vzniknou dva nové klíče, soukromný ``id_rsa`` a
   veřejný ``id_rsa.pub``. Obsah veřejného klíče se pak předá admistrátorovi
   ssh serveru nebo automaticky nahraje na ssh server příkazem::

      $ ssh-copy-id x.x.x.x

scp
^^^

Šifrované kopírování z nebo na ssh server::

   $ scp user@x.x.x.x:~/file.txt .  # z ssh serveru k sobě
   $ scp file.txt user@x.x.x.x:~    # od sebe na ssh server

.. note::

   ``scp`` se chová jako ``cp`` příkaz, tudíž pokud potřebuji kopírovat něco
   rekurzivně, použiju opět volbu ``-r``::

      $ scp -r dir user@x.x.x.x:/

sftp
^^^^

Šifrované verze ftp protokolu, přičemž princip ovládání je obdobný (místo
``ftp`` bude ``sftp``).

Ostatní příkazy
---------------

date
^^^^

Zobraz aktuální čas a datum v počítači::

   $ date
   Ne kvě  7 18:14:05 CEST 2017

Zobraz jen čas::

   $ date +"%T"
   18:15:14

Zobraz jen datum ve formátu ``DD-MM-YYYY``::

   $ date +"%d-%m-%y"
   07-05-17

cal
^^^

Zobraz kalendář pro aktuální měsíc::

   $ cal

Zobraz kalendář pro jiný měsíc v tomto roce::

   $ cal -m 4

Zobraz kalendář pro konkrétní měsíc v konkrétním roce::

   $ cal -m 4 1995

Zobraz kalendář pro tento rok::

   $ cal -y

Zobraz kalendář pro konkrétní rok::

   $ cal -y 1995

df -h
^^^^^

Zobraz informaci o využití diskového prostoru::

   $ df -h

time
^^^^

Změř, jak dlouho trvalo vykonání příkazu::

   $ time find ~ -type f -name "*.rst" 2> /dev/null

   real  0m0,134s
   user  0m0,024s
   sys   0m0,048s

Řádek s ``real`` časem uvádí celkovou dobu trvání příkazu.

uname -a
^^^^^^^^

Zobraz informace o systému (operační systém, verze kernelu, architektura
procesoru aj.)::

   $ uname -a
   Linux badger 4.10.0-20-generic #22-Ubuntu SMP Thu Apr 20 09:22:42 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux

uptime
^^^^^^

Zobraz informaci, jak dlouho běží počítač::

   $ uptime
    18:26:02 up 2 days, 19:58,  1 user,  load average: 1,79, 1,45, 1,15

Proměnné v shellu
-----------------

V shellu jsou uložené proměnné, se kterými pracuji nějaké programy.

Typický příklad z reálného světa může být, že se program podívá, zda existuje
daná proměnná a zda ji je přirazena nějaká hodnota. Podle této hodnoty se pak
rozhodne, co má udělat (např. načtení správného konfiguračního souboru).

export
^^^^^^

Vypiš veškeré proměnné spolu s hodnotami::

   $ export

Taktéž vytvoř novou proměnnou s nebo bez hodnoty::

   $ export test
   $ export TEST="Hello world!"

.. note::

   Stejný postup bude použit i pro změnu hodnoty.

Zobrazit hodnoty konkrétní proměnné lze pomocí příkazu ``echo``::

   $ echo $TEST
   Hello world!

unset
^^^^^

Smaž konkrétní proměnnou::

   $ unset test

Konfigurační soubor
===================

Ještě předtím, než se přípraví příkazový řádek, tak Bash hledá konfigurační
soubory, kde mohou být uložené různé nastavení, aliasy, proměnné, které
jsou nezbytné pro práci s příkazovým řádkem.

Jedním z konfiguračních souborů je ``~/.bashrc``::

   $ less ~/.bashrc

Jakmile se změní obsah tohoto souboru, je třeba ho znovu načíst pomocí příkazu
``source``::

   $ source ~/.bashrc

Aliasy
------

Pokud je nějaký příkaz dlouhý nebo je těžký na zapamatování, tak si mohu
vytvořit alias(y)::

   $ which here             # zda příkaz existuje
   $ alias here="pwd"
   $ here
   /home/davie/
   $ unalias here
   $ here
   here: command not found

.. note::

   Do konfiguračního souboru ``.bashrc`` budu tedy psát::

      alias here="pwd"

   Aliasy lze psát separátně do souboru ``.bash_aliases``. pokud se v
   konfiguračním souboru se nachází následující podmínka::

      if [ -f ~/.bash_aliases ]; then
          . ~/.bash_aliases
      fi

Proměnné
--------

Proměnné, kterou jsou vlastnoručně definované pomocí příkazu ``export`` vždy
zaniknou po odhlášení uživatele či vypnutí počítače. Aby tyto proměnné
existovaly trvale, je třeba si je uložit do konfiguračního souboru::

   export test=test

Změna vzhledu příkazového řádku
-------------------------------

V proměnné ``PS1`` je uloženo nastavení, jak ma vypadat ve výchozím stavu
příkazový řádek, viz::

   davie@badger:~$ <příkaz>

Pokud se mi tento prompt (PS1) nelíbí, tak si mohu nastavit jiné zobrazení,
např. abych viděl i datum. Na změnu promptu je napsán tutoriál na stránce:

https://www.cyberciti.biz/tips/howto-linux-unix-bash-shell-setup-prompt.html

Klávesové zkratky
=================

Kurzor
------

* ``CTRL + a``

  * skoč na začátek řádku::

       $ ls -l
         <-----

* ``CTRL + e``

  * skoč na konec řádku::

       $ ls -l
         ----->

* ``ALT + f``

  * skoč doprava o jedno slovo::

       $ ls --all --reverse
         -->
           ------>
                 ---------->

* ``ALT + b``

  * skoč doleva o jedno slovo::

       $ ls --all --reverse
                    <-------
              <------
         <----

Text
----

Záměna textu
^^^^^^^^^^^^

* ``CTRL + t``

  * zaměn písmenko v místě kurzoru s předchozím::

       $ ls
         <--
       $ sl

* ``ALT + t``

  * zaměn slovo v místě kurzoru s předchozím::

       $ ls -l
         <-----
       $ -l ls

* ``ALT + l``

  * zaměn znaky od kurzoru po konec slova na malá písmena::

       $ ls --REVERSE
           ---------->
       $ ls --reverse

* ``ALT + u``

  * zaměn znaky od kurzoru po konec slova na velká písmena::

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

  * ukonči daný proces::

       $ ping localhost
       PING localhost (127.0.0.1) 56(84) bytes of data.
       64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.075 ms
       ^C
       --- localhost ping statistics ---
       1 packets transmitted, 1 received, 0% packet loss, time 0ms
       rtt min/avg/max/mdev = 0.075/0.075/0.075/0.000 ms

* ``CTRL + z``

  * pozastav běh procesu::

       $ python3 -q
       >>>
       ^Z
       [1]+  Stopped                 python3 -q

* ``CTRL + d``

  * ukonči shell, pokud je nějaký další otevřen (např. Python interpret) nebo
    zavři samotný terminál

Ostatní
-------

* ``TAB``

  * dvě stisknutí tabulátoru zobrazí buď možnosti relativných cest, pokud je
    za příkazem ještě mezera nebo bez mezery další možné příkazy::

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

  * vyčísti obrazovku od předchozích příkazů a jejich výstupů
  * stejného výsledku lze docílit příkazem::

       $ clear
