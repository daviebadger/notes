============
 ImportOrder
============
-------------------------
 Kontrola pořadí importů
-------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user flake8-import-order

Ukázka
======

::

   $ cat file.py
   import flake8
   import sys
   $ flake8 file.py
   file.py:2:1: I100 Import statements are in the wrong order. import sys should be before import flake8
   file.py:2:1: I201 Missing newline before sections or imports.

.. note::

   Defaultní ``import-order-style`` je nastaven na ``cryptography``::

      import os
      import sys
      from functools import path

      import X
      from X import A
      from X import B, C

      import Y
      from Y import A
      from Y import B, C

      import Z
      from Z import A
      from Z import B, C

      import local
      from local import *

   Ostatní style lze nalézt `ZDE <https://github.com/PyCQA/flake8-import-order#styles>`_.
