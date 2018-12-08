============
 SortedKeys
============
----------------------------------------------------------------
 Kontrola abecedního pořádí klíčů u několika řádkového slovníku
----------------------------------------------------------------

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

   $ pip install --user flake8-sorted-keys

Ukázka
======

::

   $ cat file.py
   d = {
       "c": 0,
       "b": 1,
       "a": 2,
   }
   $ flake8 file.py
   file.py:3:5: S001 Sort keys. 'b' should be before 'c'.
