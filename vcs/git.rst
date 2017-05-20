=====
 Git
=====
------------------------------
 Systém pro správu verzí kódu
------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

Příkazem::

   $ sudo apt install git

Základní ovládání
=================

Nastavení
---------

.. note::

   Nezbytné pro běh Gitu.

config
^^^^^^

Zobraz nebo nastav nastavení Gitu.

config --global
"""""""""""""""

Nastav globálně identitu uživatele (povinné)::

   $ git config --global user.name "Davie Badger"
   $ git config --global user.email "davie.badger@gmail.com"

Nastav globálně editor pro práci s Gitem (nepovinné)::

   $ git config --global code.editor vim

.. note::

   Bez použítí volby ``--global`` bude nastavení platné jenom v daném
   repozitáři.

config --list
"""""""""""""

Zobraz veškerá nastavení Gitu::

   $ git config --list
   user.name=Davie Badger
   user.email=davie.badger@gmail.com
   core.editor=vim

Globální nastavení se ukládá do souboru ``~/.gitignore`` a lokální v repozitáři
v ``.git/config``.

.. tip::

   Zobraz jen konkrétní nastavení::

   $ git config user.name
   Davie Badger
