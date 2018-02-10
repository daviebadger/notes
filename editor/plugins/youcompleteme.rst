===============
 YouCompleteMe
===============
-----------------------------------------------------
 Autodokončovač slov a zobrazovač dokumentace / kódu
-----------------------------------------------------

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

   Plug 'valloric/youcompleteme', {'do': 'sudo python3 install.py'}

.. note::

   Pro úspěšně nainstalování plugin je třeba nainstalovat ještě systémové
   balíčky ``build-essential`` a ``cmake``.

Konfigurace
===========

::

   " zobraz okno s použitím objektu a pak ho automaticky zavři

   let g:ycm_autoclose_preview_window_after_insertion = 1

   " aktivuj YCM jen pro Python

   let g:ycm_filetype_whitelist = {'python': 1}

   " zobraz zdrojové kódy objektu v horizontálním okně

   let g:ycm_goto_buffer_command = 'horizontal-split'

   let g:ycm_python_binary_path = 'python3'

   " klávesová zkratka pro zobrazení dokumentace objektu

   nnoremap <leader>d :YcmCompleter GetDoc<CR>

   " klávesová zkratka pro zobrazení zdrojového kódu objektu

   nnoremap <leader>g :YcmCompleter GoToDefinitionElseDeclaration<CR>

   " klávesová zkratka pro zobrazení všech souborů, kde je objekt použit (.py + .js)

   nnoremap <leader>n :YcmCompleter GoToReferences<CR>
