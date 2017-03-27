==================
 reStructuredText
==================
----------------------------------------------------------
 Pokročilý textový formát pro psaní technické dokumentace
----------------------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:Licence: CC BY-SA 4.0

:Abstract:

   `reStructuredText`_ (zkráceně RST, ReST či reST) vznikl v roce 2002 jako
   součást projektu `Docutils`_, který zpracováva text a dál jej zkonvertuje
   do dalších textových formátu jako je HTML, PDF aj. Je vyvíjen Davidem
   Goodgerem.

   RST se uchytil nejvíce v dokumentaci projektů v Pythonu. Je v něm dokoncena
   popsána celá standardní knihovna toho jazyka.

   Používá se zejména v kombinaci s generátorem dokumentace `Sphinx`_, který
   byl vyvinut pro interní potřebu Pythonu. Pomocí něj lze extrahovat
   komentáře a dokumentační řetězce ze zdrojového kódu a převést je na RST.

   RST lze vyzkoušet online v editoru http://rst.ninjs.org/.

.. contents:: Obsah

Základní formátování textu
==========================

Text s reStructuredText značkami se píše do souboru s koncovkou ".rst".

Nadpisy
-------

Značení pro nadpisy není v RST přesně definované. Pro označení lze použít
jakékoliv nealfanumerické znaky, jako např. = - ` : ' " ~ ^ _ * + # < >, které
musí být tolikrát zopakovány nad / pod nadpisem, kolik je znaků v něm.

Python používá následující strukturu::

   ##########################################################
     Název části dokumentace (v ``index.rst`` souboru) (h1)
   ##########################################################

   ********************************************
   Název kapitoly (zvlášť v jiném souboru) (h1)
   ********************************************

   Název sekce (h2)
   ================

   Název podsekce (h3)
   -------------------

   Název podpodsekce (h4)
   ^^^^^^^^^^^^^^^^^^^^^^

   Menší nadpisek o velikosti textu v odstavích (h5)
   """""""""""""""""""""""""""""""""""""""""""""""""

Co se týče titulku a podtitulku nějakého obyčejného dokumentu, tak lze použít
i následující syntaxi::

   ===================
    Titulek dokumentu
   ===================
   -----------
    Podtitulek
   ------------

   Název sekce
   ===========

   ...

Odstavce
--------

Klasický souvislý text oddělený od dalšího odstavce prázdným řádkem::

   Toto je první odstavec.

   Toto je druhý odstavec za prázdným řádkem.

Pokud potřebuji nějaký text zalomit, tak na začátku řádku musí být svislá
čára::

   | Toto je
   | zalomený text.

Kdyby se nepoužila svislá čára, tak text po konverzi na HTML by vypadal
následovně::

   Toto je zaloměný text.

Zvýraznění textu
----------------

1. kurzíva

   - na kraj slova / textu se vloží jedna hvězdička "*"::

        *kurzíva* nebo *text kurzívou*

2. tučné písmo

   * na krajích jsou dvakrát hvězdičky::

        **tučné** nebo **text tučným písmem**

Kurzívu a tučné písmo nejde spolu kombinovat, pokud si nevytvořím vlastní
pravidlo a styl v CSS, které půjde vidět v HTML.

.. tip::

   Pokud text vyžaduje hvězdičky, ale já nechci formátovat text na kurzívu či
   tučné písmo, tak musím před hvězdičky vloziž zpětná lomítka pro deaktivaci::

      \*Toto není text kurzívou.\*

Seznamy
-------

1. neseřazené

   * jako odrážky se považují znaky "-", "+" a "-", kde nejpoužívanějším znakem
     je hvězdička

2. číselné

   * jako číselné seznamy se považuji tyto sekvence:

     * arabská čísla: 1, 2, 3
     * malá písmena: a, b, c
     * malé římské číslice: i, ii, iii
     * velká písmena: A, B, C
     * velké římské číslice: I, II, III

   * tyto sekvence lze formátovat pomocí:

     * tečky na konci: 1., 2., 3.
     * závorkámi na obou stranách: (1), (2), (3)
     * zavirájící závorkou na konci: 1), 2), 3)

   * nejčastějí použivánou variantou jsou arabská čísla s tečkou na konci::

        1. jedna
        2. dva
        3. tři

Obě dvě varianty lze jakkoliv kombinovat. Důležitě je vědět, že vnořené seznamy
se oddělují prázdnými řádky a delší text v nich se odsazuje na místě, kde
začíná předchozí řádek s textem, viz::

   * ovoce

     1. ananas je
        tropický ovoce

   * zelenina

     - okurka

       Okurka se pěstuje na poli či zahradě.

     - paprika

.. tip::

   Pokud jsem moc líný, tak mohu nechat RST automaticky počítat čísla položek
   v seznamu. Stačí místo nich používat mřížku "#"::

      #. automatická jednička
      #. automatický dvojka

Definice
--------

Speciální seznam pro vysvětlení jednotlivých definic::

   HTTP
      Internetový protokol pro výměnu HTML souborů.

   Python
      Skriptovací programovací jazyk.

Odkazy
------

1. odkaz v textu

   a) bez popisku::

         http://www.python.org

   b) s popiskem::

         `Python <http://www.python.org>`_

2. odkaz odkazují na odkaz na konci souboru

   a) jednoslovný popisek::

         Python_ je programovací jazyk.

         .
         .
         .

         .. _Python: http://www.python.org

   b) víceslovný popisek::

         Python je můj neojblíbenější `programovací jazyk`_.

         .
         .
         .

         .. _programovací jazyk: http://www.python.org

   c) odkaz odkazují na již existující odkaz::

         Python_ je `programovací jazyk`_.

         .
         .
         .

         .. _Python: http://www.python.org
         .. _programovací jazyk: Python_

.. tip::

   Odkazy mohou vést i uvnitř dokumentu na další nadpisy (sekce). Stačí uvést
   jeho název, tak jak je v dokumentu::

      Tento následující odkaz odkazuje do sekce `Odkazy`_.

Poznámky pod čarou
------------------

Alias indexy v textech s odkazy na konec souboru, kde jsou dodatečné
vysvětlivky a odkazy (citace) na jiné stránky::

   Python [1]_ je programovací jazyk.

   .. [1] Python (programming language).
      Wikipedia: the free encyclopedia. [online].
      2001- [cit. 2017-02-26].
      Dostupné z: https://en.wikipedia.org/wiki/Python_(programming_language)

Zajímavý problém nastavene ve chvíli, kdy v dokumentu už nějaké indexy mám
a chci mezi ně přidat další. V této situaci buď přepišu čísla nebo použiju
automatické číslování indexů::

   Python [#]_ je programovací jazyk.

   .. [#] Python...

U automatického číslování stačí zjistit, kde se nachází předchozí / další index
a podlé toho správně vložít nový řádek s novým indexem mezi už popsané indexy
na konci souboru.

Obrázky
-------

Vkládájí se pomocí::

   .. image:: http://example.org/img.png

Citace
------

Citovaný text začíná odsazením od začátku řádku (3 mezery)::

   ...Toto je první odstavec citovaného textu, který je odsazen od začátku
   ...řádku třemi mezerami (použít místo teček, ty jsou jen pro ilustraci).

   ...Toto je další citovaný odstavec.

Dělící čára
-----------

Alias horizontální čára se značí jakýmkoliv interpunkčním znaménkem, pričemž
nejpoužívanější je pomlčka. Ta se musí navíc čtyřikrát opakovat a okolí ní
musí být prázdné řádky::

   Toto je řádek před dělící čárou.

   ----

   Toto je řádek za dělící čárou.

Zdrojové kódy
-------------

1. jednořákové

   * kód je uvnitř textu, značí se dvěmi zpětnými uvozovkami na obou stranách::

        Stiskni klávesovou zkratku ``CTRL + LSHIFT + V`.

2. víceřádkové

   * zde je mnoho variant, jak takový blok zapsat:

     a) dvojtečky na začátku řádku (zmizí při konverzi na jiný formát)::

           ::

              Toto je zdrojový kód zalomený
              přes dva řádky

     b) dvojtečka za klasickou dvojtečkou (jedna zmizí)::

           Toto je text s dvojtečkou na konci::

              Toto je další zdrojový kód

     c) dvojtečky s mezerou na konci (opět obě zmizí)::

           Toto je obyčejný věta. ::

              Toto je opět zdrojový kód.

     d) na styl Python interpretu::

           >>> print(True)
           True

.. note::

   Uvnitř zdrojového kódu budou jakékoliv RST značky deaktivovány.

Tabulky
-------

1) jednoduché

   * bez nějakých složitých dat či spojených několika buňek v těle tabulky::

        ===============  ===============
        Název sloupce A  Název sloupce B
        ===============  ===============
        1                hodnota pro první řádek ve sloupci B
        2                hodnota pro druhý řádek ve sloupci B
        3                hodnota pro třetí řádek ve sloupci B
        ===============  ===============

   * pokud potřebuji sloučit buňky v záhlaví (jinak ne u této varianty)::

        =====  =====  ========
            Vstup     Výstup
        ------------  --------
          A      B    A nebo B
        =====  =====  ========
        False  False  False
        True   False  True
        False  True   True
        True   True   true
        =====  =====  ========

2) komplexnější

   * v buňkách moho různě formátovat text a též je mohu různě slučovat::

        +-----------+-----------+---------------+
        | Sloupec A | Sloupec B | Sloupec C     |
        +===========+-----------+---------------+
        | blabla    | blabla    | blabla blabla |
        +-----------+-----------+---------------+
        | **blabla**            | - blabla      |
        +-----------------------+ - blabla      |
        | blabla    | blabla    | - blabla      |
        +-----------+-----------+---------------+

   * na rozdíl od jednodušší varianty je těžší na vytvoření, pokud se
     nepoužije nějaké chytré rozšíření do textových editorů

Pokročilé formátování textu
===========================

Komentáře
---------

Pro vlástní poznámky v textu, které jinak nebudou vidět při převodu do jiného
textového formátu::

   .. Toto je komentář.

   .. Toto je taky komentář,
      ale přes dva řádky.

      Tento odstavec je taky považován jako součást komentáře.

Definice pokročile
------------------

Jednotlivé termíny lze ještě dále přidat do jednotlivých skupin, pod které
mohou spadat::

   Jablko : ovoce
      Plod jabloně.

Skupin může být na řádku více, stačí vždy použít na začátku prefix s dvojtečkou
a mezerou::

   Název : skupina1 : skupina2 : skupina3
      Popis

Obrázky pokročile
-----------------

Obrázkům lze nastavit i různé atributy jako v HTML a CSS::

   .. image:: picture.jpg
      :align: center
      :alt: Alternativní text, pokud selže načtení obrázku.
      :class: název_css_selektoru
      :height: 100
      :target: `Odkaz na jinou stránku po kliknutí`_
      :width: 100

Velikost obrázku je defaultně v pixelech. Lze použít i jiné měrné jednotky
jako "cm" či "em", nicméně moderní "rem" ještě nejde využít.

Pokud potřebuji k obrázku přidat viditelný popisek, legendu či skutečně
zarovnat obrázek v dokumentu (nezávisle na jiných elementech v HTML), tak
použiju jinou direktivu::

   .. figure:: picture.jpg
      :alt: Blabla

      Toto je popisek.

      Zde začíná legenda, která může mít i několiv odstavců, tabulky aj.

"figure" direktiva nabízí další dva možné atributy::

   :figclass: název_css_selektoru
   :figwidth: 200

.. note::

   "figwidth" je větší, než velikost samotného obrázku. Jedná se spíše o
   maximální šířku pro popisný text.

Substituce
----------

Aneb nahrazení části textu nečím jiným:

a) jiným textem::

      |Python| je programovací jazyk.

      .. |Python| replace:: C++

b) Unicode znakem::

      |zavináč|

      .. |zavináč| unicode:: U+0040

b) obrázkem do textu::

      Toto je vnořený |obrázek|.

      .. |obrázek| image:: example.png

Speciální seznam pro příkazy
----------------------------

Seznam voleb a přepínačů, které lze použít u nějakého příkazu::

   -a       popis...
   -b TEXT  popis...

   -c, --compile  popis...

   -f FILE, --file=FILE
      popis na dalším řádku...

Metadata
--------

Dodatkové informace k danému RST souboru jako např. číslo verze, datum vydání,
jména autorů, kontakt na ně atd.::

   =========
    Titulek
   =========
   ------------
    Podtitulek
   ------------

   :Autor: Daviebadger
   :Kontakt: davie.badger@gmail.com
   :Datum vydání: 26. února 2017

Buď mohu použít vlastní pojmenování polí nebo použít již předdefinované:

* Author
* Authors
* Organization
* Contact
* Address
* Version
* Status
* Date
* Copyright
* Dedication
* Abstract

.. tip::

   Poslední jmenováné pole "Abstract" lze použít na klasický abstrakt (stručný
   výtah z dokumentu)::

      :Abstract:

         Blablabla.

         Blablabla.

         Blablabla.

HTML metadata
-------------

Jsou určená jen pro HTML soubor, pokud se do nich bude převádět obsah RST
souboru::

   .. meta::
      :charset=utf-8:
      :description: Popisek stránky.
      :keywords: Klíčová slova.

Pro nastavení textu v záložce (HTML titulku) je třeba napsat::

   .. title:: Název titulku

Direktivy
---------

Jsou takové konstrukce, pomocí kterých lze rozšiřovat funkcionalitu (značení)
v RST dokumentu. Setkali jsme se s nimi už u odkazů, obrázku či komentářů.
Začátek řádku vždy začinal na dvě tečky::

   ..

Obecně direktivy mají následující syntaxi::

   .. název_direktivy:: argument
      :název_atributu: hodnota

      Obsah direktivy

U všech direktiv lze použít tyto obecné atributy:

* class

  * název "class" selektoru v CSS, pomocí kterého chci sám nastylovat
    direktivu::

       .. tip::
          :class: název_třídy1 název_třídy2

          Text

* name

  * dodatečný text pro direktivu, platné zejména u obrázku::

       .. image:: pc.png
          :name: Počítač

Výčet všech zabudovaných direktiv lze najít na stránce
http://docutils.sourceforge.net/docs/ref/rst/directives.html

Obsah
"""""

Automatické vygenerování obsahu (bude zjevné při převodu na jiný textový
formát)::

   .. contects::

   nebo

   .. contents:: Obsah

Taktéž mohu uvést hloubku, tj. do jaké úrovně nadpisů se mají zobrazit
odkazy v obsahu::

   .. contents::
      :depth: 3

Číslování nadpisů
"""""""""""""""""

Jednotlivé nadpisy budou mít číselný prefix ve tvaru "1.", "1.1." atd.::

   .. sectnum::

Lze i nastavit, od kolika se ma začít počítat::

   .. sectnum::
      :start: 5

Rubriky
"""""""

Nadpisek pro odstavce, pričemž tento nadpis nebude zobrazen v obsahu. Zpravidla
se používá pro vytvoření patičky::

   .. rubric:: Footnotes

   .. [1] Bla bla bla.

Speciální text
""""""""""""""

Takový ten text, který bývá na stránkách zobrazen v nějakém barevném boxu
podle svého významu. Totéž lze docílit i v RST::

   .. tip::

      Toto je text s nějakým tipem pro čtenáře.

RST má tyto zabudované direktivy se speciálním textem:

* attention
* caution
* danger
* error
* hint
* important
* note
* tip
* warning

Vylepšený zdrojový kód
""""""""""""""""""""""

Lze nastavit číslování řádku a zvýraznit syntaxi, pokud jde o kód z nějakého
programovacího či značkovacího jazyka nebo konfiguračního souboru::

   .. code:: python
      :number-lines: 1

      def my_function():
          pass

Postranní panel
"""""""""""""""

Panel, který se objeví naboku vedle textu::

   .. sidebar:: Titulek postraního panelu
      :subtitle: Volitelný podtitulek

      Samotný obsah.

Textové role
------------

Nějakému označenému textu může být přisouzena nějaká textová role, např.
aby byl kurzívou. Tento text lze označit buď klasickými hvězdičami na obou
stranách nebo pomocí textové role::

   :emphasis:`Toto je text kurzívou.`

Vlastní textové role
""""""""""""""""""""

Pokud chci vytvořit vlastní textovou roli (platí jen pro krátké texty) a
tímpadem jinak nastylovat označený text, tak pomohu podle následujícího
postupu:

1. vytvořit novou roli před samotným použitím::

      .. role:: název_role

2. využít ji v textu::

      :název_role:`Text pro tuto roli.`

3. nastylovat pomocí CSS danou roli, která bude mít stejnojmenný název "class"
   elementu

   * vyrendrovaná role v HTML vypadá následovně::

        <p><span class="název_role">Text</p>

.. note::

   CSS pro RST lze aplikovat buď u Sphinxu (dokumentační nástroj pro Python
   spolu s RST) nebo u konvetorů (rst2html / rst2html5), kde lze uvést cestu
   k CSS souboru, který se má použít.

Zabudované textové role
"""""""""""""""""""""""

* sup (superscript)

  * text v horním indexu::

       Tento :sup:`Text` je v hodním indexu.

* sub (subscript)

  * text v dolním indexu::

       Tento :sub:`Text` je v dolním indexu.

* PEP

  * pro hypertextový odkaz na nějaký PEP (Python Enhancement Proposal)::

       Viz :PEP:`8`.

* RFC

  * dokumenty pro internetové protokoly RFC (Request For Comments)::

       Viz :RFC:`2822`.

Načtení obsahu jiného souboru
"""""""""""""""""""""""""""""

Na dané označené místo se vložít obsah z jiného souboru, ke kterému musím uvést
relativní cestu::

   Za tento odstavec se načte obsah ze souboru "tutorial.rst".

   .. include:: tutorial.rst

.. _reStructuredText: Dostupné z: https://en.wikipedia.org/wiki/ReStructuredText
.. _Docutils: http://docutils.sourceforge.net/
.. _Sphinx: http://www.sphinx-doc.org/en/stable/
