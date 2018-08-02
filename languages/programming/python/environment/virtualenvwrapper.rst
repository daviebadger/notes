===================
 Virtualenvwrapper
===================
--------------------------
 Rozšíření pro virtualenv
--------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user virtualenvwrapper

.. note::

   Po instalaci je ještě třeba nakonfigurovat ``virtualenvwrapper`` ve
   startovacím skriptu pro shell (``.bashrc``)::

      export WORKON_HOME=$HOME/.virtualenvs             # adresář pro virtualenvy
      export PROJECT_HOME=$HOME/gitlab                  # adresář pro projekty
      export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3  # verze Pythonu při instalaci

      source $HOME/.local/bin/virtualenvwrapper.sh

   Restart ``.bashrc`` souboru::

      $ source ~/.bashrc
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/premkproject
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/postmkproject
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/initialize
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/premkvirtualenv
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/postmkvirtualenv
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/prermvirtualenv
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/postrmvirtualenv
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/predeactivate
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/postdeactivate
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/preactivate
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/postactivate
      virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/get_env_details

Virtuální prostředí
===================

.. note::

   Příkazem ``virtualenvwrapper`` lze zobrazit všechny možné příkazy pro
   práci s virtualenvy pomocí virtualenvwrapperu::

      $ virtualenvwrapper

Vytvoření virtualenvu
---------------------

Vytvoř virtualenv s výchozí verzí Pythonu::

   $ mkvirtualenv venv
   Using base prefix '/usr'
   New python executable in /home/davie/.virtualenvs/venv/bin/python3
   Also creating executable in /home/davie/.virtualenvs/venv/bin/python
   Installing setuptools, pip, wheel...done.
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/venv/bin/predeactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/venv/bin/postdeactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/venv/bin/preactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/venv/bin/postactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/venv/bin/get_env_details

Vytvoř virtualenv s konkrétní verzí Pythonu::

   $ mkvirtualenv --python=python3.6 venv
   Running virtualenv with interpreter /usr/bin/python3.6
   Using base prefix '/usr'
   New python executable in /home/davie/.virtualenvs/venv/bin/python3.6
   Also creating executable in /home/davie/.virtualenvs/venv/bin/python
   Installing setuptools, pip, wheel...done.
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/venv/bin/predeactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/venv/bin/postdeactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/venv/bin/preactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/venv/bin/postactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/venv/bin/get_env_details

.. note::

   Virtualenvy se ukládájí do ``~/.virtualenv``, není-li nakonfigurováno jinak
   v shellové proměnné ``WORKON_HOME``, tudíž je třeba mít unikátně pojmenované
   virtualenvy.

.. tip::

   Vytvoř dočasný virtualenv, který se po deaktivaci smaže včetně vlastních
   vytvořených souborů::

      $ mktmpenv

Ovládání virtualenvu
--------------------

Aktivace
^^^^^^^^

Aktivuj virtualenv::

   $ workon venv

.. note::

   Pomocí ``workon`` příkazu se lze přepnout i na jiný virtualenv::

      $ workon another_venv

   Není-li použít žádný argument pro ``workon``, zobrazí se seznam
   virtualenvů::

      $ workon
      venv

.. tip::

   Spusť příkaz ve všech virtualenvech::

      $ allvirtualenv pip list --outdated

Deaktivace
^^^^^^^^^^

Deaktivuj virtualenv::

   $ deactivate

Smazání virtualenvu
-------------------

Smaž virtualenv::

   $ rmvirtualenv venv

.. note::

   Před smazáním virtualenvu je třeba jej deaktivovat.

Virtuální prostředí s projekty
==============================

Vytvoření projektu s virtualenvem
---------------------------------

Vytvoř projekt se stejnojmenným virtualenvem::

   $ mkproject project
   Using base prefix '/usr'
   New python executable in /home/davie/.virtualenvs/project/bin/python3
   Also creating executable in /home/davie/.virtualenvs/project/bin/python
   Installing setuptools, pip, wheel...done.
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/project/bin/predeactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/project/bin/postdeactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/project/bin/preactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/project/bin/postactivate
   virtualenvwrapper.user_scripts creating /home/davie/.virtualenvs/project/bin/get_env_details
   Creating /home/davie/gitlab//project
   Setting project for project to /home/davie/gitlab/project

Vytvoř projekt s konkrétní verzi Pythonu ve virtualenvu::

   $ mkproject --python=python3.6 project

.. note::

   Projekt se vytvoří v adresáři, který je definovaný v shellové proměnné
   ``PROJECT_HOME``.

.. tip::

   Vytvoř virtualenv, pokud už projekt existuje v ``PROJECT_HOME``::

      $ mkproject --force project

   Vytvoř virtualenv pro projekt mimo ``PROJECT_HOME``::

      $ mkvirtualenv -a ~/test venv
      $ # or
      $ mkvirtualenv -a . venv

Ovládání projektu s virtualenvem
--------------------------------

Aktivuj virtualenv a zároveň zmeň aktuální pracovní adresář na projektový::

   $ pwd
   /home/davie
   $ workon project
   $ pwd
   /home/davie/gitlab/project

.. note::

   Do projektového adresáře se lze kdykoliv vrátít příkazem ``cdproject``::

      $ pwd
      /
      $ cdproject
      $ pwd
      /home/davie/gitlab/project

.. tip::

   Virtualenv lze aktivovat i pomocí skriptu v ``.bashrc``, je-li v kořenu
   projektového adresáře skrytý soubor ``.venv`` s názvem virtualenvu uvnitř::

      activate_venv() {
        if [ -e '.venv' ] && ! [ -f '.venv' ]; then
          workon "$(cat .venv)"
        fi
      }

      activate_venv

      function cd {
        builtin cd "$@"

        activate_venv
      }

Smazání projektu s virtualenvem
-------------------------------

Smaž projekt spolu s virtualenvem::

   $ deactivate
   $ rmvirtualenv project
   $ rm -r ~/gitlab/project
