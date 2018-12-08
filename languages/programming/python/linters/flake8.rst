========
 Flake8
========
-------------------------------------------------------
 Agregátor kontrolovačů pycodestyle, pyflakes a mccabe
-------------------------------------------------------

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

   $ pip install --user flake8

Ovládání
========

flake8
------

Zkontroluj dodržování standardů kódu v souboru::

   $ cat test.py
   print ( "Hello World!" )
   $ flake8 test.py
   test.py:1:6: E211 whitespace before '('
   test.py:1:8: E201 whitespace after '('
   test.py:1:23: E202 whitespace before ')'

Zkontroluj kódy v adresáři::

   $ ls
   test test.py
   $ flake8
   ./test.py:1:6: E211 whitespace before '('
   ./test.py:1:8: E201 whitespace after '('
   ./test.py:1:23: E202 whitespace before ')'
   ./test/b.py:4:1: E302 expected 2 blank lines, found 1
   ./test/b.py:7:1: E302 expected 2 blank lines, found 1
   ./test/c.py:1:4: E999 SyntaxError: invalid syntax
   ./test/a.py:1:1: F401 'this' imported but unused
   $ flake8 test
   test/b.py:4:1: E302 expected 2 blank lines, found 1
   test/b.py:7:1: E302 expected 2 blank lines, found 1
   test/c.py:1:4: E999 SyntaxError: invalid syntax
   test/a.py:1:1: F401 'this' imported but unused

.. note::

   Pokud jsou vypsány chybové hlášky, exitový kód příkazu je ``1``::

      $ echo $?
      1

   Naopak, nedošlo-li k porušení standardů, exitový kód je ``0``::

      $ touch file.py
      $ flake8 file.py
      $ echo $?
      0

.. tip::

   ``flake8`` lze použít jako pre-commit hook v gitu, který zabrání vytvoření
   commitu, pokud se objeví chybová hláška::

      $ flake8 --install-hook git
      $ git config --bool flake8.strict true
      $ git config --bool flake8.lazy true
      $ git commit
      ./test.py:1:6: E211 whitespace before '('
      $

Odbočka k chybovým hláškám
^^^^^^^^^^^^^^^^^^^^^^^^^^

Každý kontrolovač má své vlastní chybové hlášky:

* `pycodestyle <https://pycodestyle.readthedocs.io/en/latest/intro.html#error-codes>`_

  * ``E`` jako errory a ``W`` jako warningy
  * kontrola stylistiky kódu, např. odsazení či prázdné řádky

* `pyflakes <http://flake8.pycqa.org/en/latest/user/error-codes.html#error-violation-codes>`_

  * ``F`` jako errory
  * kontrola nestylistické části kódu, např. nepoužité importy nebo proměnné

.. note::

   ``mccabe`` má jen jednou hlášku a to ``C901`` pro komplexní kód. Tento
   kontrolovač není defaultně zapnutý, dokud se nespecifikuje maximální
   komplexnost kódu, zpravidla číslo ``10``::

      $ flake8 --max-complexity=10

flake8 --show-source
^^^^^^^^^^^^^^^^^^^^

Zobraz chybové hlášky včetně zobrazení řádku, na kterém došlo k porušení::

   $ flake8
   ./test.py:1:6: E211 whitespace before '('
   print ( "Hello World!" )
        ^
   ./test.py:1:8: E201 whitespace after '('
   print ( "Hello World!" )
          ^
   ./test.py:1:23: E202 whitespace before ')'
   print ( "Hello World!" )
                         ^
   ./test/b.py:4:1: E302 expected 2 blank lines, found 1
   def bar():
   ^
   ./test/b.py:7:1: E302 expected 2 blank lines, found 1
   def baz():
   ^
   ./test/c.py:1:4: E999 SyntaxError: invalid syntax
   x @@@ y
      ^
   ./test/a.py:1:1: F401 'this' imported but unused
   import this
   ^

flake8 --exclude
^^^^^^^^^^^^^^^^

Ignoruj konkrétní soubory či adresáře::

   $ flake8
   ./test.py:1:6: E211 whitespace before '('
   ./test.py:1:8: E201 whitespace after '('
   ./test.py:1:23: E202 whitespace before ')'
   ./test/b.py:4:1: E302 expected 2 blank lines, found 1
   ./test/b.py:7:1: E302 expected 2 blank lines, found 1
   ./test/c.py:1:4: E999 SyntaxError: invalid syntax
   ./test/a.py:1:1: F401 'this' imported but unused
   $ flake8 --exclude=test
   ./test.py:1:6: E211 whitespace before '('
   ./test.py:1:8: E201 whitespace after '('
   ./test.py:1:23: E202 whitespace before ')'

flake8 --ignore
^^^^^^^^^^^^^^^

Ignoruj konkrétní chybové hlášky::

   $ flake8 --ignore=E
   ./test/a.py:1:1: F401 'this' imported but unused
   $ flake8 --ignore=E,F401
   $

flake8 --max-line-length
^^^^^^^^^^^^^^^^^^^^^^^^

Uprav maxilní délku řádku::

   $ cat file.py
   1 * 11 * 111 * 11111 * 11111 * 111111 * 1111111 * 11111111 * 111111111 * 1111111111
   $ flake8 file.py
   file.py:1:80: E501 line too long (83 > 79 characters)
   $ flake8 --max-line-length=99 file.py
   $

flake8 --select
^^^^^^^^^^^^^^^

Zobraz jen konkrétní chybové hlášky::

   $ flake8 --select=F
   ./test/a.py:1:1: F401 'this' imported but unused
   $ flake8 --select=F,E302
   ./test/b.py:4:1: E302 expected 2 blank lines, found 1
   ./test/b.py:7:1: E302 expected 2 blank lines, found 1
   ./test/a.py:1:1: F401 'this' imported but unused

.. note::

   Některé chybové hlášky z ``pycodestyle`` jsou defaultně deaktivovány, např.
   ``E226`` pro chybějící mezery okolo aritmetických operátorů. Z tohoto důvodu
   je třeba explicitně povolit všechny hlášky::

      $ flake8 --select E,F,W

   Zaroveň při použítí ``--select`` dojde k vypnutí pluginů, které nepoužívají
   AST pro detekci chyb, proto je třeba tyto plugin explicitně zapnout pomocí
   volby ``--enable-extensions``.

flake8 --disable-noqa
^^^^^^^^^^^^^^^^^^^^^

Spusť kontrolu s ignorováním ``noqa`` komentářů::

   $ cat a.py
   import this
   $ flake8 a.py
   a.py:1:1: F401 'this' imported but unused
   $ cat b.py
   import this  # noqa
   $ flake8 b.py
   $
   $ flake8 --disable-noqa b.py
   b.py:1:1: F401 'this' imported but unused

.. note::

   Speciální ``noqa`` (Not Quality Assurance) komentáře lze i specifikovat na
   konkrétní kódy chybových hlášek::

      # noqa: E731,E123

.. tip::

   Celý soubor lze ignorovat pomocí ``noqa`` komentáře na začátku řádku, pokud
   nelze použít volbu ``--exclude`` pro explicitní ignorování souborů::

      $ cat file.py
      # flake8: noqa

flake8 --isolated
^^^^^^^^^^^^^^^^^

Spusť kontrolu s ignorováním konfiguračního souboru::

   $ flake8 --isolated

flake8 --count
^^^^^^^^^^^^^^

Zobraz na konci výstupu počet porušení::

   $ flake8 --count
   ./test.py:1:6: E211 whitespace before '('
   ./test.py:1:8: E201 whitespace after '('
   ./test.py:1:23: E202 whitespace before ')'
   ./test/b.py:4:1: E302 expected 2 blank lines, found 1
   ./test/b.py:7:1: E302 expected 2 blank lines, found 1
   ./test/c.py:1:4: E999 SyntaxError: invalid syntax
   ./test/a.py:1:1: F401 'this' imported but unused
   7

flake8 --statistics
^^^^^^^^^^^^^^^^^^^

Zobraz na konci výstupu statistiku porušení::

   $ flake8 --statistics
   ./test.py:1:6: E211 whitespace before '('
   ./test.py:1:8: E201 whitespace after '('
   ./test.py:1:23: E202 whitespace before ')'
   ./test/b.py:4:1: E302 expected 2 blank lines, found 1
   ./test/b.py:7:1: E302 expected 2 blank lines, found 1
   ./test/c.py:1:4: E999 SyntaxError: invalid syntax
   ./test/a.py:1:1: F401 'this' imported but unused
   1     E201 whitespace after '('
   1     E202 whitespace before ')'
   1     E211 whitespace before '('
   2     E302 expected 2 blank lines, found 1
   1     E999 SyntaxError: invalid syntax
   1     F401 'this' imported but unused

Rozšíření
=========

Pro ``flake8`` existuje několik pluginů, které rozšiřují jeho funkčnost. Pokud
jsou tyto pluginy nainstalovány, tak je ``flake8`` automaticky detekuje a
použije::

   $ pip install --user flake8-print
   $ flake8 --help | tail -2
   Installed plugins: flake8-print: 3.0.1, mccabe: 0.6.1, pycodestyle: 2.3.1,
   pyflakes: 1.6.0

.. note::

   Pluginy mohou být defaultně vypnuty nebo upozaděny kvůli ``--select`` volbě,
   není-li nastaveno jinak::

      $ flake8 file.py
      $ flake8 --enable-extensions=T file.py
      ./file.py:1:1: T001 print found.

Konfigurace
===========

Některé volby příkazu ``flake8`` lze uložit do konfiguračního souboru,
zpravidla se jedná o ``setup.cfg`` soubor ve formátu ``INI`` v rootu projektu::

   [flake8]
   # disable-noqa = True
   # enable-extensions = T
   exclude = docs,tests
   # ignore = F401
   max-complexity = 10
   max-line-length = 99
   select = E,F,W
