========
 Tagbar
========
------------------------------
 Zobrazovač struktury souboru
------------------------------

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

   Plug 'majutsushi/tagbar'

.. note::

   Pro běh Tagbaru je třeba doinstalovat balíček `exuberant-ctags`::

      sudo apt install exuberant-ctags

Ovládání
========

Zobrazení okna
--------------

* ``:TagbarToggle``

  * otevři nebo zavři Tagbar okno

Ovládání okna
-------------

* ``o``

  * otevři nebo zavři fold

* ``s``

  * seřaď nebo neseřaď tagy v okně

* ``v``

  * zobraz nebo schovej skryté tagy

* ``p``

  * zobraz daný tag v souboru, avšak zůstaň s kurzorem v oknu

* ``ENTER``

  * skoč s kurzorem na daný tag v souboru

.. note::

   V oknu lze použít standardní klávesy pro ovládání foldů, ke kterým lze
   navíc přidat:

   * ``zj``

     * skoč na další fold

   * ``zk``

     * skoč na předchozí fold

   * ``CTRL + n``

     * skoč na další nadřazený fold

   * ``CTRL + p``

     * skoč na předchozí nadřazený fold

Konfigurace
===========

::

   nnoremap <F2> :TagbarToggle<CR>

.. note::

   Tagbar nepodporuje zdaleka všechny jazyky. Podporu pro ostatní jazyky lze
   nalézt `ZDE <https://github.com/majutsushi/tagbar/wiki>`_.
