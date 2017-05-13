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
     jiného módu se zpátky na Normal mód přepne pomocí klávesy ``ESC``

2. Insert

   * mód pro vkládání textu do souboru
   * zapne se zpravidla stisknutím písmenka ``i``, po kterém lze začít
     psát či editovat text

3. Command-line

   * mód pro ovládání editoru jako takového pomocí příkazů
   * editor se ovládá z příkazového řádku, který se objeví po stisknutí
     dvojtečky ``:`` (viz zavření Vimu pomocí ``:q``)

.. note::

   Pomocí šipky nahoru lze v Command-line módu zobrazit předchozí příkaz.

Otevření souboru
----------------

Příkazem ``vim`` lze i otevřít nějaký existující nebo neexistující soubor::

   $ vim test.txt

Soubor jde také otevřit až uvnitř Vimu pomocí příkazu ``:e`` a uvedení cesty k
souboru::

   $ :e ~/Documents/test.txt

Pro začátek psaní do souboru je třeba přejít do Insert módu pomocí písmenka
``i`` a začít psát či editovat text. Po skončení editace je vhodné se vrátit
zpět do Normal módu pomocí ``ESC``.

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

Pro uložení změn je třeba použít příkaz ``:w`` v Normal módu::

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

   Tento text se vloží do Vimu uvnitř Insert módu za použití klávesové
   zkratky ``CTRL + SHIFT + v``.

Základní pohyb po znacích a řádcích
-----------------------------------

Šipkami vlevo a vpravo, respektive písmenky ``h`` a ``l`` se posune kurzor
o jeden znak do strany. Šipkami nahoru a dolu, respektive písmenky ``k`` a
``h`` se posunu kurzor o řádek v daném směru, viz schéma::

         k
         ^
         |
   h <--- ---> l
         |
         v
         j

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
       ---->----->

* ``b`` (``B``)

  * skoč na začátek aktuálního nebo předchozího slova::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
       <-----<----

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
       ------>------------>
       <-----<-------------

* ``?pattern`` + ``ENTER``

  * najdi v textu nalevo od kurzoru až po začátek souboru výskyt daného
    patternu
  * taktéž lze použít ``n`` a ``N``, avšak zde bude účinek opačný

Oba dva způsoby jsou defaultně citlivé na rozdíl velkých a malých písmen. Pro
vypnutí této citlivosti je třeba na konec patternu napsat suffix ``\c``::

   /pattern\c
   ?pattern\c

.. note::

   Tyto způsoby se spíše používájí pro vyhledávání v textu, než na skákání jako
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

Skok na vertikální hranu okna
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``H``

  * skoč na první řádek v okne (horní hrana)

* ``M``

  * skoč doprostřed okna

* ``L``

  * skoč na poslední řádek v okně (spodní hrana)

.. tip::

   Pokud chci aktuální řádek posunout na hranu okna, tak mohu použít tyto
   klávesy:

   * ``zt``

     * posuň aktuální řádek na horní hranu okna

   * ``zz``

     * posuň aktuální řádek doprostřed okna

   * ``zb``

     * posuň aktuální řádek na spodní hranu okna

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

Skok na konkrétní znak na řádku
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``f`` + znak

  * skoč dopředu na první výskyt daného znaku::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
       -------->
          fu

  * na druhý a další vyskýt se skočí pomocí ``;``, zpátky přes ``,``

* ``F`` + znak

  * skoč dozadu na první výskyt daného znaku
  * taktéž lze použít ``;`` a ``,``, akorát chování je obráceně

Skok na další výskyt slova v souboru
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``*``

  * skoč na další výskyt slova v souboru, pokud se kurzor právě nachází
    v daném slově

* ``#``

  * skoč na předchozí výskyt slova v souboru, pokud se kurzor právě nachází
    v daném slově

Skok na kraj závorky
^^^^^^^^^^^^^^^^^^^^

- ``%``

  * skoč na kraj závorky (platí pro všechny tvary závorek)::

       2 * (a + b)
           <----->
              %

.. note::

   Pokud se kurzor nachází někde uvnitř závorek, tak první skok pomocí ``%``
   bude na otevírající závorku.

Skok na další větu
^^^^^^^^^^^^^^^^^^

* ``)``

  * skoč na začátek další věty::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur...
             ------------------------------------------------->

* ``(``

  * skoč na začátek předchozí věty::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur...
       <-----------------------------------------------------------

Skok na další odstavec
^^^^^^^^^^^^^^^^^^^^^^

* ``}``

  * skoč na další odstavec (za blok textu)::

       | * one
       | * two
       | * three
       v
         Lorem ipsum dolor sit amet, eos eu aperirir moderatius.

* ``{``

  * skoč na předchozí odstavec (před blok textu)

Skok na předchozí místo před skokem
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``\```` (bez zpětného lomítka)

  * skoč na pozici před skokem

.. tip::

   Dále do minulých pozic se skočí pomocí ``CTRL + o`` a zpět do budoucnosti
   přes ``CTRL + i``.

Odbočka k dalším vstupům do Insert módu
---------------------------------------

* ``a``

  * Insert mód začne za kurzorem (opak ``i``)

* ``A``

  * Insert mód začne na konci řádku za posledním znakem

* ``I``

  * Insert mód začne od začátku řádku, případne od začátku odsazeného
    textu

Je-li třeba zároveň i odřádkovat:

* ``o``

  * Insert mód začne na dalším novém řádku::

       | Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur
       v
         nostrud quaeque eu, an his hendrerit prodesset, nonumes oportere
         gloriatur qui ut.

* ``O``

  * Insert mód začne na předchozím novém řádku::

       ^
       | Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur
         nostrud quaeque eu, an his hendrerit prodesset, nonumes oportere
         gloriatur qui ut.

.. tip::

   Je-li třeba vložit opakovaně stejný text, lze místo kopírování a vkládání
   použít zkratku přes opakovaný vstup do Insert módu. Např. pro vložení
   ``xxxxxxxxxx`` do textu stačí napsat ``9ix`` a ``ESC``::

      9ix + ESC
      xxxxxxxxx

   Stejného postupu lze docílit pomocí jednoho vložení písmenka ``x`` a pak
   v Normal módu napst ``8.``, kdy se ještě 8x vloží písmenko ``x``. Tečka
   ``.`` zopakuje předchozí akci.

Editace textu
=============

Mazání textu
------------

Mazání po znaku
^^^^^^^^^^^^^^^

* ``x``

  * smaž znak pod kurzorem

* ``X``

  * smaž znak před kurzorem

.. note::

   Je-li třeba tuto akci zopakovat, stačí před stisknutím ``x`` / ``X``
   stisknout číslo, kolik se má smazání znaku provést, např. ``3x``.

Odbočka k zahození a obnovení změn v souboru
""""""""""""""""""""""""""""""""""""""""""""

* ``u``

  * zahoď poslední změnu v souboru, např. smázání znaku

* ``CTRL + r``

  * vrať poslední změnu v souboru (po stisknutí ``u``)

.. note::

   ``u`` a ``CTRL + r`` lze několikrát opakovat.

Mazání po slovu
^^^^^^^^^^^^^^^

* ``dw``

  * smaž znaky až do začátku dalšího slova

* ``de``

  * smaž znaky až do konce slova

* ``db``

  * smaž znaky až do začátku slova

* ``daw``

  * smaž celé slovo, pokud se v něm nachází kurzor

.. tip::

   Pro smazání věty se použije ``das`` a pro smazání odstavce ``dap``.

Mazání na kraj řádku
^^^^^^^^^^^^^^^^^^^^

* ``d0``

  * smaž text až na začátek řádku

* ``d$``

  * smaž text až po konec řádku

* ``d^``

  * smaž text až do začátku odsazení řádku

Mazání po řádku
^^^^^^^^^^^^^^^

* ``dd``

  * smaž aktuální řádek

* ``dj``

  * smaž aktuální řádek a řádek pod ním

* ``dk``

  * smaž aktuální řádek a řádek nad ním

* ``dG``

  * smaž aktuální řádek až po poslední řádek včetně

* ``dgg``

  * smaž aktuální řádek až po první řádek včetně

* ``d`` + číslo + ``G``

  * smaž aktuální řádek až po daný řádek včetně

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

Stiskem ``x`` nebo ``d`` při označeném textu ve Visual módu, viz níže.

Odbočka k Visual módu
"""""""""""""""""""""

Mód pro označení nějaké části textu. Text se označuje následujícími způsoby:

* ``v``

  * označování textu po znacích, slovech aj. v kombinaci s navigačními znaky
  * písmenkem ``o`` mohu skočit na opačnou stranu označeného textu a případně
    rozšířit nebo zmenšit označený text

* ``V``

  * označování textu po řádcích

* ``CTRL + v``

  * označování textu po sloupcích
  * písmenkem ``O`` mohu skočit na opačný kraj sloupově označeného textu

.. note::

   Zpátky na Normal mód se přepne klasicky pomocí ``ESC``.

V rámci označeného textu jdou použít i tyto speciální znaky:

* ``>``

  * posuň (odsaď) text doprava o jeden tabulátor

* ``<``

  * posuň text doleva o jeden tabulátor

* ``u``

  * zmenši text na malé písmena

* ``U``

  * zvětši text na velké písmena

* ``~``

  * prohoď velikost malých a velkých písmen

.. tip::

   Pomocí ``gv`` lze opětovně označit předchozí označený text.

Přepisování textu
-----------------

Přepisování po znaku
^^^^^^^^^^^^^^^^^^^^

* ``r`` + znak

  * přepiš znak v místě kurzoru na jiný

Přepisování po slovu
^^^^^^^^^^^^^^^^^^^^

* ``cw``

  * přepiš znaky až do začátku dalšího slova na jiný text napsaný v Insert
    módu (platí pro každý přepis níže)

* ``ce``

  * přepiš znaky až do konce slova

* ``cb``

  * přepiš znaky až do začátku slova

* ``ciw``

  * přepiš celé slovo, pokud se v něm nachází kurzor

.. tip::

   Pro přepsání věty se použije ``cis`` a pro přepsání odstavce ``cip``.

Přepisování na kraj řádku
^^^^^^^^^^^^^^^^^^^^^^^^^

* ``c0``

  * přepiš text až na začátek řádku

* ``d$``

  * přepiš text až po konec řádku

* ``d^``

  * přepiš text až do začátku odsazení řádku

Přepisování po řádku
^^^^^^^^^^^^^^^^^^^^

* ``cc``

  * přepiš aktuální řádek

* ``cj``

  * přepiš aktuální řádek a řádek pod ním

* ``ck``

  * přepiš aktuální řádek a řádek nad ním

* ``cG``

  * přepiš aktuální řádek až po poslední řádek včetně

* ``cgg``

  * přepiš aktuální řádek až po první řádek včetně

* ``c`` + číslo + ``G``

  * přepiš aktuální řádek až po daný řádek včetně

Přepisování ve vymezené části textu
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Stiskem ``c`` při označeném textu ve Visual módu.

.. note::

   Při stisku ``r`` ve Visual módu a následného stisknutí libovolného znaku
   se celý text přepíše na tento libovolný znak.

Nahrazení textu
---------------

Nahrazení na řádku
^^^^^^^^^^^^^^^^^^

* ``:s/`` + starý text + ``/`` + nový text + ``ENTER``

  * nahraď jednou starý text za nový text na daném řádku::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.
       :s/Lorem/Merol
       Merol ipsum dolor sit amet, eos eu aperiri moderatius.

* ``:s/`` + starý text + ``/`` + nový text + ``/g`` + ``ENTER``

  * nahraď všechen starý text za nový text na daném řádku

Nahrazení v konkrétních řádcích
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``:`` + začátek + ``,`` + konec + ``s/starý_text/nový_text`` + ``ENTER``

  * nahraď jednou starý text za nový text v daných řádcích::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur
       nostrud quaeque eu, an his hendrerit prodesset, nonumes oportere
       gloriatur qui ut.
       :1,3s/eu/ue

* ``:začátek,konecs/starý_text/nový_text`` + ``/g`` + ``ENTER``

  * nahraď všechen starý text za nový text v daných řádcích

Nahrazení v celé souboru
^^^^^^^^^^^^^^^^^^^^^^^^

* ``:%s/starý_text/nový_text`` + ``ENTER``

  * nahraď jednou starý text za nový text v celém souboru

* ``:%s/starý_text/nový_text/g`` + ``ENTER``

  * nahraď všechen starý text za nový text v celém souboru

Přesouvání textu
----------------

.. note::

   Nejprve je nutné smazat nějaký text, aby bylo možné tento smazaný text
   přesunout na jiné místo v souboru.

* ``p``

  * vlož smazaný text za kurzorem

* ``P``

  * vlož smazaný text před kurzorem

.. note::

   ``p`` lze použít i v rámci Visual módu, např. když je třeba vložit
   smazaný řádek na místo s prázdným řádkem

Kopírování a vkládání textu
---------------------------

* ``y``

  * zkopíruj označený text ve Visual módu

* ``yy``

  * zkopíruj akutální řádek bez nutnosti použít Visual mód

Tento zkopírovaný text se vloží na jiném místě v souboru pomocí ``p`` nebo
``P``, viz přesouvání textu.

Pokročilé ovládání
==================

Práce s více soubory
--------------------

Bez záložek
^^^^^^^^^^^

Soubory jsou načteny do paměti a seřazeny v tzv. zásobníku (buffer), kdy na
popředí jde vidět obsah jen jednoho souboru a další čekají na editaci v pozadí.

Otevírání a zavírání souborů
""""""""""""""""""""""""""""

* ``:e`` + cesta k souboru

  * otevři v popředí daný soubor a aktuální schovej na pozadí::

       :e ~/.vimrc

  * alternativě lze otevřít více souborů najednou i z příkazového řádku::

       $ vim a.txt b.txt c.txt

* ``:bd``

  * zavři daný soubor, respektive zavři násilně bez uložení změn pomocí
    ``:bd!``

.. note::

   Pokud se zavře poslední soubor z bufferu, tak na rozdíl od ``:q`` se Vim
   nezavře, ale zůstane stále otevřený s prázdnou obrazovkou.

Zobrazení přehledu souborů v bufferu
""""""""""""""""""""""""""""""""""""

* ``:ls``

  * zobraz pořadí otevřených souborů a polohu kurzoru v každém souboru

Přepínání mezi soubory
""""""""""""""""""""""

* ``:bn``

  * přepni se na další soubor v pořadí

* ``:bp``

  * přepni se na předchozí soubor v pořadí

* ``:b2``

  * přepni se na soubor s pořadovým číslem 2

V oknech
^^^^^^^^

Vytvoření a zavření oken
""""""""""""""""""""""""

* ``:sp``

  * otevři kopii aktuálně otevřeného souboru nad aktuálním oknem

* ``:sp`` + cesta k souboru

  * otevři nad aktuálním oknem daný soubor::

       :sp ~/.vimrc

* ``:vs``

  * otevři kopii aktuálně otevřeného souboru vlevo od aktuálního okna

* ``:vs`` + cesta k souboru

  * otevři vlevo od aktuálního okna daný soubor

* ``:q`` (``:q!``)

  * zavři okno, ve kterém se nachází kurzor

* ``:qa`` (``:qa!``)

  * zavři všechna okna najednou

* ``:on`` (``:on!``)

  * zavři všechna okna kromě okna, ve kterém se nachází kurzor

.. tip::

   Pomocí ``:wa`` lze uložit změny ve všech oknech a přes ``:wqa`` zavřít
   všechny okna i celý Vim

Přepínání mezi okny
"""""""""""""""""""

* ``CTRL + w`` + směrový pohyb (``h``, ``j``, ``k`` a ``l``)

  * přepni se na dané okno

Přesouvání oken
"""""""""""""""

* ``CTRL + w + x``

  * prohoď dva stejné typy oken vedle sebe nebo nad sebou

* ``CTRL + w + r``

  * posuň okno dolu u horizontálních oken nebo doprava u vertikálních oken

* ``CTRL + w + R``

  * posuň okno nahoru u horizontálních oken nebo doleva u vertikálních oken

* ``CTRL + w`` + ``H`` nebo ``J`` nebo ``K`` nebo ``L``

  * přesuň okno úplně vlevo / dolu / nahoru / doprava (může se změnit typ okna
    z vertikálního na horizontální a naopak)

Úprava velikosti oken
"""""""""""""""""""""

Na výšku:

* ``CTRL + w + +``

  * zvětši okno o jeden řádek nebo více řádků, je-li stisknuto před klávesovou
    zkratkou i číslo

* ``CTRL + w + -``

  * zmenši okno o jeden řádek nebo více řádků, je-li stisknuto před klávesovou
    zkratkou i číslo

* ``:res`` + číslo

  * nastav fixní výšku okna na daný počet řádků::

       :res 30

Na šírku:

* ``CTRL + w + >``

  * zvětší okno o jeden sloupec nebo více sloupců, je-li stisknuto před
    klávesovou kratkou i číslo

* ``CTRL + w + <``

  * zmenši okno o jeden sloupec nebo více slopců, je-li stisknuto před
    klávesovou zkratkou i číslo

* ``:vert res`` + číslo

  * nastaví fixní šířku okna na daný počet sloupců::

       :vert res 80

.. tip::

   Pokud bych chtěl mít dvě rozdělená okna stejně velká::

      CTRL + w + =

Se záložkami
^^^^^^^^^^^^

Záložky jsou na rozdíl od bufferu přehledně zobrazeny v horní části Vimu. Navíc
každá záložka může mít jinak uspořádána okna.

Otevírání a zavírání záložek
""""""""""""""""""""""""""""

* ``:tabnew``

  * otevři novou prázdnou záložku a přepni se na ni

* ``:tabnew`` + cesta k souboru

  * otevři v nové záložce obsah daného souboru a přepni se na ni

* ``:tabc`` (``:tabc!``)

  * zavři aktuální záložku (obsah souboru může ještě zůstat v bufferu)

* ``:tabo`` (``:tabo!``)

  * zavři všechny záložky krom aktuálně otvřené záložky

Přecházení mezi záložkami
"""""""""""""""""""""""""

* ``qt``

  * přepni se na další záložku

* ``qT``

  * přepni se na předchozí záložku

* číslo + ``gt``

  * přeni se na danou záložku (čísluje se od jedničky)

* ``:tabfir``

  * přepni se na první záložku v pořádí

* ``:tabl``

  * přepni se na poslední záložku v pořádí

Přesouvání záložek
""""""""""""""""""

* ``tabm`` + číslo

  * přesuň aktuální záložku na jiné pořadí (jde použít nulu)

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

* text buffery
* :n (editace dalšího souboru)
* :N (editace předchozího souboru)
* :buffer
* qa, @a, @@ (makra)
* ma ('a) (registry i pro kopírování, mazání, vkládání)
* mksession
* CTRL + W + o (zavři ostatní okna krom aktuálního)
* !10Gsort
* !!date
* gJ (spoj řádky bez mezery)
* (CTRL + v) + !sort

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

::

   :set nowrap

::

   :so ~/.vimrc

::

   :set incsearch

* šablony (skeletony souborů) a snippety
* tagy
* vimgrep hledání napříč soubory
* adresář pro swapy
* kopírování z Vimu ven
* ukládání session

  ::

     :set directory=/tmp
     :set directory=.,/tmp

* no hls after ESC
