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
   file.py:1:1: T001 print found.

.. note::

   Plugin bude vypnutý, pokud při použití ``flake8`` je použita volba
   ``--select`` na konkrétní chybové hlášky, proto je třeba jej zapnout
   pomocí volby ``--enable-extensions=T``::

      $ flake8 --select E,F,W --enable-extensions=T file.py
      file.py:1:1: T001 print found.
