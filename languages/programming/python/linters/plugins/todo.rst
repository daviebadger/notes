======
 TODO
======
-------------------------
 Kontrola TODO komentářů
-------------------------

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

   $ pip install --user flake8-todo

Ukázka
======

::

   $ cat file.py
   VERBOSE = 0  # TODO(Davie): Change to namedtuple
   $ flake8 file.py
   file.py:1:16: T000 Todo note found.
