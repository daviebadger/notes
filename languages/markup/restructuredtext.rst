==================
 reStructuredText
==================
-------------------------------------------------------
 Značkový jazyk pro psání technické dokumentace (.rst)
-------------------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Základní značky
===============

Nadpisy
-------

Vlož nadpisy různé úrovně::

   ************
   První úroveň
   ************

   Druhá úroveň
   ============

   Třetí úroveň
   ------------

   Čtvrtá úroveň
   ^^^^^^^^^^^^^

   Pátá úroveň
   """""""""""

.. tip::

   Je-li třeba použít titulek a podtitulek, lze použít následující strukturu::

      =========
       Titulek
      =========
      ------------
       Podtitulek
      ------------

      Nadpis
      ======

Odstavce
--------

Vlož odstavce::

   První odstavec.

   Druhý odstavec.

.. tip::

   Je-li třeba zalomit text, použije se na začátku řádku ``|``::

      | První řádek
      | Druhý řádek
      | Třetí řádek

Zvýraznění textu
----------------

Označ text kurzívou::

   *Text kurzívou.*

Označ text tučným písmem::

   **Text tučným písmem.**

.. note::

   Kurzívu a tučné písme nejde dohromady kombinovat.

.. tip::

   Označ text horním indexem::

      Horní :sup:`index`.

   Označ text dolním indexem::

      Dolní :sub:`index`.

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

   Místo ``.`` lze použít i ``)`` a místo čísel písmena nebo římské číslice.

.. tip::

   Pomocí ``#`` lze automaticky číslovat položky v seznamu::

      #. jedna
      #. dva
      #. tři

Odkazy
------

Vlož hypertextový odkaz::

   https:://google.com

Vlož hypertextový odkaz s popiskem::

   `Google <https://google.com`_

.. note::

   Odkaz může taky vést na nějaký nadpis v dokumentu::

      `Název nadpisu`_

.. tip::

   Je-li stejný odkaz použit vícekrát v dokumentu, lze z něj vytvořit
   referenci::

      Google_
      `Linux logo`_

      .. _Google: https://google.com
      .. _Linux logo: https://upload.wikimedia.org/wikipedia/commons/a/af/Tux.png

Obrázky
-------

Vlož obrázek bez viditelného popisku::

   .. image:: https://upload.wikimedia.org/wikipedia/commons/a/af/Tux.png

Vlož obrázek s viditelným popiskem::

   .. figure:: https://upload.wikimedia.org/wikipedia/commons/a/af/Tux.png

      Tux

.. tip::

   Obrázky lze dále konfigurovat::

      .. image:: https://upload.wikimedia.org/wikipedia/commons/a/af/Tux.png
         :align: center
         :alt: Tux
         :height: 100
         :width: 100

Citace
------

Vlož citaci::

   Citovaný text:

      První citovaný odstavec.

      Druhý citovaný odstavec.

Dělící horizontální čara
------------------------

Odděl text dělící horizontální čarou::

   Text před dělící horizontální čarou.

   ----

   Text za dělící horizontální čarou.

Zdrojové kódy
-------------

Vlož zdrojový kód do textu::

   Stiskni klávesovou zkratku ``levý ALT + F4``

Vlož blok zdrojového kódu bez zvýraznění syntaxe::

   ::

      import this

   Zdrojový kód::

      import this

Vlož blok zdrojového kódu se zvýrazněním syntaxe::

   .. code:: python

      import this

Vlož blok zdrojového kódu se zvýrazněním syntaxe a číslováním řádků::

   .. code:: python
      :number-lines: 1

      import this

.. note::

   Jakékoliv reStructuredText značky uvnitř zdrojového kódu budou nefunkční.

.. tip::

   Zdrojový kód v Python lze zapsat i za pomocí interpreteru::

      >>> import this

Tabulky
-------

Vytvoř tabulku bez sloučených buněk::

   =========  =========
   Sloupec A  Sloupec B
   =========  =========
   A1         B1
   A2         B2
   A3         B3
   =========  =========

Vytvoř tabulku se slučenými buňkami::

   +-----------+-----------+-----------+
   | Sloupec A | Sloupec B | Sloupec C |
   +===========+===========+===========+
   | A1        | B1        | C1        |
   +-----------+-----------+-----------+
   | A2 + B2               | C2 + C3   |
   +-----------+-----------+           |
   | A3        | B3        |           |
   +-----------+-----------+-----------+

Slovník pojmů
-------------

Vytvoř slovník pojmů::

   HTTP
      Internetový protokol pro výměnu HTML souborů.

   Python
      Skriptovací programovací jazyk.

.. tip::

   Jednotlivé pojmy lze i škatulkovat do kategorií::

      Jablko : ovoce
         Plod z jabloně.

Poznámky pod čarou
------------------

Vytvoř poznámku pod čarou::

   Python [1]_ je programovací jazyk.

   ----

   .. [1] Python (programming language)
      Wikipedia: the free encyclopedia. [online].
      2001- [cit. 2017-06-18].
      Dostupné z: https://en.wikipedia.org/wiki/Python_(programming_language)

.. tip::

   Automatické číslovní poznámek pod čarou::

      Python [#]_ je programovací jazyk.

      ----

      .. [#] Python (programming language)

Pokročilé značky
================

Komentáře
---------

Vlož komentář::

   .. Komentovaný text.

Metadata
--------

Vlož metadata k dokumentu::

   =========
    Titulek
   =========
   ------------
    Podtitulek
   ------------

   :Autor: Daviebadger
   :Kontakt: davie.badger@gmail.com
   :Datum vydání: 18.6.2017

.. note::

   U metadat lze buď použít vlastní klíče nebo již předdefinované:

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

.. tip::

   K metadatům lze přiřadit i abstrakt dokumentu::

      :Abstract:

         Abstrakt dokumentu.

Obsah dokumentu
---------------

Vygeneruj obsah dokumentu::

   .. contents:: Obsah:

.. note::

   Defaultně budou zahrnuty všechny úrovně nadpisů v obsahu, není-li
   uvedeno jinak::

      .. contents:: Obsah:
         :depth: 3

.. tip::

   Nadpisy lze očíslovat, a případně jim ještě nastavit suffix::

      .. sectnum::
         :suffix: .

Text se speciálním významem
---------------------------

Vlož varování do textu::

   .. warning::

      Pozor!

.. note::

   Seznam zabudovaných direktiv pro text se speciálním významem:

   * attention
   * caution
   * danger
   * error
   * hint
   * important
   * note
   * tip
   * warning

Načtení obsahu jiného souboru
-----------------------------

Vlož do dokumentu obsah jiného souboru::

   .. include:: ../CHANGELOG.rst
