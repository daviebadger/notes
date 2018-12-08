=====
 Cov
=====
-----------------------------
 Ukazatel pokrytí kódu testy
-----------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user pytest-cov

Ovládání
========

Zobraz statistiku pokrytí kódu testy::

   $ pytest --cov=.
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   plugins: cov-2.5.1
   collected 2 items

   test_add.py ..                                                    [100%]

   ----------- coverage: platform linux, python 3.6.3-final-0 -----------
   Name          Stmts   Miss  Cover
   ---------------------------------
   add.py            2      0   100%
   test_add.py       5      0   100%
   ---------------------------------
   TOTAL             7      0   100%


   ======================= 2 passed in 0.03 seconds ========================

.. note::

   Zobrazená statistika se automaticky ukládá do souboru ``.coverage`` v místě
   spuštění testů, zpravidla v rootu projektu. Pokud už tento soubor existuje,
   tak se přepíše, není-li nastaveno jinak.

.. tip::

   Se statisikou pokrytí kódu umí pracovat různé nástroje, např. pro open
   source projektu to je `Codecov <https://codecov.io/>`_, který archivuje
   minulé statistiky, srovnává je se současným během či posílá alerty při
   poklesu sledovaného % pokrytí kódu.

Konfigurace
===========

Zobraz chybějící neotestované řádky kódu s příkazy::

   $ pytest --cov=trainer --cov-report=term-missing
   ...

   ----------- coverage: platform linux, python 3.6.6-final-0 -----------
   Name                             Stmts   Miss  Cover   Missing
   --------------------------------------------------------------
   trainer/__init__.py                  0      0   100%
   trainer/cli.py                       9      2    78%   19-20

   ...

Ulož statistiku jako HTML soubory do adresáře ``htmlcov``::

   $ pytest --cov=trainer --cov-report=html

Ulož statistiku jako XML soubor do souboru ``coverage.xml``::

   $ pytest --cov=trainer --cov-report=html

.. note::

   Reporty lze kombinovat, např.::

      $ pytest --cov=trainer --cov-report=term-missing --cov-report=xml
      ...

      TOTAL                              296    106    64%
      Coverage XML written to file coverage.xml

      ...

.. tip::

   V případě potřeby lze přejmenovat výstupny soubory a adresáře pro HTML a
   XML report::

      $ pytest --cov=trainer --cov-report=html:cov_html --cov-report=xml:cov.xml
