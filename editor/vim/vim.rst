=====
 Vim
=====
---------------------------------------
 Textový editor zabudovaný v terminálu
---------------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

Příkazem::

   $ sudo apt install vim

.. note::

   Defaultně v Ubuntu už je Vim nainstalovaný, nicméně se jedná o osekanější
   verzi kvůli zpětně kompatibilitě s editorem ``vi``. Ten se pro zajímavost
   spustí stejnojmenným příkazem::

      $ vi

Základní ovládání
=================

Otevření a zavření editoru
--------------------------

Vim se spustí také stejnojmenným příkazem::

   $ vim

Pro zavření Vimu je třeba napsat na klávesnici::

   :q

.. note::

   Pokud se v editoru nedopatřením objevil nějaký nový text, tak je třeba pro
   jistotu stisknout klávesu ``ESC`` a poté jej zavřít násilným způsobem (bez
   uložení)::

      :q!

Odbočka k módům
^^^^^^^^^^^^^^^

Ve Vimu jsou zavedené tzv. módy, pomocí kterých se editor patřičně ovládá. Ty
nejzákladnější jsou:

1. Normal

   * výchozí stav po spuštení Vimu
   * slouží pro navigaci v textu nebo pro přepínání na jiný mód, přičemž z
     jiného módu se zpátky na ``NORMAL`` mód přepne pomocí klávesy ``ESC``

2. Insert

   * mód pro vkládání textu do souboru
   * zapne se zpravidla stisknutím písmenka ``i``, po kterém lze začít
     psát či editovat text

3. Command-line

   * mód pro ovládání editoru jako takového pomocí příkazů
   * editor se ovládá z příkazového řádku, který se objeví po stisknutí
     dvojtečky ``:`` (viz zavření Vimu pomocí ``:q``)

Otevření souboru
----------------

Příkazem ``vim`` lze i otevřít nějaký existující nebo neexistující soubor:: 

   $ vim test.txt

Soubor jde také otevřit až uvnitř Vimu pomocí příkazu ``:e`` a uvedení cesty k
souboru::

   $ :e ~/Documents/test.txt

Pro začátek psaní do souboru je třeba přejít do ``INSERT`` módu pomocí písmenka
``i`` a začít psát či editovat text. Po skončení editace je vhodné se vrátit
zpět do ``NORMAL`` módu pomocí ``ESC``.

.. tip::

   Pomocí klávesové zkratky ``CTRL + d`` se ukážou veškeré možné cesty, které
   jdou použít pro dostání se k souboru::

      :e ~/Do
           CTRL + d
      Documents/  Downloads/
   
   Klávesa ``TAB`` pak automaticky dokončí cestu, je-li to možné. Pokud se
   doplnila špatná cesta, tak opětovným stiskem ``TAB`` klávesy se vybere
   další možná cesta v pořádí. Zpětně se vybírá cesta pomocí ``SHIFT + TAB``.

Uložení změn do souboru
-----------------------

Pro uložení změn je třeba použít příkaz ``:w`` v ``NORMAL`` módu::

   :w

.. note::

   Pokud jsem otevřel prázdný Vim nebo neexistující soubor, tak je třeba ještě
   uvést název souboru, pod kterým se má uložit::

      :w ~/Documents/test.txt

Jestliže je třeba existující soubor uložit pod jiným názvem, tak se použije
příkaz ``:sav``::

   :sav /cesta/k/souboru

.. tip::

   V jednom kroku lze najednou uložit změny a zavřít editor::

      :wq

Navigace v textu
================

Cvičný text::

   Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur nostrud
   quaeque eu, an his hendrerit prodesset, nonumes oportere gloriatur qui
   ut. Cu malis summo saperet nec, eam ei purto fastidii sententiae. Graece
   detracto reformidans ex mel. At oportere moderatius ius, sea at scripta
   regione dissentiunt.

   Vel no ferri aeterno deleniti. Ne eam nisl dissentiunt comprehensam, ea
   accusata vulputate mea. Ne duo assum meliore tincidunt, ius option
   molestiae et. Magna porro lucilius ea mea. Tota malorum ut vis, vim id
   posse civibus praesent.

   Quot cibo eloquentiam eum id, tation mentitum consectetuer pri ad. Ei mel
   exerci explicari, equidem aliquando nec et, an sed assum hendrerit. Id
   vel modus philosophia. Ea quo dicant minimum, choro scaevola ex mel. Tale
   vide nostrum ei usu, his illum scriptorem te. Ex legere cotidieque pro,
   quo nisl dolor assentior an, et iriure scripta blandit per.

.. note::

   Tento text se vloží do Vimu uvnitř ``INSERT`` módu za použití klávesové
   zkratky ``CTRL + SHIFT + v``.

Základní pohyb po znacích a řádcích
-----------------------------------

Šipkami vlevo a vpravo, respektive písmenky ``h`` a ``l`` se posune kurzor
o jeden znak do strany. Šipkami nahoru a dolu, respektive písmenky ``k`` a
``h`` se posunu kurzor o řádek v daném směru, viz schéma::

         ^
         k
   < h       l >
         j
         v

Při podržení klávesy se kurzor začne automaticky pohybovat daným směrem až
do uvolnění klávesy. Taktéž lze pohnout kurzorem najednou o Ntý počet znaků do
stran či o Ntý počet řádků nahoru nebo dolu.

Ukázky:

* ``3k``

  * o tři řádky nahoru

* ``5j``

  * o pět řádků dolu

* ``10l``

  * o 10 znaků doprava na řádku

* ``10h``

  * o 10 znaků doleva na řádku

Skoky
-----

Skok po slovu
^^^^^^^^^^^^^

* ``w`` (``W``)

  * skoč na začátek dalšího slova (může být i interpunkční znaménko)::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
       ------>

  * pro ignorování interpunkčních znaků je třeba použít ``W``::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
                             ------>

* ``e`` (``E``)

  * skoč na konec aktuálního nebo dalšího slova::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
       ---->
           ------>

* ``b`` (``B``)

  * skoč na začátek aktuálního nebo předchozího slova::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
             <----
       <------

Stejně jako u pohybu po znacích či řadcích, i zde lze posunout kurzor o Ntý
počet slov, např. ``3w``, ``5e`` aj.

.. tip::

   Pro posunutí kurzoru na konec předchozího slova se použije ``ge``,
   respektive ``gE``::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
           <------

Skok na konkrétní slovo
^^^^^^^^^^^^^^^^^^^^^^^

* ``/pattern`` + ``ENTER``

  * najdi v textu napravo od kurzoru až po konec souboru výskyt daného patternu
    a skoč na něj::

       /sit
       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
       ------------------>

  * pokud bylo nalezeno více výskytů odpovídajících danému patternu, tak se
    na další výskyt skočí pomocí ``n`` a na předchozí ``N``::

       /i
       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
       ------>
             ------------->
             <-------------
       <------

* ``?pattern`` + ``ENTER``

  * najdi v textu nalevo od kurzoru až po začátek souboru výskyt daného
    patternu
  * taktéž lze použít ``n`` a ``N``, avšak zde bude účinek opačný

Oba dva způsoby jsou defaultně citlivé na rozdíl velkých a malých písmen. Pro
vypnutí této citlivosti je třeba na konec patternu napsat suffix ``\c``::

   /pattern\c
   ?pattern\c

.. note::

   Tyto způsoby se spíše používájí na vyhledávání v textu, než na skákání jako
   takové.

Skok na kraj řádku
^^^^^^^^^^^^^^^^^^

* ``0``

  * skoč na začátek řádku::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
       <--------------------------

* ``$``

  * skoč na konec řádku::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
                                 --------------------------->

.. tip::

   Pokud řádek začíná odsazením, tak na začátek odsazeného textu se posune
   kurzor pomocí ``^``::

         <-------------------------
         Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur
      nostrud quaeque eu, an his hendrerit prodesset, nonumes oportere
      gloriatur qui ut.

Skok na konkrétní řádek
^^^^^^^^^^^^^^^^^^^^^^^

* ``gg`` (``1G``)

  * skoč na začátek souboru, tedy první řádek::

       ^ Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur
       | nostrud quaeque eu, an his hendrerit prodesset, nonumes oportere
         gloriatur qui ut.

* ``2G``

  * skoč na druhý řádek v souboru::

       | Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur
       v nostrud quaeque eu, an his hendrerit prodesset, nonumes oportere
         gloriatur qui ut.

* ``G``

  * skoč na konec souboru, tedy poslední řádek::

       | Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur
       | nostrud quaeque eu, an his hendrerit prodesset, nonumes oportere
       v gloriatur qui ut.

.. note::

   Po tomhle pohybu bude vždy kurzor na začátku řádku, ačkoliv mohl být
   předtím někde jinde na řádku.

Skok na kraj okna
^^^^^^^^^^^^^^^^^

* ``L``

  * skoč na poslední řádek v okně (spodní kraj)

* ``H``

  * skoč na první řádek v okne (horní kraj)

.. tip::

   Doprostřed obrazovky se skočí pomocí ``M``.

Skok po oknu
^^^^^^^^^^^^

* ``CTRL + f``

  * skoč na další okno (přesne o tolik řádku, kolik se jich vleze do okna)

* ``CTRL + b``

  * skoč na předchozí okno

Pokud je třeba jen poloviční velikost, tak:

* ``CTRL + d``

  * skoč o půlku okna dolu

* ``CTRL + u``

  * skoč o půlku okna nahoru

Ostatní skoky
-------------

Odbočka k dalším vstupům do Insert módu
---------------------------------------

Teď, když umíme se pohybovat v textu, je dobré vědět o dalších možnostech,
jak si usnadnit vstup do Insert módu (kromě klasického "i"):

* a

  * na rozdíl od "i" nezačně Insert mód v místě, kde je kurzor, ale o
    jeden znak napravo
  * rozdíl bude patrný z následujícího příkladu::

       # Mějme v editoru pouze text "Vim", ke kterému chci dopsat text
       # " je super."

       Vim

       # Navigujeme kurzorem na konec řádku. Pokud bychom do Insert módu
       # vstoupili pomocí "i" a začali psát dovětek, vypadalo by to takhle:

       Vi je super.m

       # Naopak při stisku "a" se kurzor posune o jeden znak doprava za
       # písmenko "m" (vznikne mezera, která zanikne po stisku ESC,
       # jestliže nic nenapíšeme), pak lze v pořádku dopsat zbytek:

       Vim je super.

* A

  * kurzor skočí na konec řádku a interně stiskne "a", abychom mohli
    pokračovat v psaní nové věty či odentrovat na jiný řádek

* I

  * relativně opak stisku "A", kdy se kurzor přemístí na úplný začátek
    souboru

.. tip::

   Když před zmáčknutím "a" / "A" / "i" / "I" stisknu ještě nějaké číslo,
   tak to, co napíšu v Insert módu se tolikrát vloží do textu, když se vrátím
   zpět do Normal módu.

   Např. chci třikrát vložit písmenko "X"::

      3iX + ESC

Pokud chci při vstupu rovnou vložit i prázdný řádek, tak mám na výběr, zda
ho chci vložit:

a) o řádek výše, než je kurzor

   * stisknu "O" (velké o)
   * příklad::

        # Mám kurzor na prvním řádku souboru, který obsahuje větu:

        |U|čím se Vim.

        # Pokud stisknu "O", tak se celá věta posune na druhý řádek a první
        # řádek bude prázdný, kam se přesune i kurzor a mód bude klasiky
        # Insert.

        | |
        Učím se Vim.

b) o řádek níž

   * stisknu "o" (malé o), opak k předchozí variantě

Editace textu
=============

Občas se může stát, že provedete nějakou akci, které lituje a chtěli byste se
vrátít v čase zpátky nebo naopak vrátit z minulosti dopředu:

* u

  * odstraní poslední akci (může se jednat o příkaz či vložený text)
  * lze několikrát stisknout za sebou (přesne o tolik stisknutí se vrátí
    do minulosti)

* CTRL + r

  * vrátí se o jednu akci z minulosti dopředu (taktéž lze opakovat)

Co se týče jednotlivých editačních akcí (mazání, kopírování aj.) uvedených
níže v textu, tak ve většině případů lze skloubit speciální znaky pro danou
akci spolu s čísly a pohybovými znaky.

Syntaxe tedy bude vypadat následovně:

1. speciální_znak
2. číslo + speciální_znak
3. speciální_znak + pohybový_znak
4. speciální_znak + číslo + pohybový_znak

.. tip::

   Kdyby se náhodou stálo, že potřebuji několikrát zopakovat předchozí
   událost, tak stačí tolikrát stisknout ".". Např. místo trojíte stisku
   "u" mohu taktéž třikrát stisknout tečku.

Mazání textu
------------

Lze samozřejmě použít klasické klávesy pro mazání (backspace a delete), ale
je to zdlouhavý proces, pokud potřebuji mazat např. více znaků / slov / řádku
najednou.

Při použítí následujícíh způsobu mazání je třeba být klasicky v Normal módu.

Mazání po znacích
^^^^^^^^^^^^^^^^^

* x

  * smaže znak, který se nachází v místě kurzoru
  * když uvedu i číslo, tak smažu X znaků doprava::

       5x

Pro mazání více znaků doleva mimo klasické způsoby lze následovně::

   3dj

Toto smaže od aktuálního kurzoru 3 znaky nalevo. Pro smazání všech znaků až
na začátek / konec řádku to bude::

   d0
   d$

.. tip::

   Bylo by dobré vědět do budoucna, že písmenko "d" nejenom, že maže určitý
   úsek textu, ale taky tuto smaznou část si ještě zapamatuje. Toto se bude
   hodit do situaci, kdy je třeba vystřihnout text a přemístit ho jinam.

Mazání po slovech
^^^^^^^^^^^^^^^^^

Kombinace písmenka "d" spolu s písmenky "w" / "e" / "b" a případně i čísly
uprostřed mezi nimi.

Co se týče mazání slova, tak lze použít zkratku namísto skoku na nějaký kraj
a až pak smazat znaky na druhý kraj. Jde o::

   daw

.. tip::

   Kromě mazání slova (aw = a word) lze mazat i věty (as = a sentence) nebo
   celé odstavce (ap = a paragraph)::

      das
      dap

   Tyto zkratky se budou hodit i v kapitolce `Přepisování textu`_-

Mazání po řádcích
^^^^^^^^^^^^^^^^^

a) aktuální řádek

   * dd

     * smaže řádek, na kterém se nachází kurzor

b) od aktuálního řádku dolu

   * dj

     * smaže aktuální řádek a řádek pod ním

   * 3dd

     * smaže aktuální řádek a dva řádky pod ním

   * d + číslo_řádku + G

     * pokud je číslo_řádku větší než číslo řádku, na kterém se nacházím,
       tak maže řádky až po dané číslo_řádku

   * dG

     * až na konec souboru

c) od aktuálního řádku nahoru

   * dk

     * smaže aktuální řádek a řádek nad ním

   * d + číslo_řádku + G

     * pokud je číslo_řádku menší, než číslo aktuálního řádku, tak se maže
       až po daný řádek nahoru

   * dgg

     * až na začátek souboru

.. tip::

   Pokud bych měl nějaký zalomený text, např::

      Dnes je
      pondělí.

   a chtěl tuto větu spojit na jeden řádek spolu s přidáním mezery za slovo
   "je", tak mohu stisknout "J" kdekoliv na prvním řádku pro sjednocení
   s následujícím řádkem. Výsledek pak bude::

      Dnes je pondělí.

Mazání vymezené části textu
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Zde bude k zapotřebí si představit další mód a to Visual. Ten slouží pro
označení textu, se kterým chci dál pracovat. Mám na výběr ze dvou znaků:

* v

  * chci označovat po znacích
  * lze opět kombinovat s pohybovými znaky "h", "e", "$" atd.

* V

  * chci označovat po celých řadcích

Pokud potřebuji upravit začátek výběru textu a naopak konec, tak můžu mezi
těmito dvěmi místy skákat pomocí "o" (malé o).

.. note::

   Ve Visual módu má "o" jiný význam, než v Normal módu (jeden ze vstupů
   do Insert módu).

Dále ještě existuje speciální varianta označení textu a to pomocí CTRL + v,
kde se jedná o takový sloupcový výběr. Příklad::

   # Mějme následující text, ve kterém chci změnit najednou mezery na
   # dvojtečky.

   01 45
   05 00
   08 24

   # Kurzorem najedu na místo první mezery, stisknu CTRL + v a dvojitým
   # kliknutím "j" označím i dva řádky pod tím.

   01| |45
   05| |00
   08| |24

   # Stisknu "r" pro náhrazení znaku (bude probráno za chvíli) a zmáčknu ":".
   # Text nyní bude vypadát následovně:

   01:45
   05:00
   08:24

Nyní zpět k mazání. Pro smazání označeného textu stisknu klasicky "d" nebo i
"x".

.. tip::

   Pro práci s označeným textem se může hodit do budoucnosti vědět i o
   dalších speciálních znacích, které jdou stisknout ve Visual módu:

   * >

     * posune (odsadí) text doprava o jeden tabulátor.

   * <

     * posune text doleva o jeden tabulátor

   * ~

     * změní označení text na opačnou velikost písma. např. pokud nějaké
       písmenko  bylo malé, tak se změní na velké a naopak

Přepisování textu
-----------------

Zkrácená varianta, která kombinuje najednou mazání nevhodného textu a
okamžitý vstup do Insert módu.

.. note::

   Existuje ještě Replace mód, do kterého se vstoupuje velkým písmenem "R",
   který začne jakoby přepisovat vše, co mu stojí v cestě.

   Příklad::

      # Mějme klasickou větu:

      Lorem ipsum dolor sit amet, eos eu aperiri moderatius.

      # Pokud bych vstoupil do Replace módu na začátku řádku a začal psát,
      # tak tento nový text překryje ten starý:

      Přepisuji tuto větu.t amet, eos eu aperiri moderatius.

      # Kdybych ještě zůstal v Replace módu, neodcházel do Normalu a začal
      # mazat to, co jsem nově napsal, tak uvidím zpět původní text, který
      # byl překryt:

      Lorem ipsum dolor sit amet, eos eu aperiri moderatius.

Přepisování po znacích
^^^^^^^^^^^^^^^^^^^^^^

* r

  * hned po stisknutí písmenka "r" stisknu nový znak, který nahradí ten
    starý
  * při použití této varianty není žádný vstup do Insert módu, vše probíhá
    v Normal módu

* s

  * smaže daný znak a stále zůstává v Insert módu pro přepisování

Přepisování po slovech
^^^^^^^^^^^^^^^^^^^^^^

* c

  * kombinace písmena "c" s "w" / "e" / "b" a potažmo i čísly (počtem)

Co se týče kombinace "c" s objekty pro slova (aw) / věty (as) / odstavce (ap),
tak zde je naopak nevýhoda, že zmizí i mezery za / před daný objekt, viz
následující příklad::

   # Mějme větu:

   Dnes je pondělí.

   # ve které chci změnit "pondělí" na "úterý". Pokud použiju kombinaci
   # "caw", tak vstup do Insert módu bude vypadat následovně:

   Dnes je|.|

   # tzn. že první musím vložit mezeru a až pak slovo "úterý". Proto, abych
   # si ušetřil čas, tak budu chtít zanechat při přepisování mezeru (v tomto
   # případě před slovem) pomocí "ciw":

   Dnes je |.|

   # Pro větu to bude "cis" a odstavec "cip".

Přepisování po řádcích
^^^^^^^^^^^^^^^^^^^^^^

* cc (nebo i přes "S")

  * smaže celý řádek, kde je kurzor a přepnutí na Insert mód

Pro více řádku pak platí stejné kombinace, jako jsou uvedené v sekcí "Mazání
po řádcích", kde akorát místo písmenka "d" se bude použít "c".

Přepisování ve vymezené části textu
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Opět přes označení textu a pak stisknutím "c". Pokud by se stisklo "r", tak se
na daném řádku bude tolikrát opakovat nový znak, kolik bylo předtím znaků na
něm.

Nahrazování textu
-----------------

Alias přepisování na několika místech najednou.

Nahrazování na řádku
^^^^^^^^^^^^^^^^^^^

* :s/starý_text/nový_text + ENTER

  * pokud se na daném řadku, kde je kurzor, nachází "starý_text" vícekrát,
    tak bude nahrazen novým textem jen jednou

* :s/starý_text/nový_text/g + ENTER

  * nahradí všechen "starý_text" na řádku

Nahrazování na více řádcích
^^^^^^^^^^^^^^^^^^^^^^^^^^^

* :%s/starý_text/nový_text + ENTER

  * nahradí "starý_text" jen jednou na každém řádku v souboru

* :%s/starý_text/nový_text/g + ENTER

  * nahradí "starý_text" všude v celém souboru

Pokud chci nahrazovat jen ve vymezeném území, např. jen od prvního po pátý
řádek včetně, tak použiju::

   :1,5s/starý_text/nový_text + ENTER

   # nebo

   :1,5s/starý_text/nový_text/g + ENTER

Přesouvání textu
----------------

Alias vyjmutí (smazání) části textu a jeho přesunutí na jiné místo.

Při mazání (přes "d", případně i "x") se obsah smazaného textu ještě ukládá do
paměti. Jednak je to kvůli historii (procházení zpět a vpřed) a druhak pro
opětovné vkládání na stejném / jiném místě, což je nyní náš případ.

* p

  * vloží smazaný text za kurzorem (napravo)

* P

  * vloží smazný text před kurzorem (nalevo)

Kopirování textu
----------------

* y

  * hlavní písmenko pro kopírování, které lze použít samostatně jen ve
    Visual módu

* yy

  * zkopíruje celý řádek, na kterém se nacházím

Pří použití "y" s jakýmkoliv dalším pohybovým znakem lze kopírovat ještě v
Normal módu (netřeba přepínat na Visual). Pro vkládání tohoto zkopírovaného
textu se používají opět písmenka "p" / "P".

Pokročilé ovládání
==================

Práce s více soubory
--------------------

Bez záložek
^^^^^^^^^^^

Soubor, se kterým chci aktuálně pracovat, tak ho uvidím na popředí a ostatní
budou čekat na pozadí, dokud se na ně nepřepnu. Nevýhodou je, že nemám
přehled, jaké soubory jsou otevřené v pozadí, pokud nepoužiju příkaz / plugin.

Otevírání souborů nad sebe a jejich zavírání
""""""""""""""""""""""""""""""""""""""""""""

* :e cesta_k_souboru

  * otevře daný soubor a ostatní otevřené soubory schová

* :bd (:bd!)

  * zavře daný soubor
  * pokud je to jediný soubor, který mám otevřevený, tak na rozdíl od ":q"
    se Vim nezavře, jen zůstané prázdný

Zobrazení přehledu otevřených souborů
"""""""""""""""""""""""""""""""""""""

* :ls

  * zobrazení všech souborů, které jsou otevřeny a pod jakým pořadovým
    číslem (bude se hodit pro přepínání)
  * číslování je od jedničky

Přepínání mezi soubory
""""""""""""""""""""""

* :bn

  * přepne se další soubor v pořadí

* :bp

  * přepne se na předchozí soubor v pořadí

* :b2

  * přepne se na soubor s pořadovým číslem 2

V oknech
^^^^^^^^

Alias zobrazení několika souborů (stejných či různých) do oken tak, abych je
všechny viděl najednou a v případě potřeby mohl mezi nimi přepínat. Okna mohou
být jak vedle sebe (vertikálně), tak i nad / pod sebou (horizontálně).

.. note::

   V každé záložce mohou být jinak rozvrstveny okna.

Vytvoření a zavření oken
""""""""""""""""""""""""

a) stejný soubor ve více oknech

   * CTRL + ws (:sp)

     * vytvořii kopii aktuálního souboru včetně změn a otevře jej v dalším
       okně horizontálním způsobem (pod aktuálním oknem)

   * CTRL + wv (:vsp)

     * to samé, ale nové okno vznikne vpravo vedle aktuálního okna
       (vertikální způsob)

b) různé soubory v oknech

   * :sp cesta_k_souboru

     * načte obsah daného souboru a zobrazí ho v okně pod aktuálním oknem

   * :vsp cesta_k_souboru

     * to samé, ale zobrazí ho ve vedlejším okne napravo

Okno, ve kterém je kurzor se zavírá pomocí::

   CTRL + wq

   # nebo taktéž klasicky

   :q
   :q!
   :qa
   :qa!
   :wq

Zavření všechn ostatních oken kromě aktuálního okna::

   :on

Přepínání mezi okny
"""""""""""""""""""

* CTRL + w + pohybový_směrový_znak

  * tím pohybovým směrovým znakem mám na mysli klasické "h" / "j" / "k" a
    "l", pomocí kterých se lze přepínat mezi okny

Přesouvání oken
"""""""""""""""

* CTRL + w + r

  * přesune okno dolů / doprava, avšak zaleží na typech oknech (nelze
    kombinovat horizontální okno s vertikálním)

* CTRL + w + R

  * přesune okno nahoru / doleva (platá stejná podmína, jako před chvíli)

* CTRL + w + H / J / K / L

  * přesune dané okno na úplně vlevo / dolu / nahoru / doprava, přičemž se
    může změnit i typ okna, např. z vertikálního na horizontálního

Úprava velikosti oken
"""""""""""""""""""""

a) na výšku

   * CTRL + w + +

     * zvětší okno na výšku o jeden řádek

   * 5 + CTRL + w + +

     * zvětší okno o 5 řádků

   * CTRL + w + -

     * zmenší okno o jeden řádek

   * 5 + CTRL + w + -

     * zmenší okno o 5 řádků

   * :res 20

     * nastaví fixní výšku na 20 řádků

b) na šířku

   * CTRL + w + >

     * zvětší okno na šířku o jeden sloupec

   * 5 + CTRL + w + >

     * zvětší okno o 5 sloupců

   * CTRL + w + <

     * zmenší okno o jeden sloupec

   * 5 + CTRL + w + -

     * zmenší okno o 5 sloupců

   * :vert res 80

     * nastaví fixní šířku na 80 znaků

.. tip::

   Pokud bych chtěl mít 2 okna vedle / pod sebe stejně velká, stisknu::

      CTRL + w + =

Se záložkami
^^^^^^^^^^^^

Na rozdíl od varianty bez záložek jednak uvidím ve výchozím stavu nahoře ve
Vimu přehledně záložky se jmény souborů, které v nich mám otevřeny a druhak
mohu mít v nich jinak rozvrstevny okna, což by ve variantě bez záložek nešlo.

Otevírání a zavírání záložek
""""""""""""""""""""""""""""

Novou záložku mohu otevřít jak prázdnou, tak i načtenou s obsahem nějakého
souboru:

a) prázná záložka

   * :tabnew

     * otevře prázdnou záložku (nahoře v terminálu bych měl vidět
       rozdělení na záložky)
     * aktuální záložku poznám jednak podle tučného písmena a druhak podle
       barvy pozadí (je stejné, jako u řádků pod záložkami)
     * pokud bych načíst do této prázdné záložky obsah nějakého souboru,
       tak použiju syntaxi::

          :o cesta_k_souboru

b) záložka se souborem

   * :tabnew cesta_k_souboru

     * načte do záložky rovnou obsah daného souboru

Zavřít záložku/y mohu několika způsoby:

1. :tabc

   * zavře záložku, na které se nacházím, nicméne soubor bude stále otevřený
     v paměti
   * jestliže jsou v daném souboru na dané záložce nějaké změny, které nejsou
     uložené, tak Vim odmítne exekuci tohoto příkazu
   * pro zavření záložky bez uložení je třeba používat ještě vykričník::

        :tabc!

   * pro zavření záložky s uložením změn se použije standardně::

        :wq

   * pro za

2. :tabo (:tabo!)

   * zavře všechny ostatní záložky, ale aktuální ne
   * taktéž Vim zařve, pokud nějaká změna v nějaké záložce není uložena

3. :qa (:qa!)

   * zavření všech záložek a ukončení Vimu

Přecházení mezi záložkami
"""""""""""""""""""""""""

* qt (:tabn)

  * přepne se na další záložku (vpravo)

* qT (:tabp)

  * přepne se na předchozí záložku (vlevo)

* 3gt

  * přene se na třetí záložku v pořadí (počítá se od jedničky)

.. tip::

   Pokud bych chtěl najednou ve všech záložkách spustit stejný příkaz,
   použiju následující syntaxi::

      :tabd příkaz

   U příkazu není třeba na začátku používat dvojtečku.

Přesouvání záložek
""""""""""""""""""

Jestli se mi nelíbí pořádí záložek, tak si ho můžu upravit pomocí syntaxe::

   :tabm nová_pozice_záložky

.. note::

   Zde se naopak čísluje od nuly. Tudíž, pokud chci přesunout aktuální
   záložku na úplný začátek, použiju právě nulu::

      :tabm 0

Exekuce externích příkazů
-------------------------

S dočasným opuštěním Vimu
^^^^^^^^^^^^^^^^^^^^^^^^^

Externí terminálové příkazy se z Vimu spouštějí pomocí vykřičníku za klasickou
dvoutečkou a názvem daného příkazu::

   :!ls -l

Vim bude dočasně schovaný, neboť se zobrazí klasický terminál s výsledkem
příkazu. Pro návrat do editoru se pak stiskne ENTER.

Další možností je:

1. přesunout editor na pozadí klávesovou zkratkou::

      CTRL + z

2. spustit příkaz a do editoru se vrátit příkazem::

      fg

Bez opuštění Vimu
^^^^^^^^^^^^^^^^^

* :w !příkaz

  * výstup příkazu se zobrazí v přikazovém řádku dole

* :r !příkaz

  * výstup se zapíše na aktuální místo kurzoru v souboru
  * pro jiné místo v souboru je nutné uvést i číslo řádku (počítá se od
    nuly, takže vždy 1 dílek ubrat), např. pro 5 řádek v souboru to bude::

       :4r !ls

.. tip::

   Pro vložení obsahu je jiného souboru lze zkratka:

      :r cesta/k/souboru

Pracovní prostředí
------------------

Rozvržení oken a záložek si mohu uložit a zpětně zobrazit při dalším spuštění
Vimu. Stačí aktuální nastavení uložit pomocí příkazu::

   :mks cesta/pro/uložení/souboru.vim

   # Doporučuji vytvořit adresář "~/.vim/sessions/" a ukládat tam

   :mks ~/.vim/sessions/název_uloženého_pracovního_prostředí.vim

Poté stačí při dalším otevření editoru použít příkaz::

   $ vim ~/.vim/sessions/název_pracovního_prostředí.vim

   # nebo taktéž uvnitř Vimu pomocí:

   :source ~/.vim/sessions/název_pracovního_prostředí.vim

.. note::

   Pokud budete používat plugin NERDTree, tak při otevření pracovního
   prostředí nebude strom vidět (BUG). Stačí si otevřít další a hned ho opět
   zavřít (budou vidět dva najednou).

Obnovení souborů
----------------

Vim defaultně nedělá zálohy souborů (soubory s koncovkou "~"). Nicméně i
přesto si uchavává dost informací o poslední editaci souboru pro případ
obnovení (např. se vypnul z ničeho nic počítač).

Při editaci souborů se v daném adresáři objeví skrytý soubor se stejným
názvem editovaného souboru a koncovkou ".swp". Soubor ze zálohy se spustí
pomocí příkazu::

   $ vim -r název_souboru

Objeví se hláška o obnově a doporučení uložit obnovený soubor pod jiným
názvem. Hláška se vypne stisknutím ENTER klávesy. Po editaci v obnoveném
souboru je pak potřeba smazat již starý ".swp" soubor.

Seznam souboru k obnově lze zobrazit příkazem::

   $ vim -r

Přízpůsobení Vimu
=================

Aneb nastavení vlastního vzhledu, zvýrazňování syntaxe, zobrazení řádku s
čísly atd.

Konfigurační soubor
-------------------

Slouží pro ukládání nastavení pro každé budoucí spuštení Vimu. Je třeba jej
vytvořit v domovském adresáři se jménem::

   .vimrc

Rovnou si můžeme napsat i nějaké to základní nastavení::

   set number          " zobraz čísla řádků
   set colorcolumn=80  " ukáž vodorovnou čáru na 80. znaku (lze překročit)

   " Globální nastavení tabulátorů

   set tabstop=4       " velikost tabulátoru podle znaků
   set softtabstop=4  " v souboru nechá původní velikost tabu, ale já
                       " uvidím ve Vimu jen 4 mezery
   set shiftwidth=4    " velikost odsazení (např. ve Visual módu přes ">")
   set expandtab       " zkonvertuje tabulátory na mezery
   set smarttab        " pokud mám nastavený expandtab, tak při mazání se
                       " smažou 4 mezery najednou a ne jen po jedné

   " Nastavení pro jednotlivé soubory

   autocmd Filetype html setlocal ts=2 sw=2 sts=2
   autocmd Filetype css setlocal ts=2 sw=2 sts=2
   autocmd Filetype js setlocal ts=2 sw=2 sts=2

.. note::

   Dvojitá otevírací uvozovka slouží pro komentáře (nutno bez zavírací).

Pluginy
-------

Aneb zásuvné moduly, které rozšířují funkčnost Vimu. Mohu si je vytvořit sám
nebo použít už nějaký hotový od někoho.

Plug
^^^^

https://github.com/junegunn/vim-plug

Vim Plug je z mnoha nástrojů pro správu modulů. Umí klasicky stáhnout
externí moduly, nainstalovat je a aktivovat je pro každou instanci Vimu.

Lze ho stáhnout příkazem::

   curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

Dále není třeba nic instalovat. Stačí jen ve Vimu vyjmenovat moduly (externí),
které chci použivat::

   call plug#begin('~/.vim/plugged')

   Plug 'název_uživatele/název_repozitáře_na_githubu'
   Plug 'https://adresa.doména/cesta/k/git/repozitáři.git'

   call plug#end()

Nyní je třeba znovu načíst konfigurační soubor (lze rovnou z Vimu)::

   :source ~/.vimrc

Pak stačí spustit příkaz pro instalaci vyjmenovaných modulů::

   :PlugInstall

Kdybych přestal nějaký plugin používat, tak jej odstraním z konfiguráku a
odintaluji pomocí::

   :PlugClean

   # nebo bez potvrzení

   :PlugClean!

TODO
====

* X (x před kurzorem)
* xp (přehoď dva znaky)
* . (zopakuj)
* text buffery
* :args (zobraz soubory, když jich bylo otevřeno více najednou)
* :n (editace dalšího souboru)
* :N (editace předchozího souboru)
* :buffer
* |
* {
* }
* %
* (
* )
* \*
* #
* .
* 10itext
* 3.
* (CTRL + v) + I + "# " (rychlé zakomentování)
* qa, @a, @@ (makra)
* v + "w" (automatické odsazení)
* r / R
* s / S
* ma ('a)
* CTRL + i / CTRL + i
* visual + u (malé)
* visual + U (velké)
* mksession

::

   " To save, ctrl-s.
   nmap <c-s> :w<CR>

::

   set incsearch
   imap <c-s> <Esc>:w<CR>a

::

   :set paste
   :set nopaste

::

   :set textwidth=80

* šablony (skeletony souborů) a snippety
* tagy
* vimgrep hledání napříč soubory
