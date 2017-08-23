========
 Python
========
------------------------------------------------
 Všeobecný skriptovací programovací jazyk (.py)
------------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

Python je defaultně nainstalovaný v Ubuntu::

   $ python3
   Python 3.6.2

.. note::

   Samotný příkaz ``python`` odkazuje na starší verzi::

      $ python --version
      Python 2.7.13

První program
=============

Python programy jdou spustit dvěma způsoby:

1. pomocí konzole / interaktivního shellu
2. pomocí souboru / skriptu

Interaktivní shell
------------------

Spusť interaktivní shell::

   $ python3
   Python 3.6.2 (default, Aug  4 2017, 14:35:04)
   [GCC 7.1.0] on linux
   Type "help", "copyright", "credits" or "license" for more information.
   >>>

Každý řádek v shellu za ``>>>`` je okamžitě exekutován po stisknutí klávesy
``ENTER``::

   >>> print("Hello world!")
   Hello world!
   >>>

Shell lze vypnout klávesovou zkratkou ``CTRL + D`` nebo zavoláním funkce
``quit`` (platí jen uvnitř shellu)::

   >>> quit()
   $

.. note::

   Při vypnutí shellu zanikne i historie použitých příkazů. Ta lze zobrazit v
   shellu postupně pomocí šipky nahoru.

.. tip::

   Jsou-li nainstalované i jiné verze Pythonu, lze je spustit s označením
   minor verze::

      $ python3.5
      Python 3.5.3+ (default, Jun  7 2017, 23:23:48)
      [GCC 6.3.0 20170519] on linux
      Type "help", "copyright", "credits" or "license" for more information.
      >>>

Skript
------

Spusť skript::

   $ cat hello.py
   print("Hello world!")
   $ python3 hello.py
   Hello world!

.. tip::

   Skript lze spustit i jako spustitelný soubor:

   1. přidat hlavičku (shebang) na začátek souboru::

         #!/usr/bin/env python3

         print("Hello world!")

   2. přidat oprávnění pro exekuci souboru::

         $ chmod +x hello.py

   3. spustit soubor::

         $ ./hello.py
         Hello world!

Základní syntaxe
================

Komentáře
---------

Vlož komentář, který bude Pythonem ignorován při exekuci kódu::

   $ cat hello.py
   # print("Hello")

   print("Hello world!")
   $ python3 hello.py
   Hello world!
   $

.. note::

   Komentáře se zpravidla používájí jen tam, kde je třeba vysvětlit úmysl,
   proč je právě použít daný kód, neboť ten nemusí být každému zřejmý při
   čtení kódu.

   V žádném případě by neměl zbytečně popisovat kód jak funguje, neboť se
   očekává, že ten kdo bude kód číst sám rozumí Pythonu.

.. tip::

   Délka řádku v souboru včetně komentářů by neměla překročit počet 79 znaků::

      # Strašně dlouhý ukázkový komentář,
      # který je pro ilustraci rozložen do tří řádků,
      # namísto jednoho dlouhého řádku překračující limit 79 znaků.
