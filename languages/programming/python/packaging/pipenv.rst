========
 Pipenv
========
-----------------------------------------------------
 Komplexní balíčkovací nástroj pro privátní projekty
-----------------------------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   pip install --user pipenv

Příkazy
=======

pipenv
------

Zobraz použítí ``pipenv`` příkazu::

   Usage: pipenv [OPTIONS] COMMAND [ARGS]...

   Options:
     --where          Output project home information.
     --venv           Output virtualenv information.
     --py             Output Python interpreter information.
     --envs           Output Environment Variable options.
     --rm             Remove the virtualenv.
     --bare           Minimal output.
     --completion     Output completion (to be eval'd).
     --man            Display manpage.
     --three / --two  Use Python 3/2 when creating virtualenv.
     --python TEXT    Specify which version of Python virtualenv should use.
     --site-packages  Enable site-packages for the virtualenv.
     --version        Show the version and exit.
     -h, --help       Show this message and exit.


   Usage Examples:
      Create a new project using Python 3.6, specifically:
      $ pipenv --python 3.6

      Install all dependencies for a project (including dev):
      $ pipenv install --dev

      Create a lockfile containing pre-releases:
      $ pipenv lock --pre

      Show a graph of your installed dependencies:
      $ pipenv graph

      Check your installed dependencies for security vulnerabilities:
      $ pipenv check

      Install a local setup.py into your virtual environment/Pipfile:
      $ pipenv install -e .

      Use a lower-level pip command:
      $ pipenv run pip freeze

   Commands:
     check      Checks for security vulnerabilities and against PEP 508 markers
                provided in Pipfile.
     clean      Uninstalls all packages not specified in Pipfile.lock.
     graph      Displays currently–installed dependency graph information.
     install    Installs provided packages and adds them to Pipfile, or (if none
                is given), installs all packages.
     lock       Generates Pipfile.lock.
     open       View a given module in your editor.
     run        Spawns a command installed into the virtualenv.
     shell      Spawns a shell within the virtualenv.
     sync       Installs all packages specified in Pipfile.lock.
     uninstall  Un-installs a provided package and removes it from Pipfile.
     update     Runs lock, then sync.

pipenv --three
^^^^^^^^^^^^^^

Vytvoř virtuální prostředí pro daný projekt s trojkovou verzí Pythonu::

   $ pipenv --three
   Creating a virtualenv for this project…
   Using /usr/bin/python3 to create virtualenv…
   ⠋Already using interpreter /usr/bin/python3
   Using base prefix '/usr'
   New python executable in /home/davie/.local/share/virtualenvs/test-2dBqg_TL/bin/python3
   Also creating executable in /home/davie/.local/share/virtualenvs/test-2dBqg_TL/bin/python
   Installing setuptools, pip, wheel...done.

   Virtualenv location: /home/davie/.local/share/virtualenvs/test-2dBqg_TL
   Creating a Pipfile for this project…

.. note::

   V adresáři se objeví prázdný ``Pipfile`` soubor, do kterého se budou
   automaticky zapisovat závilosti při instalování externích balíčků::

      $ cat Pipfile
      [[source]]
      url = "https://pypi.python.org/simple"
      verify_ssl = true
      name = "pypi"

      [packages]

      [dev-packages]

      [requires]
      python_version = "3.6"

.. tip::

   Pomocí výskytu ``PIPENV_VENV_IN_PROJECT`` proměnné lze nastavit, aby se
   virtualenvy vytvářely přimo v projektu ve skrytém adresáři ``.venv`` namísto
   centrálního místa ``$HOME/.local/share/virtualenvs``::

      export PIPENV_VENV_IN_PROJECT=true

pipenv --python
^^^^^^^^^^^^^^^

Vytvoř virtuální prostředí pro daný projekt s konkrétní verzí Pythonu::

   $ pipenv --python python2.7
   Creating a virtualenv for this project…
   Using /usr/bin/python2.7 to create virtualenv…
   ⠋Running virtualenv with interpreter /usr/bin/python2.7
   New python executable in /home/davie/test/.venv/bin/python2.7
   Also creating executable in /home/davie/test/.venv/bin/python
   Installing setuptools, pip, wheel...done.

   Virtualenv location: /home/davie/test/.venv
   Creating a Pipfile for this project…

pipenv --rm
^^^^^^^^^^^

Smaž vytvořený virtualenv pro daný projekt::

   $ pipenv --rm
   Removing virtualenv (/home/davie/test/.venv)…

pipenv install
^^^^^^^^^^^^^^

Nainstaluj všechny balíčky z ``Pipfile`` pro produkci::

   $ pipenv install

Nainstaluj konkrétní balíček(y) pro projekt::

   $ pipenv install requests

.. note::

   Při instalaci se automaticky vytvoří ``Pipfile.lock`` soubor, ve kterém
   jsou natvrdo uvedeny závislosti mezi balíčky tak, aby bylo možné mít i na
   jiném počítačí naprosto totožné prostředí.

pipenv install --ignore-pipfile
"""""""""""""""""""""""""""""""

Nainstaluj všechny balíčky z ``Pipfile.lock`` souboru pro produkci::

   $ pipenv install --ignore-pipfile

.. tip::

   Zkráceně lze použít příkaz ``pipenv sync`` pro instalací závislostí z
   ``Pipfile.lock`` souboru.

pipenv install --dev
""""""""""""""""""""

Nainstaluj všechny balíčky z ``Pipfile`` pro vývoj::

   $ pipenv install --dev

Nainstaluj konkrétní balíček(y) pro vývoj::

   $ pipenv install --dev 'pytest>=3.0.0' sphinx

.. tip::

   Vlastní projekt se ``setup.py`` souborem lze nainstalovat do editačního
   módu stejně jako u ``pip`` příkazu::

      $ pipenv install --dev '-e .'

   Při odinstalaci vlastního projektu bude třeba použít hash jako název
   balíčku, který se vygeneroval pro vlastní projekt::

      $ cat Pipfile | grep 'path ='
      "e1839a8" = {path = ".", editable = true}

pipenv update
^^^^^^^^^^^^^

Upgraduj všechny zastaralé balíčky::

   $ pipenv update

pipenv update --outdated
""""""""""""""""""""""""

Zobraz jen zastaralé balíčky::

   $ pipenv update --outdated

.. note::

   Pokud má balíček v ``Pipfile`` natvrdo závislost, např. pomocí ``==``
   operátoru, tak se nové verze balíčku nebudou zobrazovat.

pipenv uninstall
^^^^^^^^^^^^^^^^

Odinstaluj konkrétní balíček::

   $ pipenv uninstall pytest

.. note::

   Při odinstalaci se automaticky aktualizuje ``Pipfile.lock`` se závislostmi.

pipenv uninstall --all
""""""""""""""""""""""

Odinstaluj všechny balíčky z virtualenvu::

   $ pipenv uninstall --all

pipenv lock
^^^^^^^^^^^

Vytvoř nebo aktualizuj ``Pipfile.lock``::

   $ pipenv lock

.. note::

   V ``Pipfile.lock`` se nachází natvrdo všechny verze nainstalovaných balíčků
   tak, aby i na jiném počítači mohlo vzniknout totožné prostředí po instalací
   závilostí z tohoto souboru.

pipenv check
^^^^^^^^^^^^

Zkontroluj bezpečnost závislých balíčků::

   $ pipenv check
   Checking PEP 508 requirements…
   Passed!
   Checking installed package safety…
   All good!

pipenv shell
^^^^^^^^^^^^

Aktivuj virtualenv v novém subshellu::

   $ pipenv shell
   $ exit

.. note::

   Pokud projekt obsahuje soubor ``.env``, ve kterém jsou definované
   proměnné pro daný projekt, ``pipenv`` je automaticky načte do virtualenvu::

      $ cat .env
      NAME="Davie Badger"
      $ echo $NAME

      $ pipenv shell
      $ echo $NAME
      Davie Badger
      $ exit

.. tip::

   Pomocí shell skriptu lze automaticky aktivovat subshell při otevření
   terminálu nebo změně adresáře, je-li virtualenv vytvoření v ``.venv``
   adresáři v projektu::

      activate_venv() {
        if [ -e '.venv' ] && [ -d '.venv' ]; then
          pipenv shell
        fi
      }

      activate_venv

      function cd {
        builtin cd "$@"

        activate_venv
      }

pipenv run
^^^^^^^^^^

Spusť daný příkaz z virtualenvu, aniž by se virtualenv aktivoval v shellu::

   $ pipenv run python -q
   Loading .env environment variables…
   >>> import os
   >>> os.environ["NAME"]
   'Davie Badger'

.. tip::

   Mimo balíčkovací systém ``pipenv`` lze s projektovým ``.env`` souborem
   pracovat pomocí balíčku ``python-dotenv``.
