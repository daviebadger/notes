========
 Commas
========
----------------------------------------------------------------
 Kontrola čárek u několika řádkových seznamů, n-tic či slovníků
----------------------------------------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user flake8-commas

Ukázka
======

::

   $ cat file.py
   a = [
       "a"
   ]
   $ flake8 file.py
   file.py:2:8: C812 missing trailing comma
