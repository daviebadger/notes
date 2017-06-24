===========
 Syntastic
===========
---------------------
 Kontrolovač syntaxe
---------------------

Instalace
=========

::

   Plug 'scrooloose/syntastic'

Systémové instalace jednotlivých kontrolovačů:

* HTML::

     $ sudo apt install tidy

* Markdown::

     $ gem install --user-install mdl

* Python::

     $ pip3 install --user flake8 pylint

* reStructuredText::

     $ pip3 install --user docutils


.. note::

   Je třeba přidat do ``PATH`` proměnné v terminálu následující lokace pro
   hledání spusitelných souborů::

      $HOME/.local/bin           # Python
      $HOME/.gem/ruby/2.3.0/bin  # Ruby

Ovládání
========

Vyhledávání kontrolovačů
------------------------

Zobraz seznam kontrolovačů pro všechny podporované soubory::

   :help syntastic-checkers

Zobraz seznam kontrolovačů jen pro daný typ souboru::

   :help syntastic-checkers-python

Ověřování kontrolovačů
----------------------

Zobraz informace ohledně kontrolovačů k aktuálnímu typu souboru::

   :SyntasticInfo
   Syntastic version: 3.8.0-59 (Vim 800, Linux, GUI)
   Info for filetype: python
   Global mode: active
   Filetype python is active
   Available checkers: flake8 pep8 pycodestyle pyflakes pylint python
   Currently enabled checker: flake8

Zobraz informace ohledně kontrolovačů ke konkrétnímu typu souboru::

   :SyntasticInfo python

Navigace v errorech
-------------------

* ``:lne``

  * skoč na další error

* ``:lp``

  * skoč na předchozí error

Konfigurace
===========

::

   " Show error in statusline if cursor is on the line with the error

   set statusline+=%#warningmsg#
   set statusline+=%{SyntasticStatuslineFlag()}
   set statusline+=%*

   " Automatically open and close quick window with errors

   let g:syntastic_always_populate_loc_list = 1
   let g:syntastic_auto_loc_list = 1

   " Check syntax errors when buffer opened and each time when write action
   " is called except for quit action

   let g:syntastic_check_on_open = 1
   let g:syntastic_check_on_wq = 0

   " Enable specific checkers

   let g:syntastic_html_checkers = ['tidy']
   let g:syntastic_markdown_checkers = ['mdl']
   let g:syntastic_python_checkers = ['flake8', 'pylint']
   let g:syntastic_rst_checkers = ['rst2pseudoxml']

.. note::

   Kontrolovače se spouštějí v daném pořadí za sebou, není-li nakonfigurávno
   jinak. Další se spustí jen v případě, pokud předešlý nenašel žádnou chybu.

.. tip::

   Je-li třeba spouštět kontrolovače s argumenty::

      let g:syntastic_python_flake8_args = '--max-line-length=99'
