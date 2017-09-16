==========
 Markdown
==========
-------------------------------------------------
 Značkový jazyk pro editaci prostého textu (.md)
-------------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

.. highlight:: markdown

Značky
======

Nadpisy
-------

Vlož nadpisy různé úrovně::

   # První úroveň

   ## Druhá úroveň

   ### Třetí úroveň

   #### Čtvrtá úroveň

   ##### Pátá úroveň

   ###### Šestá úroveň

.. note::

   Nadpis první úrovně by se měl v textu vyskytovat jen jednou, neboť se jedná
   o hlavní nadpis dokumentu.

Odstavce
--------

Vlož odstavce::

   První odstavec.

   Druhý odstavec.

.. tip::

   Je-li třeba zalomit text, použije se na konci řádku ``\`` nebo dvě mezery::

      První řádek \
      Druhý řádek \
      Třetí řádek

Zvýraznění textu
----------------

Označ text kurzívou::

   *Text kurzívou.*

Označ text tučným písmem::

   **Text tučným písmem.**

.. note::

   Místo ``*`` lze použít i ``_``::

      _Text kurzívou._
      __Text tučným písmem.__

.. tip::

   Text kurzívou a tučným písmem zároveň::

      *__Text kurzívou a tučným písmem zároveň.__*
      **_Text kurzívou a tučným písmem zároveň._**

Seznamy
-------

Neseřazené
^^^^^^^^^^

Vytvoř neseřazený seznam::

   * ovoce
     * ananas
     * banán
     * citrón
   * zelenina

.. note::

   Místo ``*`` lze použít i ``+`` nebo ``-``.

.. tip::

   Je-li třeba deaktivovat označení seznamu, respektive jakékoliv jiné
   formátování textu, je nutné použít escapování::

      \* ovoce

Číslované
^^^^^^^^^

Vytvoř číslovaný seznam::

   1. jedna
   2. dva
   3. tři

Vytvoř kombinaci číslovaného a neseřazeného seznamu::

   1. jedna
      - a
      - b
      - c
   2. dva

.. note::

   Místo ``.`` lze použít i ``)``.

Odkazy
------

Vlož hypertextový odkaz::

   [Google](https://google.com)

.. tip::

   Je-li stejný odkaz použit vícekrát v dokumentu, lze z něj vytvořit
   referenci::

      [Google][google]

      [google]: https://google.com

Obrázky
-------

Vlož obrázek::

   ![Tux](https://upload.wikimedia.org/wikipedia/commons/a/af/Tux.png)

.. note::

   U obrázku lze taktéž použít referenci::

      ![Tux][tux]

      [tux]: https://upload.wikimedia.org/wikipedia/commons/a/af/Tux.png

Citace
------

Vlož citaci::

   > První citovaný odstavec.
   >
   > Druhý citovaný odstavec.

Dělící horizontální čára
------------------------

Odděl text dělící horizontální čarou::

   Text před dělící horizontální čarou.

   ---

   Text za dělící horizontální čarou.

.. note::

   Jako dělící čáru lze použít i ``***``.

Zdrojové kódy
-------------

Vlož zdrojový kód do textu::

   Stiskni klávesovou zkratku `levý ALT + F4`.

Vlož blok zdrojového kódu bez zvýraznění syntaxe::

   ```
   import this
   ```

Vlož blok zdrojového kódu se zvýrazněním syntaxe::

   ```py
   import this
   ```

.. note::

   Jakékoliv Markdown značky uvnitř zdrojého kódu budou nefunkční.

.. tip::

   Blok zdrojového kódu bez zvýraznění syntaxe lze vytvořit i pomocí odsazení::

      Zdrojový kód:

          import this
