============
 PEP8Naming
============
---------------------------------------------------
 Kontrola pojmenování objektů podle PEP 8 konvencí
---------------------------------------------------

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

   $ pip install --user pep8-naming

.. note::

   ``flake8`` umí automaticky nadetekovat tento plugin, ačkoliv se nejmenuje
   např. ``flake8-pep8-naming``.

Ukázka
======

::

   $ cat file.py
   def badFunctionName():
       pass
   $ flake8 file.py
   file.py:1:5: N802 function name 'badFunctionName' should be lowercase xxx
