============
 Virtualenv
============
----------------------------------------------------
 Nástroj pro vytváření izolovaných Python prostředí
----------------------------------------------------

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

   $ pip install --user virtualenv

.. note::

   Alternativně lze použít již zabudovaný a osekaný ``venv`` nástroj v Pythonu,
   přičemž je třeba mít nainstalovaný systémový balíček ``python3-venv``::

      $ python3 -m venv venv
      The virtual environment was not created successfully because ensurepip is not
      available.  On Debian/Ubuntu systems, you need to install the python3-venv
      package using the following command.

          apt-get install python3-venv

      You may need to use sudo with that command.  After installing the python3-venv
      package, recreate your virtual environment.

      Failing command: ['/home/davie/github/notes/venv/bin/python3', '-Im', 'ensurepip', '--upgrade', '--default-pip']
      $ sudo apt install python3-venv
      $ python3 -m venv venv
      $ ls
      venv

Virtuální prostředí
===================

Vytvoření virtualenvu
---------------------

Vytvoř virtualenv s verzí Pythonu, ve které je se samotný ``virtualenv``
balíček nainstalován::

   $ virtualenv venv
   Using base prefix '/usr'
   New python executable in /home/davie/test/venv/bin/python3
   Also creating executable in /home/davie/test/venv/bin/python
   Installing setuptools, pip, wheel...done.

Vytvoř virtualenv s jinou verzí Pythonu::

   $ virtualenv --python=/usr/bin/python3.6

.. note::

   Ve virtualenvu, respektive v adresáři ``venv`` se nacházejí zejména
   následující adresáře:

   * ``bin/``

     * adresář se spustitelnými soubory

   * ``lib/``

     * adresář pro standardní knihovnou Pythonu a nainstalované balíčky, které
       se nacházejí v adresářích::

          venv/lib/python3.5/
          venv/lib/python3.5/site-packages

.. tip::

   Verzi Pythonu pro virtualenv lze předem definovat pomocí proměnné v shellu::

      $ export VIRTUALENV_PYTHON=/usr/bin/python3.6
      $ virtualenv venv

Ovládání virtualenvu
--------------------

Aktivace
^^^^^^^^

Aktivuj virtualenv::

   $ source venv/bin/activate

.. note::

   Po aktivaci virtualenvu bude prompt dočasně obsahovat prefix daného
   virtualenvu, není-li nakonfigurováno jinak::

      (venv) davie@badger:~/test$

.. tip::

   Uvnitř virtualenvu lze spustit použitý Python zkráceně::

      $ python

   To samé platí pro instalátor ``pip``, kde není nutné používat volbu
   ``--user``, neboť se balíček instaluje jen pro daný virtualenv::

      $ pip install flake8

Deaktivace
^^^^^^^^^^

Deaktivuj virtualenv::

   $ deactivate

.. note::

   Je-li deaktivace provedena mimo aktivovaný virtualenv, bude se jednat o
   neplatný příkaz::

      $ deactivate
      deactivate: command not found

Smazání virtualenvu
-------------------

Smaž virtualenv::

   $ rm -r venv
