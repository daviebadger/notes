===========
 AutoPairs
===========
-----------------------------------------
 Automatické zavirání závorek a uvozovek
-----------------------------------------

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

   Plug 'jiangmiao/auto-pairs', {'commit': '3bd07a4'}

.. note::

   Commit ``3bd07a4`` nerozbije chování klávesnice, např. při znaku ``ý``.

Konfigurace
===========

::

   let g:AutoPairsShortcutToggle = '<F4>'  " zapni / vypni autozavírání
