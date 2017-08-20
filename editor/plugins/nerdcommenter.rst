===============
 NERDCommenter
===============
-----------------
 Komentovač kódu
-----------------

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

   Plug 'scrooloose/nerdcommenter'

Ovládání
========

* ``\c`` + mezera

  * zakomentuj / odkomentuj označené řádky

Konfigurace
===========

::

   " ignoruj odsazení při komentování

   let g:NERDDefaultAlign = 'left'

   let g:NERDCommentEmptyLines = 1

   " přidej mezeru za komentářem

   let g:NERDSpaceDelims = 1

   let g:NERDTrimTrailingWhitespace = 1

   " nepřidávej dvě mezery v Pythonu, jen jednu (bug)

   let g:NERDCustomDelimiters = {
       \ 'python': { 'left': '#' }}
