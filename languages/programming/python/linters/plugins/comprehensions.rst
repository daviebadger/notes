================
 Comprehensions
================
----------------------------------------------------
 Kontrola komprehencí u seznamů, množin či slovníků
----------------------------------------------------

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

   $ pip install --user flake8-comprehensions

Ukázka
======

::

   $ cat file.py
   max([number for number in range(10)])
   $ flake8 file.py
   file.py:1:1: C407 Unnecessary list comprehension - 'max' can take a generator.
