========
 Quotes
========
------------------------
 Kontrola typů uvozovek
------------------------

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

   $ pip install --user flake8-quotes

Ukázka
======

::

   $ cat file.py
   "test"


   def function():
       '''
       Doc
       '''
   $ flake8 file.py
   file.py:1:1: Q000 Remove bad quotes.
   file.py:5:5: Q001 Remove bad quotes from multiline string.
   $ flake8 --inline-quotes '"' --multiline-quotes "'" file.py
   $

.. note::

   Plugin defaultně podporuje jednoduché uvozovky pro stringy a dvojité pro
   docstringy, není-li nakonfigurováno jinak::

      [flake8]
      inline-quotes = "
