=====
 Riv
=====
--------------------------------------
 Podpora pro reStructuredText soubory
--------------------------------------

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

   Plug 'Rykka/riv.vim'

Ovládání
========

Tvorba nadpisů
--------------

* ``<C-E>s1`` až ``<C-E>s6``

  * vytvoř nadpis z aktuálního řádku

.. tip::

   Pomocí ``<C-E>hs`` lze zobrazit v novém okně přehled nadpisů a případně na
   nějaký konkrétní skočit pomocí ``ENTER``.

Tvorba tabulek
--------------

* ``<C-E>tc``

  * vytvoř grid tabulku s daným počtem řádků a sloupců

.. note::

   Grid tabulka se bude sama natahovat do šírky a výšky, je-li to třeba.

.. tip::

   Pomocí ``+-+<Enter>`` lze vytvořit manuálně grid tabulku nebo také přidat
   nový řádek. Nový sloupec lze přídat pomocí ``|`` na řádku.

Konfigurace
===========

::

   " klasické Vimovské odsazení

   let g:riv_disable_indent = 1

   " informace o foldech v levé časti

   let g:riv_fold_info_pos = 'left'

   " foldování jen pro sekce (nadpisy)

   let g:riv_fold_level = 1

   " vlastní značení nadpísů H1 - H6

   let g:riv_section_levels = '*=-^"'''
