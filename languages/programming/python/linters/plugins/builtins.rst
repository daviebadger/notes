==========
 Builtins
==========
------------------------------------------
 Kontrola přepisování zabudovaných funkcí
------------------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user flake8-builtins

Ukázka
======

::

   $ cat file.py
   def function(object):
       max = 1
   $ flake8 file.py
   file.py:1:14: A002 "object" is used as an argument and thus shadows a python builtin, consider renaming the argument
   file.py:2:5: F841 local variable 'max' is assigned to but never used
   file.py:2:5: A001 "max" is a python builtin and is being shadowed, consider renaming the variable
