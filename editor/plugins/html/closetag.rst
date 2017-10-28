==========
 CloseTag
==========
------------------------------------
 Automatické zavírání párových tagů
------------------------------------

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

   Plug 'alvan/vim-closetag'

Ovládání
========

Defaultně se tag uzavře, existuje-li v páru.

.. tip::

   Pomocí dalšího ``>`` na konci tagu lze odsadit uzavírající tag ob další
   řáděk a kurzor vložit dovnitř tagu::

      <p>|<p/>

      <p>
        |
      </p>
