=======
 CtrlP
=======
----------------------------
 Rychlé vyhledávání souborů
----------------------------

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

   Plug 'ctrlpvim/ctrlp.vim'

Ovládání
========

Otevření a zavření okna
-----------------------

* ``CTRL + p``

  * otevři ``CtrlP`` okno a respektuj aktuální adresář, respektive projekt
    ve verzovacím systému (Git)

* ``:CtrlP`` + adresář

  * otevři ``CtrlP`` okno a vyhledávej soubory od daného adresáře

* ``ESC``

  * zavři ``CtrlP`` okno

.. note::

   Defaultně se otevře ``CtrlP`` okno pro vyhledávání souborů.

Práce s oknem
-------------

Přepínání mezi módy
^^^^^^^^^^^^^^^^^^^

* ``CTRL + f``

  * přepni dopředu mezi ``CtrlP`` módy (soubory, buffery, posledně použité
    souboru)

* ``CTRL + b``

  * přepní dozadu mezi ``CtrlP`` módy

Způsob vyhledávání souborů
^^^^^^^^^^^^^^^^^^^^^^^^^^

Defaultně se hledá celá cesta včetně adresářů.

* ``CTRL + d``

  * hledej jen soubory

* ``CTRL + r``

  * hledej podle regexu

.. note::

   Pokud došlo ke změně obsahu adresáře / projektu, je třeba aktualizovat
   keš v ``CtrlP`` pomocí ``F5``.

.. tip::

   Pomocí ``CTRL + p``, respektive ``CTRL + n`` lze zobrazit historii
   hledaných souborů.

Navigace mezi najitými soubory
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``CTRL + k`` nebo šipka nahoru

  * označ soubor o řádek výš

* ``CTRL + j`` nebo šipka dolů

  * označ soubor o řádek níž

.. note::

   Soubory jsou seřazeny vzestupně podle nejlepší shody.

Otevření najitých souborů
^^^^^^^^^^^^^^^^^^^^^^^^^

* ``ENTER``

  * otevři soubor jako nový buffer

* ``CTRL + x``

  * otevři soubor v novém horizontálním okně

* ``CTRL + v``

  * otevři soubor v novém vertikálním okně

* ``CTRL + t``

  * otevři soubor na nové záložce

.. tip::

   Pomocí ``CTRL + z`` lze označit více souborů, které lze pak najednou
   otevřít.

Konfigurace
===========

::

   " Ignoruj soubory vyjmenované v .gitignore

   let g:ctrlp_user_command = ['.git', 'cd %s && git ls-files -co --exclude-standard']

.. note::

   ``CtrlP`` respektuje ignorované patterny v ``wildignore``.
