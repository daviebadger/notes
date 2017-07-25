============
 PythonMode
============
----------------------------
 Podpora pro Python soubory
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

   Plug 'python-mode/python-mode'

Ovládání
========

Zabalení a rozbalení kódu
-------------------------

* ``za``

  * zabal / rozbal daný fold

* ``zo``

  * rozbal daný fold

* ``zO``

  * rozbal daný fold včetně všech vnořených foldů

* ``zR``

  * rozbal všechny foldy

* ``zc``

  * zabal daný fold

* ``zC``

  * zabal daný fold včetně všech vnořených foldů

* ``zM``

  * zabal všechny foldy

.. tip::

   Navigace mezi foldy:

   * ``zj``

     * skoč na další fold

   * ``zk``

     * skoč na předchozí fold

   * ``]z``

     * skoč na poslední řádek foldovaného textu

   * ``[z``

     * skoč na první řádek foldovaného textu

Pohybování v kódu
-----------------

* ``]]``

  * skoč na další třídu / funkci bez odsazení

* ``[[``

  * skoč na předchozí třídu / funkci bez odsazení

* ``]M``

  * skoč na další třídu / metodu / funkci v pořadí

* ``[M``

  * skoč na předchozí třídu / metodu / funkci v pořadí

Objekty pro označení / kopírování / přepísování / mazání:

* ``aC``

  * celá třída

* ``iC``

  * vnitřní obsah třídy

* ``aM``

  * celá metoda / funkce

* ``iM``

  * vnitřní obsah metody / funkce

Breakpointy pro debugování
--------------------------

* ``\b``

  * vlož / smaž breakpoint pro debugování::

       import ipdb; ipdb.set_trace()  # XXX BREAKPOINT

.. note::

   Defeaultní debugger je ``pdb``, není-li nainstalovaný jiný.

Konfigurace
===========

::

   " deaktivuj kontrolovače kódu (Syntastic preferován)

   let g:pymode_lint = 0

   " deaktivuj autodokončování kódu aj. (YouCompleteMe preferován)

   let g:pymode_rope = 0

   " deaktivuj automatickou aktivaci virtualenvu

   let g:pymode_virtualenv = 0
