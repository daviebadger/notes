==========
 Debugger
==========
--------------------
 Kontrola debuggerů
--------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user flake8-debugger

Ukázka
======

::

   $ cat file.py
   import ipdb; ipdb.set_trace()
   $ flake8 file.py
   file.py:1:1: T002 import for ipdb found
   file.py:1:12: E702 multiple statements on one line (semicolon)
   file.py:1:14: T002 trace found: ipdb.set_trace used
