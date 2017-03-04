========
 Sphinx
========
----------------------------------------------------------------
 Nástroj pro vytvaření dokumentací pro projekty psané v Pythonu
----------------------------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:Licence: CC BY-SA 4.0

:Abstract:

   `Sphinx`_ ...

.. contents:: Obsah

TODO
====

1. jak nastavit docstringy pro jednotlivé styly

Formátování docstringů
----------------------

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

   - nejlépe stručný, jednořádkový popisek, ve kterém není zmíňka o názvu
     funkci či názvu jeho parametrů::

      def secti(a, b):
          """
          Součet dvou čísel.
          """

2. rozšiřující popisek

   - pokud nestačí krátký popisek, tak lze napsat do dalšího odstavce delší
     popisek, který však nesmí (neměl by) popisovat samotný kód::

      def foo():
          """
          Krátký popisek.

          Delší popisek přes
          dva řádky.
          """

3. popis jednotlivých parametrů

   - o jaký parametr se jedná? jaký jeho význam? jak má vypadat argument pro
     něj? je volitelný? má nějakou výchozí hodnotu? ::

      Args:
          x: Popis parametru.
          y (int): Popis parametru.
          z (str, optional): Popis parametru.
          *args: Popis parametru.
          **kwargs: Popis parametru.

   - možná je i explicitnější varianta se slovem "Arguments" místo "Args"

4. popis atributů

   - u tříd, přičemž platí stejný postup, jako u parametrů::

      Attributes:
          x (int): Popis atributu.

   - speciální property atributy se popisují až ve své metodě (pokud je použit
     setter a getter najednou, tak je v geteru)::

      @property
      def foo(self):
          """
          int: Popis property atributu.
          """

5. popis návratové hodnoty

   - jestiže funkce vrací nějakou hodnotu, tak jakou? jakého typu je? jaký má
     význam? ::

      Returns:
          Popis návratové hodnoty bez uvedení datového typu.

      Returns:
          int: Popis návratové hodnoty.

   - pokud se jedná o generátor, tak místo slůvka "Returns" bude "Yields"::

      Yields:
          int: Popis návratové hodnoty.

6. popis možných errorů

   - jestli se někdě v kódu volá "raise" pro vyvolání erroru, tak by o tom
     měl být uživatel informován, za jakých podmínek to může nastat a jaký
     error bude vyvolán::

      Raises:
          ValueError: Popis, za jakých podmínek to nastane.

7. příklady

    - ukázka použítí dané funkce ve stylu interpretu::

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

   - nejlépe stručný, jednořádkový popisek, ve kterém není zmíňka o názvu
     funkci či názvu jeho parametrů::

      def secti(a, b):
          """
          Součet dvou čísel.
          """

2. informace o budoucím odstranění objektu (volitelné)

   - varování pro uživatele, aby v budoucnu u vyšších verzí nespoléhali na
     dané funkci (není už spravována), neboť v tu dobu už nebude existovat::

      .. note:: Deprecated in NumPy 1.6.0
                `o_old` will be removed in NumPy 2.0.0, it is replaced by
                `o_new` because the latter works also with array subclasses.

3. rozšiřující popisek

   - pokud nestačí krátký popisek, tak lze napsat do dalšího odstavce delší
     popisek, který však nesmí (neměl by) popisovat samotný kód::

      def foo():
          """
          Krátký popisek.

          Delší popisek přes
          dva řádky.
          """

4. popis jednotlivých parametrů

   - o jaký parametr se jedná? jaký jeho význam? jak má vypadat argument pro
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

   - u popisu datových typů lze použít i nové typové anotace podle :PEP:`484`::

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

   - jestiže funkce vrací nějakou hodnotu, tak jakou? jakého typu je? jaký má
     význam? ::

      Returns
      -------
      int
          Popis návratové hodnoty bez uvedení datového typu (nedoporučuji).

   - když funkce vrací více hodnot, tak je mohu více popsat (obdobně jako u
     parametrů)::

      Returns
      -------
      err_code : int
          Popis návrtového hodnoty `err_code`.
      err_msg : str or None
          Popis návratové hodnoty `err_msg`.

   - pokud se jedná o generátor, tak místo slůvka "Returns" bude "Yields"::

      Yields
      ------
      int
          ...

6. popis ostatních nedůležitých parametrů (volitelné)

   - když má funkce mnoho parametrů, tak do sekce "Parameters" vypíšu jen ty
     nejdůležitější a nejpoužívanější, zbytek mohu umístit zde ve stejném
     duchu::

      Other Parameters
      ----------------
      x : int
          ...

7. popis možných errorů

   - jestli se někdě v kódu volá "raise" pro vyvolání erroru, tak by o tom
     měl být uživatel informován, za jakých podmínek to může nastat a jaký
     error bude vyvolán::

      Raises
      ------
      ValueError
          Popis, za jakých podmínek to nastane.

8. doporučení pro uživatele (volitelné)

   - zda-li by se uživatel neměl podívat ještě podrobně na nějaký jiný objekt::

      See Also
      --------
      název_funkce1_ze_stejného_modulu
      název_funkce2_ze_stejného_modulu : Rychlý popisek funkce.
      název_funkce3_ze_stejného_modulu, název_funkce4_ze_steného_modulu, ...
      vnořený_modul.název_funkce : Popisek.
      jiný_balíček.název_modulu_název_funkce : Popisek.

9. poznámky (volitelné)

   - dodatečné poznámky, o kterých by mohl zvídavý uživatel vědět, např. proč
     bych zvolen daný algoritmus::

      Notes
      -----
      Blablabla.

10. reference a citace (volitelné)

    - pokud v předchozí sekci o poznámkách nebo jiné napíšu horní index s
      odkazem, tak samotné odkazy a citace vložím do této sekce
    - cituje se podle standardních zvyklostí::

       .. [1] Blablabla.

11. příklady

    - ukázka použítí dané funkce ve stylu interpretu::

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

   - tato sekce se nachází hned za sekcí "Parameters" (parametry v
     konstruktoru)::

      Attributes
      ----------
      x : float
          Popis `x` atributu.

   - pokud atribut je brán jako property, tak se vypíše jen jeho název a
     zbytek dokumentace je v samotné property metodě::

      Attributes
      ----------
      název_property_atributu
      y : int
          Popis `y` atributu.

2. popis metod (volitelné)

   - není to vůbec nutné, nicméně pokud má třída mnoho veřejných metod, ale jen
     pár je velmi užitečných, tak je možné je vyjmenovat (hned za sekcí s
     atributami)::

      Methods
      -------
      název_metody(parametr=argument)
          Popisek metody.

.. note::

   Dokumentace konstruktoru se píše v rámci docstringu pro třídu a nikoliv
   v samotné magické metodě.
