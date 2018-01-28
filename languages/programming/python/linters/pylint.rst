========
 Pylint
========
----------------------------
 Komplexní kontrolovač kódu
----------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user pylint

Ovládání
========

pylint
------

Zkontroluj kód v souboru::

   $ cat file.py
   print ( "Hello World!"  )
   $ pylint file.py
   No config file found, using default configuration
   ************* Module file
   C:  1, 0: No space allowed around bracket
   print ( "Hello World!" )
         ^ (bad-whitespace)
   C:  1, 0: No space allowed before bracket
   print ( "Hello World!" )
                          ^ (bad-whitespace)
   C:  1, 0: Missing module docstring (missing-docstring)

   ----------------------------------------------------------------------
   Your code has been rated at -20.00/10 (previous run: -20.00/10, +0.00)

.. note::

   Pro kontrolu kódu napříč projektem je třeba správně strukturovat adresáře
   do Python balíčků se soubory ``__init__.py``::

      $ mkdir test
      $ touch test/a.py test/b.py test/c.py
      $ pylint test
      No config file found, using default configuration
      *************
      F:  1, 0: error while code parsing: Unable to load file test/__init__.py:
      [Errno 2] No such file or directory: 'test/__init__.py' (parse-error)
      $ touch test/__init__.py
      $ pylint test
      No config file found, using default configuration

.. tip::

   ``pylint`` lze efektivně kombinovat s ``flake8`` kontrolovačem, kdy druhý
   jmenovaný je čistě na kontrolu PEP 8 standardů a první jmenovaný na hledání
   potencionálních chyb v kódu nebo tipů pro refaktoring.

Odbočka k chybovým hláškám
^^^^^^^^^^^^^^^^^^^^^^^^^^

Kategorie chybových hlášek:

* ``C`` jako porušení PEP 8 konvencí
* ``R`` jako potencionální kód k přepisu
* ``W`` jako varování
* ``E`` jako errory, respektive potencionální bugy
* ``F`` jako fatální errory, kdy ``pylint`` nemohl zkontrolovat soubor

pylint --help-msg
^^^^^^^^^^^^^^^^^

Zobraz popis dané chybové hlášky::

   $ pylint --help-msg=bad-whitspace
   No config file found, using default configuration
   :bad-whitespace (C0326): *%s space %s %s %s*
     Used when a wrong number of spaces is used around an operator, bracket or
     block opener. This message belongs to the format checker.
   $ pylint --help-msg=C0326
   No config file found, using default configuration
   :bad-whitespace (C0326): *%s space %s %s %s*
     Used when a wrong number of spaces is used around an operator, bracket or
     block opener. This message belongs to the format checker.

.. tip::

   Všechny chybové hlášky lze zobrazit pomocí volby ``--list-msgs``::

      $ pylint --list-msgs

pylint --ignore
^^^^^^^^^^^^^^^

Ignoruj konkrétní soubory nebo adresáře::

   $ pylint --ignore=__init__.py,tests

pylint --disable
^^^^^^^^^^^^^^^^

Ignoruj dané chybové hlášky::

   $ pylint --disable=bad-whitespace file.py
   No config file found, using default configuration
   ************* Module file
   C:  1, 0: Missing module docstring (missing-docstring)
   C:  4, 0: Missing class docstring (missing-docstring)
   R:  4, 0: Too few public methods (0/2) (too-few-public-methods)
   C:  8, 0: Missing function docstring (missing-docstring)

   ---------------------------------------------------------------------
   Your code has been rated at 2.00/10 (previous run: -23.33/10, +25.33)
   $ pylint --disable=bad-whitespace,missing-docstring file.py
   ************* Module file
   R:  4, 0: Too few public methods (0/2) (too-few-public-methods)

   ------------------------------------------------------------------
   Your code has been rated at 8.00/10 (previous run: 2.00/10, +6.00)

.. note::

   Taktéž lze použít i další reference na chybové hlášky:

      $ pylint --disable=C0326 file.py
      $ pylint --disable=C file.py
      $ pylint --disable=all file.py

.. tip::

   Lokálně v kódu lze chybu ignorovat pomocí ``pylint`` komentáře::

      $ head -1 file.py
      print ( "Hello World!" )  # pylint: disable=bad-whitespace
      $ pylint file.py
      No config file found, using default configuration
      ************* Module file
      C:  1, 0: Missing module docstring (missing-docstring)
      C:  4, 0: Missing class docstring (missing-docstring)
      R:  4, 0: Too few public methods (0/2) (too-few-public-methods)
      C:  8, 0: Missing function docstring (missing-docstring)

      -------------------------------------------------------------------
      Your code has been rated at 2.00/10 (previous run: -2.00/10, +4.00)

pylint --enable
^^^^^^^^^^^^^^^

Povol chybové hlášky, které jsou ignorovány::

   $ pylint --disable=all --enable=bad-whitespace file.py
   No config file found, using default configuration
   ************* Module file
   C:  1, 0: No space allowed around bracket
   print ( "Hello World!" )
         ^ (bad-whitespace)
   C:  1, 0: No space allowed before bracket
   print ( "Hello World!" )
                          ^ (bad-whitespace)

   -------------------------------------------------------------------
   Your code has been rated at 6.00/10 (previous run: -2.00/10, +8.00)

pylint --load-plugins
^^^^^^^^^^^^^^^^^^^^^

Aktivuj rozšíření, které jsou defaultně vypnuty::

   $ cat file.py
   numbers = [1, 2, 3]
   numbers = range(3)
   $ pylint --disable=C --load-plugins=pylint.extensions.redefined_variable_type file.py
   No config file found, using default configuration
   ************* Module file
   R:  2, 0: Redefinition of numbers type from list to range (redefined-variable-type)

   ---------------------------------------------------------------------
   Your code has been rated at 5.00/10 (previous run: -10.00/10, +15.00)

pylint --reports
^^^^^^^^^^^^^^^^

Zobraz k chybám i report ze statické analýzy (defaultně vypnuto)::

   $ pylint --reports=y file.py
   No config file found, using default configuration
   ************* Module test
   C:  1, 0: No space allowed around bracket
   print ( "Hello World!" )
         ^ (bad-whitespace)
   C:  1, 0: No space allowed before bracket
   print ( "Hello World!" )
                          ^ (bad-whitespace)
   C:  1, 0: Missing module docstring (missing-docstring)
   C:  4, 0: Missing class docstring (missing-docstring)
   R:  4, 0: Too few public methods (0/2) (too-few-public-methods)
   C:  8, 0: Missing function docstring (missing-docstring)

   Report
   ======
   5 statements analysed.

   Statistics by type
   ------------------

   +---------+-------+-----------+-----------+------------+---------+
   |type     |number |old number |difference |%documented |%badname |
   +=========+=======+===========+===========+============+=========+
   |module   |1      |1          |=          |0.00        |0.00     |
   +---------+-------+-----------+-----------+------------+---------+
   |class    |1      |1          |=          |0.00        |0.00     |
   +---------+-------+-----------+-----------+------------+---------+
   |method   |0      |0          |=          |0           |0        |
   +---------+-------+-----------+-----------+------------+---------+
   |function |1      |1          |=          |0.00        |0.00     |
   +---------+-------+-----------+-----------+------------+---------+

   Raw metrics
   -----------

   +----------+-------+------+---------+-----------+
   |type      |number |%     |previous |difference |
   +==========+=======+======+=========+===========+
   |code      |7      |63.64 |NC       |NC         |
   +----------+-------+------+---------+-----------+
   |docstring |0      |0.00  |NC       |NC         |
   +----------+-------+------+---------+-----------+
   |comment   |0      |0.00  |NC       |NC         |
   +----------+-------+------+---------+-----------+
   |empty     |4      |36.36 |NC       |NC         |
   +----------+-------+------+---------+-----------+


   Duplication
   -----------

   +-------------------------+------+---------+-----------+
   |                         |now   |previous |difference |
   +=========================+======+=========+===========+
   |nb duplicated lines      |0     |0        |=          |
   +-------------------------+------+---------+-----------+
   |percent duplicated lines |0.000 |0.000    |=          |
   +-------------------------+------+---------+-----------+

   Messages by category
   --------------------

   +-----------+-------+---------+-----------+
   |type       |number |previous |difference |
   +===========+=======+=========+===========+
   |convention |5      |5        |=          |
   +-----------+-------+---------+-----------+
   |refactor   |1      |1        |=          |
   +-----------+-------+---------+-----------+
   |warning    |0      |0        |=          |
   +-----------+-------+---------+-----------+
   |error      |0      |0        |=          |
   +-----------+-------+---------+-----------+

   Messages
   --------

   +-----------------------+------------+
   |message id             |occurrences |
   +=======================+============+
   |missing-docstring      |3           |
   +-----------------------+------------+
   |bad-whitespace         |2           |
   +-----------------------+------------+
   |too-few-public-methods |1           |
   +-----------------------+------------+

   --------------------------------------------------------------------
   Your code has been rated at -2.00/10 (previous run: -2.00/10, +0.00)

.. note::

   Pokud jsou reporty zobrazeny, lze je vypnout pomocí ``n`` argumentu::

      $ pylint --reports=n file.py

pylint --score
^^^^^^^^^^^^^^

Nezobrazuj skóre z analýzy (defaultně zapnuto)::

   $ pylint --score=n
   No config file found, using default configuration
   ************* Module file
   C:  1, 0: No space allowed around bracket
   print ( "Hello World!" )
         ^ (bad-whitespace)
   C:  1, 0: No space allowed before bracket
   print ( "Hello World!" )
                          ^ (bad-whitespace)
   C:  1, 0: Missing module docstring (missing-docstring)
   C:  4, 0: Missing class docstring (missing-docstring)
   R:  4, 0: Too few public methods (0/2) (too-few-public-methods)
   C:  8, 0: Missing function docstring (missing-docstring)

pylint --generate-rcfile
^^^^^^^^^^^^^^^^^^^^^^^^

Zobraz vygenerovaný konfigurační soubor::

   $ pylint --generate-rcfile

.. note::

   Pro vytvoření konfiguračního souboru je nutné přesměrovat výstup do
   souboru ``.pylintrc``::

      $ pylint --generate-rcfile > .pylintrc

Konfigurace
===========

Některé volby příkazu ``pylint`` lze nakonfigurovat ve vygenerovaném
konfiguračním souboru::

   [MASTER]

   # List of plugins (as comma separated values of python modules names) to load,
   # usually to register additional checkers.
   load-plugins=pylint.extensions.docparams,pylint.extensions.redefined_variable_type

.. note::

   Rozšíření ``docparams`` pro kontrolu správné struktury docstringů je třeba
   ještě dodatečně nakonfigurovat, aby se zobrazovaly správně chybové hlášky::

      # docparams
      accept-no-param-doc=no
      accept-no-raise-doc=no
      accept-no-return-doc=no
      accept-no-yields-doc=no
