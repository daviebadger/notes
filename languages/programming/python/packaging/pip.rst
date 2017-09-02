=====
 Pip
=====
------------------------
 Správce Python balíčků
------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   sudo apt install python3-pip

Příkazy
=======

pip
---

Zobraz verzi ``pip`` příkazu a napojenou verzi Pythonu::

   $ pip --version
   pip 9.0.1 from /home/davie/.local/lib/python3.5/site-packages (python 3.5)

install
^^^^^^^

Nainstaluj nejnovější verzi balíčku(ů) z `PyPI <https://pypi.python.org/>`_
repozitáře::

   $ pip install virtualenv

Nainstaluj konkrétní verzi balíčku::

   $ pip install virtualenv==15.1.0

.. note::

   Jedná se o systémovou instalaci, která může selhat kvůli nedostatečnému
   oprávnění::

      PermissionError: [Errno 13] Permission denied: '/usr/local/lib/python3.5/dist-packages/virtualenv.py'

.. tip::

   Nainstaluj podmíněnou verzi balíčku::

      $ pip install "virtualenv<15.1.0"
      $ pip install "virtualenv>=15.0.0"

install --user
""""""""""""""

Nainstaluj balíček bez nutnosti administrátorského oprávnění::

   $ pip install --user virtualenv

.. note::

   Je třeba přidat do shellové proměnné ``PATH`` další cestu, aby mohly
   být spuštěný spustitelné soubory z balíčků::

      # ~/.profile

      export PATH="$HOME/.local/bin:$PATH"

install --upgrade
"""""""""""""""""

Upgraduj nainstalovaný balíček na nejnovější verzi::

   $ pip install --upgrade virtualenv
   $ pip install --upgrade --user virtualenv

.. tip::

   Upgraduj samotný ``pip``::

      $ pip install --upgrade pip

list
^^^^

Zobraz seznam nainstalovaných balíčků a jejich verze::

   $ pip list
   virtualenv (15.1.0)

list --outdated
"""""""""""""""

Zobraz seznam instalovaných balíčků, pro které existuje novější verze::

   $ pip list --outdated
   virtualenv (15.0.0.0) - Latest: 15.1.0 [wheel]

freeze
^^^^^^

Zobraz seznam instalovaných balíčku v instalační podobě::

   $ pip freeze
   virtualenv==15.1.0

.. note::

   Seznam těchto balíčku se zpravidla přesměřovává do souboru
   ``requirements.txt`` pro pozdější použítí::

      $ pip freeze > requirements.txt

.. tip::

   Nainstaluj balíčky s konkrétními závislostmi uvedené v ``requirements.txt``
   souboru::

      $ pip install -r requirements.txt

Odbočka k Requirements souboru
""""""""""""""""""""""""""""""

Do Requirements souboru se zapisují balíčky, které pak lze snadno nainstalovat
na jiném počítači::

   # Testing

   pytest
   pytest-cov > 2
   pytest-mock == 1.6.0

.. note::

   Závilosti mohou být uvedeny i ve více souborech, např.::

      requirements.txt
      dev-requirements.txt

   Na jiný Requirements soubor lze odkazovat uvnitř jiného Requirements
   souboru::

      -r dev-requirements.txt

.. tip::

   Při vývoji vlastního uzavřeného softwaru je vhodnější mít striktně
   definované závislosti, jako nabízí výstup příkazu ``pip freezee``.

   Naopak u otevřeného softwaru je vhodnější mít volně definované závilosti,
   aby nedošlo ke kolizi se závislostmi definované uživatelem.

uninstall
^^^^^^^^^

Odinstaluj balíček(y)::

   $ pip uninstall virtualenv
