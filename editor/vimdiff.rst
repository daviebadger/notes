=========
 Vimdiff
=========
----------------------------------------------
 Zobrazovač rozdílu v souborech v editoru Vim
----------------------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

Vimdiff je nainstalovaný spolu s editorem Vim.

Ovládání
========

Otevření diffu
--------------

Bez Gitu::

   $ vimdiff file_a.txt file_b.txt file_c.txt

S gitem po konfiguraci::

   $ git difftool
   $ git mergetool

Pomocí Fugitive pluginu::

   :Gdiff
   :Gsdiff
   :Gvdiff

Navigace mezi změnami
---------------------

* ``]c``

  * skoč na další rozdíl v souboru

* ``[c``

  * skoč na předchozí rozdíl v souboru

.. tip::

   ``]c`` a ``[c`` je možné přemapovat na ``]``, respektive ``[`` ve
   ``~/.vimrc``::

      map ] ]c
      map [ [c

Rozbalení a zabalení nezměneného textu
--------------------------------------

* ``zo``

  * rozbal zabalený text::

      +--10 lines: =====-------------------------

* ``zc``

  * zabal zpátky nezměnený text

Fixování merge konfliktu
------------------------

* ``:diffg[et]`` + buffer

  * nahraď lokální merge konflikt verzí z daného bufferu::

       " Mergetool

       :diffg L[OCAL]  " HEAD
       :diffg B[ASE]   " verze souboru před divergencí (rozdělení historie)
       :diffg R[EMOTE] " verze z dané větve

       " Fugitive

       :diffg //2 " HEAD
       :diffg //3 " verze z dané větve

.. note::

   Je třeba být v okně s mergnutým souborem (soubor se značkami ``<<<<<<<```,
   ``=======`` a ``>>>>>>>``).

.. tip::

   Pomocí ``:diffu[pdate]`` příkazu lze aktualizovat zbarvení diffů po
   odstranění lokálního konfliktu::

      :diffu
