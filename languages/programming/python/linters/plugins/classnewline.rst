==============
 ClassNewline
==============
--------------------------------------------------------------
 Kontrola prázdného řádku mezi definicí třídy a první metodou
--------------------------------------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user flake8-class-newline

Ukázka
======

::

   $ cat file.py
   class A(object):
       def __init__(self):
           pass


   class B(object):
       b = 0

       def __init__(self):
           pass


   class C(object):
       @property
       def c(self):
           pass
   $ flake8 file.py
   file.py:2:1: CNL100 Class definition does not have a new line.
   file.py:14:1: CNL100 Class definition does not have a new line.
