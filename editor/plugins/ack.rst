=====
 Ack
=====
----------------------------------------
 Rychlé vyhledání patternů v souborech
----------------------------------------

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

   Plug 'mileszs/ack.vim'

.. note::

   Ačkoliv plugin očekává systémový příkaz ``ack`` z balíčku ``ack-grep``,
   tak jej lze překonfigurovat na ``ag`` z ``silversearcher-ag``, neboť
   původní ``ack`` již není podporován v Ubuntu od verze 17.10::

      $ sudo apt install silversearcher-ag

Ovládání
========

Vyhledávání
-----------

Práce s oknem
-------------

* ``o``

  * otevři daný soubor na daném řádku

* ``O``

  * otevři daný soubor na daném řádku a zavři ``ack`` okno

* ``go``

  * otevři daný soubor na daném řádku a ponech kurzor aktivní v ``ack`` okně

* ``t``

  * otevři daný soubor na daném řádku v nové záložce

* ``T``

  * otevři daný soubor na daném řádku v nové záložce bez přesunutí na danou
    záložku

* ``h``

  * otevři daný soubor v horizontálním okně

* ``H``

  * otevři daný soubor v horizontálním okně a kurzor ponech aktivní v ``ack``
    okně

* ``v``

  * otevři daný soubor ve vertikálním okně

* ``gv``

  * otevři daný soubor v vertikálním okně a kurzor ponech aktivní v ``ack``
    okně

* ``q``

  * zavři ``ack`` okno

.. note::

   Po otevření souborů se chybně zvětšuje ``ack`` okno, které lze změnšit
   příkazem ``:res 5`` na 5 řádků do výšky.

Konfigurace
===========

::

   if executable('ag')
     let g:ackprg = 'ag --vimgrep'
   endif

   " neskakej hned na první vyhledaný soubor

   cnoreabbrev Ack Ack!
   nnoremap <Leader>a :Ack!<Space>

   " rozděl okno jako nastavení splitbelow a splitright

   let g:ack_mappings = {
       \ "h": "<C-W><CR>:exe 'wincmd ' (&splitbelow ? 'J' : 'K')<CR><C-W>p<C-W>J<C-W>p",
       \ "H": "<C-W><CR>:exe 'wincmd ' (&splitbelow ? 'J' : 'K')<CR><C-W>p<C-W>J",
       \ "v": "<C-W><CR>:exe 'wincmd ' (&splitright ? 'L' : 'H')<CR><C-W>p<C-W>J<C-W>p",
       \ "gv": "<C-W><CR>:exe 'wincmd ' (&splitright ? 'L' : 'H')<CR><C-W>p<C-W>J" }
