========
 Sphinx
========
----------------------------------------------------------------
 Nástroj pro vytvaření dokumentací pro projekty psané v Pythonu
----------------------------------------------------------------

:Abstract:

   `Sphinx`_ je dokumentační generátor, který vznikl pro interní potřebu
   Pythonu jako takového. Byl napsán Georgem Brandlem a od roku 2008 je vyvíjen
   zcela otevřeně (open source).

   Tento nástroj využívá drtivá většina balíčků pro Python. Mezi nejznámnější
   lze jmenovat Django, Flask, Requests, Virtualenv atd. Dokonce i samotná
   dokumentace Pythonu a jeho standardní knihovny jej využívá.

   Sphinx staví zejména na značkovacím jazyku reStructuredText, který je velmi
   flexibilní a lze do něj přidat nové značky. Taktéž umí převést celou
   dokumentaci na jiné formátovy, jako je HTML či PDF. V neposlední řade si
   lze napsat vlastní rozšíření do Sphinxu.

.. contents:: Obsah

Instalace
=========

Příkazem::

   $ pip install sphinx

Ovládání
========

Vytvoření adresáře s dokumentací
--------------------------------

Pro vytvoření adresáře se Sphinx dokumentací se použíje následující skript,
který je třeba spustit z rootu projektu::

   $ sphinx-quickstart

Jedná se o průvodce, který se ptá na několik věci, a na základě nich vytvoří
patřičnou adresářovou strukturu spolu s konfiguračním souborem.

K otázkám lze odpovídat buď vlastními hodnotami nebo nechat defaultní hodnoty
v hranatých závorkách pomocí ENTER.

**Hlavní otázky v průvodci:**

1. root path for documentation

   * cesta do adresáře s dokumentací
   * zpravidla se uvadí hodnota "doc" (documentation) nebo "docs"
     (documentation files)

2. separate source and build directories

   * zda se má zvlášť do adresářů separovat zdrojový obsah dokumentace a její
     build
   * nechat výchozí hodnotu (n)

3. name prefix for templates and static dir

   * jaký prefix bude mít složka "templates" a "static", pokud bych chtěl
     tvořit vlastní vzhled HTML stránek
   * nechat výchozí hodnotu (_)

4. project name

   * název projektu

5. author name(s)

   * název autora/ů

6. project version

   * verze projektu
   * Sphinx rozlišuje termíny "version" pro hlavní verzi projektu (např. Python
     3.5) a "release" pro jednotlivé subvydání (např. Python 3.5.2)

7. project release

   * release projektu
   * pokud nechci duální verzování (zvlášť pro "version" a "release"), tak
     nechám defaultní hodnotu (stejná jako verze projektu)

8. project language

   * jazyk dokumentace
   * pokud nebude dokumentace psaná v angličtině (výchozí možnost), tak musím
     uvést kód jazyka, který bude použít
   * pro češtinu platí kód "cs", ostatní kódy lze najít na stránce
     http://www.sphinx-doc.org/en/stable/config.html#confval-language

9. source file suffix

   * suffix (koncovka) souborů, ve kterých bude dokumentace
   * nechat výchozí hodnotu (.rst)

10. name of you master document

    * název hlavního souboru (úvodní soubor s úvodem a obsahem)
    * nechat výchozí hodnotu (index)

11. create Makefile

    * zda se má vytvořit soubor "Makefile", pomocí kterého se bude ovládat
      celá dokumentace
    * nechat výchozí hodnotu (y)

.. note::

   Na zde nezmíněné otázky lze všude odpovídat klávesou ENTER s ponecháním
   výchozích hodnot. Akorát u poslední otázky na "Windows command file" je
   třeba odpovědět "n", pokud nepoužívám OS Windows.

Adresářová struktura dokumentace
--------------------------------

Po dokončení průvodce by se ve zvoleném dokumentačním adresáři měla vytvořit
následující adresářová struktura::

   _build/
   _static/
   _templates/
   conf.py
   index.rst
   Makefile

.. note::

   Adresář "_build/" je zpravidla ignorován Gitem (je třeba přidat do
   ".gitignore" souboru.

Do této struktury se vládájí RST soubory. Ty je možné i dále strukturovat
do vnořených adresářů::

   _build/
   _static/
   _templates/
   tutorial/
     conditions.rst
     intro.rst
     loops.rst
   api.rst
   cli.rst
   conf.py
   faq.rst
   index.rst
   MakeFile

Definování struktury dokumentace
--------------------------------

V hlavním souboru "index.rst" se zpravidla definuje obsah dokumentace s
nějakým doprovodným textem. Pro vložení obsahu je důležitá direktiva "toctree",
viz příklad::

   .. toctree::
      :maxdepth: 2

      api
      cli
      faq
      tutorial/intro
      tutorial/conditions
      tutorial/loops

Tato direktiva se může vyskytovat několikrát v souboru. Má volitelný parametr
"maxdepth", pomocí kterého se uvadí maximální hloubka nadpisů (jejich úrovně).
Defautlně se zobrazí odkazy na každý nadpis z daného souboru, pokud neuvedu
jinak.

V rámci relativních odkazů na soubory se uvádí jen názvy souborů bez koncovek.
U souborů ve vnořených adresářích je třeba vypsat i název adresáře odděleného
lomítkem.

Sphinx bude respektovat pořadí souborů v obsahu a na základě toho bude sám
generovat odkazy na další / předchozí téma v rámci dokumentace.

Nastavení dokumentace
---------------------

Veškeré nastavení dokumentace se nachází v konfiguračním souboru "conf.py"
(je automaticky vytvořen), pomocí kterého lze různě upravovat funkčnost a
chování Sphinxu, potažmo celé dokumentace.

Seznam všech konfigurovatelných hodnot je na stránce
http://www.sphinx-doc.org/en/stable/config.html.

Obecné nastavení
^^^^^^^^^^^^^^^^

* default_role

  * nastavení výchozí role pro text označený jako::

       `blabla`

  * např. pro vytváření cross-reference na Python objekty by to bylo::

       default_role = "py:obj"

* extensions

  * seznam rozšíření pro Sphinx::

       extensions = [
         "sphinx.ext.napoleon",
         "název_externího_rozšíření"
       ]

  * seznam zabudovaných Sphinx rozšíření je na stránce
    http://www.sphinx-doc.org/en/stable/extensions.html#extensions
  * u externích rozšíření je důležitý, aby šli importovat (uvádí se název
    balíčku)

* primary_domain

  * název primární domény, defaultně je "py", proto lze psát zkráceně místo
    ":py:mod:" jen "mod"
  * lze přepsat na hodnoty:

    * None
    * c
    * cpp
    * js
    * rst

* rst_epilog

  * RST značky, které budou přidány na každý konec souboru (jen při buildu)::

       rst_epilog = """
       .. |psf| replace:: Python Software Foundation
       """

* rst_prolog

  * RST značky, které budou přidány na každý začátek souboru ještě před samotný
    H1 nadpis (taktéž jen při buildu)

Nastavení projektu
^^^^^^^^^^^^^^^^^^

* author

  * jméno autora projektu (může být i jako organizace či název firmy)

* copyright

  * autorské právo ve formátu::

       2000, jméno_autora

* highlight_language

  * jméno jazyka pro zvýrazňování kódu pomocí "::" syntaxe, defaultně je
    "python3"
  * pokud nechci žádné zvýrazňování kódu, tak je třeba napsat::

        highlight_language = "none"

* pygments_style

  * název stylu, který bude obarvovat zdrojové kódy, defaultně je "sphinx"

* project

  * jméno projektu, pro kterého je vytvořena dokumentace

* release

  * číslo verze vydání (explicitnější varianta), které může být stejné jako
    "version" nebo jiné, např. "2.6.0rc1"

* version

  * číslo verze, zpravidla ve formátu "X.Y"

Nastavení překladů
^^^^^^^^^^^^^^^^^^

* language

  * kód jazyka, ve kterém je psaná dokumentace
  * seznam kódu lze najít na stránce
    http://www.sphinx-doc.org/en/stable/config.html#confval-language

Nastavení HTML buildu
^^^^^^^^^^^^^^^^^^^^^

* html_context

  * slovník s hodnotami, které se mají poslat do každé šablony

* html_favicon

  * cesta k favicon obrázku (ikonka na záložce), který má velikost 16x16 nebo
    32x32

* html_logo

  * cesta k logu, které se vyrendruje v horní části sidebaru (velikost by
    neměla překročit 200px)

* html_show_sourcelink

  * zda se má nebo nemá u každé stránky zobrazivat i odkaz na zdrojový RST
    souboru (defaultně True)

* html_show_copyright

  * zda se má nebo nemá zobrazovat copyright (defaultně True)

* html_show_sphinx

  * zda se má zobrazit nebo nemá informace, že dokumentace je vytvořena
    pomocí Sphinxu (defaultně True)

* html_theme

  * název šablony / vzhledu, jak bude vypadat dokumentace, defaultně je
    "alabaster"
  * ostatní defaultní styly lze najít na stránce
    http://www.sphinx-doc.org/en/stable/theming.html#builtin-themes

  .. note::

     Nejvíce konfiguravatelný je vzhled "classic" (alá dokumentace pro Python
     2).

* html_theme_options

  * konfigurační možnosti / úpravy pro daný HTML vzhled

* html_title

  * titulek (text v záložce), respektive suffix za každým H1 titulkem, který
    přepíše výchozí suffix::

       <název_projektu> v<revision> documentation

Build dokumentace
-----------------

Pro vytvoření samotné dokumentace v HTML či jiném formátu je nutné vytvořit
tzv. "build", kdy se vezmou zdrojové texty a ty se přetaví na příslušný formát.
Buildovat dokumentaci lze pomocí "Makefile" souboru a to příkazem::

   $ make název_buildu
   $ make html

Výčet všech možných buildů lze zobrazit pomocí::

   $ make help

Kromě samotného buildu umí Sphinx exekutuovat i externí příkazy, které se
mají provést nad danou dokumentací, např. kontrola interlinků nebo vytvoření
souborů pro překlady.

Nadstavba Sphinxu pro RST
=========================

Direktivy
---------

Sphinx přidává do RST své vlastní direktivy.

Tvorba obsahu
^^^^^^^^^^^^^

toctree
"""""""

Pro vkládání centrálního obsahu, viz sekce `Definování struktury dokumentace`_.
U lokálních obsahů (jen pro daný soubor) stačí použít klasickou RST "contents"
direktivu.

Možnosti úpravy:

* změna H1 titulku

  * pokud potřebuji mít v obsahu jiný H1 titulek, než který je v daném souboru,
    mohu si upravit pomocí syntaxe::

       .. toctree::

          Vlastní název titulku <název_souboru>

* zobrazení jen titulků ze souborů

  * nižší úrovně nadpisů (H2, H3, ...) nebudou vidět::

       .. toctree::
          :titlesonly:

* číslování sekcí

  * jednotlivé položky v obsahu budou očíslovány ve stylu 1.1, 1.1.2 atd.::

       .. toctree::
          :numbered:

* popisek obsahu

  * pro vložení textu před samotný obsah::

       .. toctree::
          :caption: Obsah:

       .. Je to samé jako:

       Obsah:

       .. toctree:

.. note::

   Jestliže se v dokumentačním adresáři nachází soubor, který není zmíněň
   nikde v "toctree" direktivě, např. chci odkazát na něj na jiném místě, tak
   Sphinx hodí červeně hlášku o problému s nekonzistentcí.

   Pro zbazení se této hlášky je třeba říct Sphinxu, aby tyto soubory v rámci
   konzistence ignoroval. Na to je třeba taktéž použít "toctree" direktivu,
   ale uvést v něm jen ty soubory, které nebudou v obsahu::

      .. toctree::
         :hidden::

         foo

Tvorba slovníčku
^^^^^^^^^^^^^^^^

glossary
""""""""

Slovníček na způsob definic v RST, akorát přes "glossary" direktivu::

   .. glossary::

      termín 1
         Popis termínu 1.

      termín 2 : název_skupiny
         Popis termínu 2.

Pokud nějaké termíny mají úplně totožný popisek, mohu použít zkratku::

   .. glossary::
      termín 1
      termín 2
         Popis obou termínů.

.. tip::

   Pro odkazování na termín ve slovníčku (může na to být vyhrazena speciální
   stránka) se používá role "term"::

      Pro více informací se podívej na :term:`termín 1`.

Informace k verzím
^^^^^^^^^^^^^^^^^^

versionadded
""""""""""""

V jaké verzi byla přidána nová funkcionalita k danému objektu::

   Popisek nové featury...

   .. versionadded:: 1.0

Do této direktivy lze napsat dovnitř i nějaký další popisný text, ale moc se
toho nevyužívá (např. v Python dokumentaci). Důležitý je popisek před touto
direktivou.

versionchanged
""""""""""""""

V jaké verzi se co a jak změnilo::

   .. versionchanged:: 1.2

      Bla bla bla.

.. note::

   Podle Sphinxu by neměl být prázdný řádek mezi názvem direktivy a popiskem,
   co se změnilo, aby text plynule navazoval na jendom řádku. Nicméně podle
   HTML buildu v nejnovějším Sphinxu to může být i s prázdným řádkem.

deprecated
""""""""""

Od jaké verze již není spravována daná funkcionalita (může být v nějaké
budouci verzi odstraněna úplně). Je vhodné dopsat i informační text, jaká
nahrádu (pokud vůbec) by měl uživatel použít::

   .. deprecated:: 1.3

      Use :func:`foo` instead.

Odkaz na další sekce
^^^^^^^^^^^^^^^^^^^^

seealso
"""""""

Pro zvídavé uživatele, aby se ještě podívali na další sekce / texty o nečem
souvísejícím::

   .. seealso::

      Module :mod:`json`
         Bla bla bla.

      `Blabla <http://link>`_
         Bla bla bla.

.. note::

   Tělo direktivy je ve formátu RST definic.

Role
----

Sphinxové role zpravidla tvoří nějaký odkaz na nějaké jiné místo, pokud není
uvedeno jinak (je jiný význam). Text v odkazu se vezme podle cíle, na který
se odkazuje. Jestlíže chci však vlastní text, použiju syntaxi jako u odkazů::

   :název_role:`Vlastní text odkazu <odzkaz>`

doc
"""

Pro odkazování na jiné soubory::

   :doc:`název_souboru`

Opět lze použít jak relativní, tak i absolutní cestu z dokumentačního adresáře.

ref
"""

Pro odkazování na jiné sekce (nadpisy) v jiných souborech. Nejprve je třeba
označit nadpis pro odkazování::

   .. _moje-označení-nadpisu:

   Nadpis
   ======

a posléze na něj odkázat pomocí "ref" role::

   Podívej se na :ref:`moje-označení-nadpisu`.

term
""""

Pro odkazování do slovníku, viz direktiva `glossary`_::

   :term:`Název termínu`

download
""""""""

Pro automatické stažení souborů::

   :download:`cesta_k_souboru`

.. note::

   Pokud chci zbuildovat dokumentace i pro jiné formáty a nemám soubory
   ke stažení nikde veřejně připravené, tak by nebylo dobré, aby se v textu
   vyskytoval nefunkční odkaz.

   Aby šly vidět odkazy jen pro HTML build, je třeba napsat::

      .. only:: builder_html

         Ke stažení :download:`ZDE <cesta_k_souboru>`.

Zvýraznění zdrojového kódu
--------------------------

Kromě klasického Python interpretu::

   >>> print(True)
   True

má Sphinx i svoje vlastní direktivy pro bloky kódu.

highlight
"""""""""

Sphinx bere každý zdrojový kód pomocí "::" syntaxe jako Python kód a pokusí se
pomocí `Pygments`_ (nástroj na zvýraznění a zbarvení syntaxe) zvýraznit klíčová
Python slova, pokud se vyskytují ve zdrojovém textu.

Pro deaktivaci tohoto chování je třeba napsat::

   .. highlight:: none

Naopak, pokud chci nastavit globálně v souboru nějaký jazyk (kromě defaultního
Pythonu), tak zpravidla na začátek souboru napíšu někam::

   .. highlight:: c

Výčet všech podporovaných programovacích jazyků a jiných formátu lze najít na
http://pygments.org/languages/.

.. important::

   Název programovacího jazyku musí být jednoslovný a vše malými písmeny. Např.
   pro Python jsou tyto možnosti:

   1. python (verze 2)
   3. python3

code-block
""""""""""

Alternativa k `highlight`_ direktivě, pokud chci jen na nějakých místech použít
jiný programovací jazyk, aniž bych musel aktivovat / deaktivovat jazyky::

   .. code-block:: python3

      print(True)

Pro obyčejný text je třeba na místo programovacího jazyka napsat::

   .. code-block:: text

      ...

Pro zobrazení čísla řádků je třeba použít "linenos" volbu::

   .. code-block:: python3
      :linenos:

literalinclude
""""""""""""""

Pro vkládání kódu, který už je někde v nějakém souboru (musí být v
dokumentačním adresáři)::

   .. literalinclude:: název_souboru.py

Používá se zpravidla relativní cesta. Avšak, pokud jsou příklady kódu na
nějakém centrálním místě, např::

   doc/
      _build/
      _static/
      _templates/
      examples/
      conf.py
      index.rst

tak lze použít i absolutní cestu::

   .. literalinclude:: /examples/název_souboru.py

Jestliže se nejedná o Python soubor, ale o nějaký jiný, tak musím uvést i
atribut pro jazyk::

   .. literalinclude:: název_souboru.py
      :language: c

Stejně jako u `code-block`_ direktivy lze použít číslování řádků::

   .. literalinclude:: název_souboru.py
      :linenos:

.. tip::

   Pokud chci z ukázkového Python souboru vytáhnout jen nějakou část, mohu
   použít "pyobject" atribut, který bude odkazovat na třídu / metodu nebo
   funkci::

      .. literalinclude:: název_souboru.py
         :pyobject: Timer.start

Další vychytávky (atributy) lze najít na
http://www.sphinx-doc.org/en/stable/markup/code.html#directive-literalinclude.

Domény
------

Soubor direktiv a rolí, které slouží k popisku a odkazování na objekty v
jednotlivých programovacích jazycích. Sphinx už není úzce vázán na Python,
ale podporuje i dokumentaci pro jazyky C, C++ a Javascript.

Python domény
^^^^^^^^^^^^^

http://www.sphinx-doc.org/en/stable/domains.html#the-python-domain

.. Cross-reference buď explicitně přes ":py:mod:" nebo zkráceně ":mod:"

C domény
^^^^^^^^

http://www.sphinx-doc.org/en/stable/domains.html#the-c-domain

C++ domény
^^^^^^^^^^

http://www.sphinx-doc.org/en/stable/domains.html#id2

Rozšíření pro Sphinx
====================

Napoleon
--------

Formátování docstringů
^^^^^^^^^^^^^^^^^^^^^^

Dokumentační řetězce (docstringy) se dají psát pro každý modul (soubor),
funkce, třídy a metody::

   """
   Dokumentace modulu.
   """

   import this


   def foo():
       """
       Dokumentace funkce.
       """


   class Bar():
       """
       Dokumentace třídy.
       """

       def baz(self):
           """
           Dokumentace metody.
           """

Při použítí Sphinxu lze psát docstringy i pro konstaty v modulech::

   NAZEV_KONSTANTY = False
   """
   Dokumentace konstanty
   """

.. note::

   Někteří mohou preferovat i následující varianty::

      def foo():
          """Krátká dokumentace funkce"""


      def bar():
          """Dokumentace funkce

          Text.
          """


      def baz():
          """Dokumentace funkce

          Text.
          """

Do docstringů lze psát dokumentaci k danému objektu buď podle svého uvažení
nebo podle nějakého existujícího stylu. Obecně nejrozšířenější je styl Google,
kterému zdatně sekunduje v akademickém světě styl Numpy.

.. note::

   Doporučená délka řádku v rámci docstringů, ale i komentářů je podle :PEP:`8`
   72 znaků. Nicméne nic hrozného se nestane, pokud řádek bude mít 75 znaků
   (celkově 79 - 4 mezery pro odsazení = 75), jako to doporučeno u Numpu stylu.

.. tip::

   V docstringech lze použít značkovací jazyk reStructuredText, pokud je to
   třeba. Hodí se to zejména pro tvorbu seznamů či tabulek.

Styl Google
^^^^^^^^^^^

Na rozdíl od Numpu stylu není příliš striktní na pořadí jednotlivých sekcí,
nicméně nějakou strukturu je třeba zachovat. Dále může být kratší co do počtu
řádku v docstringech, avšak je třeba více odsazovat a tím se křátí délka řádku.

.. note::

   K původnímu (originálnímu) stylu Google přibylo od autora Napoleon rozšíření
   pro Sphinx několik nových sekcí navíc.

Popis Google sekcí
""""""""""""""""""

1. krátký úvodní popisek

   * nejlépe stručný, jednořádkový popisek, ve kterém není zmíňka o názvu
     funkci či názvu jeho parametrů::

        def secti(a, b):
            """
            Součet dvou čísel.
            """

2. rozšiřující popisek

   * pokud nestačí krátký popisek, tak lze napsat do dalšího odstavce delší
     popisek, který však nesmí (neměl by) popisovat samotný kód::

        def foo():
            """
            Krátký popisek.

            Delší popisek přes
            dva řádky.
            """

3. popis jednotlivých parametrů

   * o jaký parametr se jedná? jaký jeho význam? jak má vypadat argument pro
     něj? je volitelný? má nějakou výchozí hodnotu? ::

        Args:
            x: Popis parametru.
            y (int): Popis parametru.
            z (str, optional): Popis parametru.
            *args: Popis parametru.
            **kwargs: Popis parametru.

   * možná je i explicitnější varianta se slovem "Arguments" místo "Args"

4. popis atributů

   * u tříd, přičemž platí stejný postup, jako u parametrů::

        Attributes:
            x (int): Popis atributu.

   * speciální property atributy se popisují až ve své metodě (pokud je použit
     setter a getter najednou, tak je v geteru)::

        @property
        def foo(self):
            """
            int: Popis property atributu.
            """

5. popis návratové hodnoty

   * jestiže funkce vrací nějakou hodnotu, tak jakou? jakého typu je? jaký má
     význam? ::

        Returns:
            Popis návratové hodnoty bez uvedení datového typu.

        Returns:
            int: Popis návratové hodnoty.

   * pokud se jedná o generátor, tak místo slůvka "Returns" bude "Yields"::

        Yields:
            int: Popis návratové hodnoty.

6. popis možných errorů

   * jestli se někdě v kódu volá "raise" pro vyvolání erroru, tak by o tom
     měl být uživatel informován, za jakých podmínek to může nastat a jaký
     error bude vyvolán::

        Raises:
            ValueError: Popis, za jakých podmínek to nastane.

7. příklady

   * ukázka použítí dané funkce ve stylu interpretu::

        Example:
            Popis příkladu::

                $ python example.py

        Examples:
            Popis příkladu.

            >>> print(True)
            True

Ostatní sekce:

1. poznámky pro uživatele::

      Note:
          Toto je poznámka.

      Notes:
          Toto je první poznámka.

          Toto je druhý poznámka.

2. varování pro uživatele::

      Warning:
          Toto je první varování.

      Warnings:
          Toto je první varování.

          Toto je druhé varování.

3. TODO::

      Todo:
          * první úkol
          * druhý úkol
          * třetí úkol

Styl Numpy
^^^^^^^^^^

Na rozdíl od Google stylu je daleko striktnější na pořadí jednotlivých sekcí
pro popisek objektu, parametrů, návratových hodnot atd. a taky delší co do
počtu řádků v docstringech.

Popis Numpy sekcí
"""""""""""""""""

1. krátký úvodní popisek

   * nejlépe stručný, jednořádkový popisek, ve kterém není zmíňka o názvu
     funkci či názvu jeho parametrů::

        def secti(a, b):
            """
            Součet dvou čísel.
            """

2. informace o budoucím odstranění objektu (volitelné)

   * varování pro uživatele, aby v budoucnu u vyšších verzí nespoléhali na
     dané funkci (není už spravována), neboť v tu dobu už nebude existovat::

        .. note:: Deprecated in NumPy 1.6.0
                  `o_old` will be removed in NumPy 2.0.0, it is replaced by
                  `o_new` because the latter works also with array subclasses.

3. rozšiřující popisek

   * pokud nestačí krátký popisek, tak lze napsat do dalšího odstavce delší
     popisek, který však nesmí (neměl by) popisovat samotný kód::

        def foo():
            """
            Krátký popisek.

            Delší popisek přes
            dva řádky.
            """

4. popis jednotlivých parametrů

   * o jaký parametr se jedná? jaký jeho význam? jak má vypadat argument pro
     něj? je volitelný? má nějakou výchozí hodnotu? ::

        Parameters
        ----------
        x
            Popis parametru `x` bez uvedení datového typu (nedoporučuji).
        y : int or tuple of int
            Popis parametru `y` s uvedením datového typu.
        z : list of str, optional
            Popis volitelného parametru `z` s uvedením datového typu, který má
            defaultní hodnotu -1.
        *args
        **kwargs

   * u popisu datových typů lze použít i nové typové anotace podle :PEP:`484`::

        Parameters
        ----------
        a : List[int]
            Popis parametru `a`.

   .. tip::

      Pokud parametr očekává, aby argument pro něj nabývál jen konkrétních
      hodnot z nějaké množiny, tak to lze zapsat jako::

         Parameters
         ----------
         b : {"den", "noc"}
             Popis parametru `b`.

5. popis návratové hodnoty

   * jestiže funkce vrací nějakou hodnotu, tak jakou? jakého typu je? jaký má
     význam? ::

        Returns
        -------
        int
            Popis návratové hodnoty bez uvedení datového typu (nedoporučuji).

   * když funkce vrací více hodnot, tak je mohu více popsat (obdobně jako u
     parametrů)::

        Returns
        -------
        err_code : int
            Popis návrtového hodnoty `err_code`.
        err_msg : str or None
            Popis návratové hodnoty `err_msg`.

   * pokud se jedná o generátor, tak místo slůvka "Returns" bude "Yields"::

        Yields
        ------
        int
            ...

6. popis ostatních nedůležitých parametrů (volitelné)

   * když má funkce mnoho parametrů, tak do sekce "Parameters" vypíšu jen ty
     nejdůležitější a nejpoužívanější, zbytek mohu umístit zde ve stejném
     duchu::

        Other Parameters
        ----------------
        x : int
            ...

7. popis možných errorů

   * jestli se někdě v kódu volá "raise" pro vyvolání erroru, tak by o tom
     měl být uživatel informován, za jakých podmínek to může nastat a jaký
     error bude vyvolán::

        Raises
        ------
        ValueError
            Popis, za jakých podmínek to nastane.

8. doporučení pro uživatele (volitelné)

   * zda-li by se uživatel neměl podívat ještě podrobně na nějaký jiný objekt::

        See Also
        --------
        název_funkce1_ze_stejného_modulu
        název_funkce2_ze_stejného_modulu : Rychlý popisek funkce.
        název_funkce3_ze_stejného_modulu, název_funkce4_ze_steného_modulu, ...
        vnořený_modul.název_funkce : Popisek.
        jiný_balíček.název_modulu_název_funkce : Popisek.

9. poznámky (volitelné)

   * dodatečné poznámky, o kterých by mohl zvídavý uživatel vědět, např. proč
     bych zvolen daný algoritmus::

        Notes
        -----
        Blablabla.

10. reference a citace (volitelné)

    * pokud v předchozí sekci o poznámkách nebo jiné napíšu horní index s
      odkazem, tak samotné odkazy a citace vložím do této sekce
    * cituje se podle standardních zvyklostí::

         .. [1] Blablabla.

11. příklady

    * ukázka použítí dané funkce ve stylu interpretu::

         Examples
         --------
         Komentář k prvnímu příkladu.

         >>> print(True)
         True

         Text k druhému příkladu.

         >>> print(False)
         False

Co se týče dokumentace pro třídy, tak tam jsou ještě další dvě sekce:

1. popis atributů

   * tato sekce se nachází hned za sekcí "Parameters" (parametry v
     konstruktoru)::

        Attributes
        ----------
        x : float
            Popis `x` atributu.

   * pokud atribut je brán jako property, tak se vypíše jen jeho název a
     zbytek dokumentace je v samotné property metodě::

        Attributes
        ----------
        název_property_atributu
        y : int
            Popis `y` atributu.

2. popis metod (volitelné)

   * není to vůbec nutné, nicméně pokud má třída mnoho veřejných metod, ale jen
     pár je velmi užitečných, tak je možné je vyjmenovat (hned za sekcí s
     atributami)::

        Methods
        -------
        název_metody(parametr=argument)
            Popisek metody.

.. note::

   Dokumentace konstruktoru se píše v rámci docstringu pro třídu a nikoliv
   v samotné magické metodě.

.. _Sphinx: https://en.wikipedia.org/wiki/Sphinx_(documentation_generator)
.. _Pygments: http://pygments.org/
