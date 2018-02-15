======
 Make
======
------------------------------------------------------
 CLI aplikace pro usnadnění volání příkazů v projektu
------------------------------------------------------

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

   $ sudo apt install make

.. note::

   Místo balíčku ``make`` lze rovnou nainstalovat balíček ``build-essential``,
   ve kterém jsou zahrnuté nezbytné balíčky pro kompilací programů v C/C++,
   jehož součástí je i balíček ``make``.

Konfigurační soubor
===================

Příkazy se konfigurují v souboru ``Makefile``.

.. note::

   Pro odsazení se používájí klasické tabulátory, jinak nebude příkaz ``make``
   správně fungovat::

      $ cat Makefile
      test:
          echo "test"
      $ make test
      Makefile:2: *** missing separator.  Stop.

Příkazy
-------

Vytvoř příkaz, který volá jiný příkaz::

   $ cat Makefile
   # subcommand test

   test:
           echo "test"
   $ make test
   echo "test"
   test

Vytvoř příkaz, který volá jiné příkazy za sebou tak, dokud je předchozí příkaz
úspěšný::

   $ cat Makefile
   right:
           echo "a"
           echo "b"
           echo "c"

   wrong:
           echo "a"
           echoecho "b"
           echo "c"
   $ make right
   echo "a"
   a
   echo "b"
   b
   echo "c"
   c
   $ make wrong
   echo "a"
   a
   echoecho "b"
   /bin/sh: 1: echoecho: not found
   Makefile:7: recipe for target 'wrong' failed
   make: *** [wrong] Error 127

Vytvoř příkaz, který volá jiné příkazy za sebou tak, že nezáleží na špatném
exitovém kódu předchozího příkazu::

   $ cat Makefile
   wrong:
           echo "a"
           - echoecho "b"
           echo "c"
   $ make wrong
   echo "a"
   a
   echoecho "b"
   /bin/sh: 1: echoecho: not found
   Makefile:7: recipe for target 'wrong' failed
   make: [wrong] Error 127 (ignored)
   echo "c"
   c

Vytvoř příkaz, který závísí na jiných příkazech nebo souborech v projektu, než
se pustí samotný příkaz::

   $ cat Makefile
   test: test-one test-two test-three
           echo "test"
   test-one:
           echo "test-one"
   test-two:
           echo "test-two"
   test-three:
           echo "test-three"
   $ make test
   echo "test-one"
   test-one
   echo "test-two"
   test-two
   echo "test-three"
   test-three
   echo "test"
   test

Vytvoř příkaz, který spustí příkazy s potlačením standardního výstupu::

   $ cat Makefile
   delete:
           rm -f foo.bar
   remove:
           @ rm -f foo.bar
   $ make delete
   rm -f foo.bar
   $ make remove
   $

Vytvoř příkaz, který zavolá příkaz z jiného ``Makefile`` souboru::

   $ ls
   docs  Makefile
   $ ls docs
   Makefile
   $ cat Makefile
   test:
           $(MAKE) -C docs html
   $ cat docs/Makefile
   html:
           echo "html"
   $ make test
   make -C docs html
   make[1]: Entering directory '/home/davie/test/docs'
   echo "html"
   html
   make[1]: Leaving directory '/home/davie/test/docs'

.. note::

   Jestliže se závolá příkaz ``make`` bez uvedení příkazu z ``Makefile``
   souboru, tak se defaultně spustí první uvedený příkaz v ``Makefile``::

      $ cat Makefile
      a:
              @echo "a"
      b:
              @echo "b"
      $ make
      a
      $ make a
      a
      $ make b
      b

   Zpravidla jako výchozí příkaz se používá příkaz ``all``, který spustí
   komplexní sadu příkazů, a který se ještě nastaví jako výchozí příkaz::

      $ cat Makefile
      .DEFAULT_GOAL := all

      all:
              @echo "install"
              @echo "test"
              @echo "build"
              @echo "deploy"
      $ make
      install
      test
      build
      deploy

.. tip::

   Pokud se některý příkaz jmenuje stejně jako název souboru v projektu, tak se
   daný příkaz nespustí, dokud není explicitně uvedeno, že se stejnojmenný
   soubor má ignorovat::

      $ cat Makefile
      test:
              @echo "test"
      $ touch test
      $ make test
      make: 'test' is up to date.
      $ echo -e ".PHONY: test\n$(cat Makefile)" > Makefile
      $ cat Makefile
      .PHONY: test
      test:
              @echo "test"
      $ make test
      test

   Zpravidla se ``.PHONY`` vyskytuje před každým příkazem::

      $ cat Makefile
      .PHONE: doc
      doc:
              @echo "doc"

      .PHONE: test
      test:
              @echo "test"
