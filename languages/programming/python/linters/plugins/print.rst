=======
 Print
=======
---------------------------
 Kontrola printů a pprintů
---------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user flake8-print

Ukázka
======

::

   $ cat file.py
   print("Hello World!")
   $ flake8 file.py
   $ flake8 --enable-extensions=T file.py
   file.py:3:1: T001 print found.
   file.py:4:1: T003 pprint found.

.. note::

   Plugin je defaultně vypnutý.
