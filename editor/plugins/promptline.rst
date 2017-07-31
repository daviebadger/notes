============
 Promptline
============
---------------------------------------------
 Generátor Airline lišty pro shellový prompt
---------------------------------------------

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

   Plug 'edkolev/promptline.vim'

Konfigurace
===========

::

   " Zobraz prompt ve tvaru:
   "
   " jméno uživatele > cesta do adresáře > git větev > Python virtualenv $

   let g:promptline_preset = {
       \'a' : [ promptline#slices#user() ],
       \'b' : [ '\w' ],
       \'c' : [ promptline#slices#vcs_branch() ],
       \'y' : [ promptline#slices#python_virtualenv() ]}

.. note::

   Poté je třeba ještě vykonat následující příkazy pro změnu PS1 promptu
   v Bashi:

   1. načíst opětovně konfigurační soubor pro Vim::

         so ~/.vimrc

   2. vygenerovat shellový skript z Vimu::

         :PromptlineSnapshot ~/.shell_prompt.sh airline

   3. přidat následující řádek do ``~/.bashrc``::

         source ~/.shell_prompt.sh
