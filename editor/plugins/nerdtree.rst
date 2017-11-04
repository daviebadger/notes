==========
 NERDTree
==========
--------------------------------
 Zobrazení adresářové struktury
--------------------------------

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

   Plug 'scrooloose/nerdtree'

Ovládání
========

Defaultně není NERDTree strom zobrazen, proto je třeba ho spustit příkazem::

   :NERDTree

Navigace
--------

* ``P``

  * skoč na roota adresářové struktury

* ``p``

  * skoč na název adresáře, respektive na nadřazený adresář

* ``J``

  * skoč na poslední objekt v daném adresáři

* ``K``

  * skoč na první objekt v daném adresáři

* ``CTRL + j``

  * skoč na další soubor, respektive adresář

* ``CTRL + k``

  * skoč na předchozí soubor, respektive adresář

Práce s adresáři
----------------

Rozbalení a zabalování adresářů
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``o``

  * rozbal nebo zabal daný adresář

* ``O``

  * rozbal daný adresář včetně všech jeho vnořených adresářů

* ``x``

  * zabal adresář, aniž bych musel být s kurzorem na místě adresáře

* ``X``

  * zabal daný adresář včetně všech jeho vnořených adresářů

Vstupování a vystupování z adresářů
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``C``

  * vstup do daného adresáře, jako by se jednalo o ``cd`` příkaz (může nastat
    menší prodleva)

* ``u``

  * vstup do nadřazeného adresáře, jako by se jednalo o ``cd ..`` příkaz

* ``U``

  * vstup do nadřazeného adresáře, ale ponechej otevřené adresáře, jestli
    nějaké jsou

Editace adresářů
^^^^^^^^^^^^^^^^

* ``m``

  * zobraz menu akcí pro editaci adresáře (vytvoření, přejmenování, mazání)

.. note::

   U vytváření nových adresářů nebo jejich přejmenování je třeba použít na
   konci názvu ``/``, aby se jednalo o adresář a ne soubor.

Aktualizace obsahu adresářů
^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``r``

  * aktualizuj obsah daného adresáře, došlo-li ke změně jeho obsahu

* ``R``

  * aktualizuj obsah root adresáře včetně jeho vnořených adresářů

Práce se soubory
----------------

Otevírání souborů
^^^^^^^^^^^^^^^^^

* ``o``

  * otevři soubor v prvním možném okně

* ``s``

  * otevři soubor v novém vertikálním okně

* ``i``

  * otevři soubor v novém horizontálním okně

* ``t``

  * otevři soubor na nové záložce a ihned se na ni přepni

* ``T``

  * otevři soubor na nové záložce, ale nepřepínej se na ni

Editace souborů
^^^^^^^^^^^^^^^

* ``m``

  * zobraz menu akcí pro editaci souborů (vytvoření, přejmenování, mazání)

Konfigurace
===========

::

   " nezobrazuj některé soubory a adresáře definované přes wildignore

   let NERDTreeRespectWildIgnore = 1

   set wildignore+=build
   set wildignore+=dist
   set wildignore+=egg-info
   set wildignore+=__pycache__
   set wildignore+=.git
   set wildignore+=.mypy_cache

   " zobraz skryté soubory a adresáře

   let NERDTreeShowHidden = 1

   " otevři NERDTree, pokud argument pro Vim je adresář

   autocmd StdinReadPre * let s:std_in=1
   autocmd VimEnter * if argc() == 1 && isdirectory(argv()[0]) && !exists("s:std_in") | exe 'NERDTree' argv()[0] | wincmd p | ene | endif
