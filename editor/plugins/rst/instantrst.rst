============
 InstantRst
============
----------------------------------------------
 Instantní zobrazení RST souborů v prohlížeči
----------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   Plug 'Rykka/instantrst'

.. note::

   Je třeba ještě nainstalovat samotný InstantRst balíček::

      pip install --user https://github.com/Rykka/instant-rst.py/archive/master.zip

Ovládání
========

* ``InstantRst``

  * zobraz v prohlížečí aktuální buffer

* ``StopInstantRst[!]``

  * přestaň zobrazovat v prohlížeči aktuální buffer, respektive všechny RST
    buffery, je-li použit vykričník

.. note::

   Při přepnutí na jiný RST buffer se zobrazí v prohlížečí přepnutý RST soubor.
