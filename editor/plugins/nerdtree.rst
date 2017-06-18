==========
 NERDTree
==========
--------------------------------
 Zobrazení adresářové struktury
--------------------------------

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

.. note::

   Pokud mimo Vim vznikne v dané adresářové struktuře nový objekt, tak se tato
   změna neprojeví v NERDTree stromu, dokud to není manuálně vyžádáno

* ``r``

  * aktualizuj obsah daného adresáře

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

   " open NERDTree if no file specified

   autocmd StdinReadPre * let s:std_in=1
   autocmd VimEnter * if argc() == 0 && !exists("s:std_in") | NERDTree | endif

   " open NERDTree if directory specified

   autocmd StdinReadPre * let s:std_in=1
   autocmd VimEnter * if argc() == 1 && isdirectory(argv()[0]) && !exists("s:std_in") | exe 'NERDTree' argv()[0] | wincmd p | ene |

   " close Vim if last open window would be NERDTree

   autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif
