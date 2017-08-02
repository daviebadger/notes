======
 Yarn
======
----------------------
 Správce Node balíčků
----------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
   echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
   sudo apt update && sudo apt install yarn

Příkazy
=======

yarn
----

Zobraz verzi ``yarn`` příkazu::

   $ yarn --version
   0.27.5

init
^^^^

Inicializuj nový projekt::

   $ yarn init
   yarn init v0.27.5
   question name (project): foo
   question version (1.0.0): 0.1.0
   question description: foo description
   question entry point (index.js):
   question repository url:
   question author (davie.badger <davie.badger@gmail.com>):
   question license (MIT):
   success Saved package.json
   Done in 22.26s.

.. note::

   V adresáří se vytvoří soubor ``package.json`` s informacemi o projektu.

add
^^^

Nainstaluj lokálně balíček(y)::

   $ yarn add vue
   yarn add v0.27.5
   [1/4] Resolving packages...
   [2/4] Fetching packages...
   [3/4] Linking dependencies...
   [4/4] Building fresh packages...
   success Saved lockfile.
   success Saved 1 new dependency.
   └─ vue@2.4.1
   Done in 0.66s.

.. note::

   Lokálně se balíčky instalují do adresáře ``node_modules``. Nainstalované
   balíčky se automaticky zapisují do ``package.json``::

      {
        "dependencies": {
          "vue": "^2.4.1"
        }
      ]

   Taktéž se vytvoří ``yarn.lock``, kde jsou detailně zmapovány závislosti
   mezi jednotlivými balíčky tak, aby jiný uživatel měl po instalaci projektu
   stejné verze balíčků na svém počítači.

Odbočka ke specifikovaní verze instalovaného balíčku
""""""""""""""""""""""""""""""""""""""""""""""""""""

Při instalaci lze určit, jaká verze se má nainstalovat::

   $ yarn add vue@2.0.0

Taktéž lze použít i relační operátory pro specifikování verze::

   $ yarn add vue@"<2.0.0"          # 1.0.28
   $ yarn add vue@"<=2.0.0"         # 1.0.28
   $ yarn add vue@">2.0.0"          # 2.4.1
   $ yarn add vue@">=2.0.0"         # 2.4.1
   $ yarn add vue@">=2.0.0 <3.0.0"  # 2.4.1

.. note::

   Yarn defaultně nainstaluje balíčky tak, aby se s přístí instalací
   nepovýšilo první nenulové číslo::

      $ yarn add vue@"^2.0.0"  # >=2.0.0 <3.0.0
      $ yarn add vue@"^0.1.0"  # >=0.1.0 <1.0.0
      $ yarn add vue@"^0.0.0"  # >=0.0.0 <0.1.0

add --dev
"""""""""

Nainstaluj lokálně balíček jen pro vývoj::

   $ yarn add --dev vue-cli

global
^^^^^^

Nainstaluj globálně balíček::

   $ sudo yarn global add vue-cli

.. note::

   Pomocí ``global`` příkazu lze instalovat, upgradovat či odstraňovat
   globální balíčky.

upgrade
^^^^^^^

Vylepší verzi balíčku(ů)::

   $ yarn upgrade vue
   $ yarn upgrade vue@2.1.0

.. note::

   Defaultně se vylepšuje na nejnovější verzi, není-li podmíněno jinak.

install
^^^^^^^

Nainstaluj všechny závislosti z ``package.json``::

   $ yarn install

.. tip::

   Zkráceně bez subpříkazu ``install``::

      $ yarn

install --production
""""""""""""""""""""

Nainstaluj jen ty závislosti z ``dependencies`` klíče v ``package.json``::

   $ yarn
   $ yarn install --production

remove
^^^^^^

Odinstaluj balíček(y)::

   yarn remove v0.27.5
   [1/2] Removing module vue...
   [2/2] Regenerating lockfile and installing missing dependencies...
   success Uninstalled packages.
   Done in 0.20s.

.. note::

   Při odinstalaci balíčku dojde také k jeho odstranění z ``package.json``.

list
^^^^

Zobraz verze nainstalovaných balíčků včetně jejich závislostí::

   $ yarn list

.. tip::

   Zobraz verze nainstalovaných balíčků bez jejich závislostí::

      $ yarn list --depth=0

outdated
^^^^^^^^

Zobraz seznam nainstalovaných balíčků, pro které existuje novější verze::

   $ yarn outdated
   yarn outdated v0.27.5
   Package Current Wanted Latest Package Type URL
   vue     2.0.0   2.0.0  2.4.1  dependencies https://github.com/vuejs/vue#readme
   Done in 0.65s.

info
^^^^

Zobraz info o konkrétním balíčků::

   $ yarn info vue

.. tip::

   Zobraz seznam všech verzí daného balíčku::

      $ yarn info vue versions

run
^^^

Spusť skript definovaný v ``package.json``::

   $ cat package.json
   {
     "name": "hello-world"
     "scripts": {
       "echo": "echo Hello World"
     }
   }
   $ yarn run echo
   yarn run v0.27.5
   $ echo Hello World
   Hello World
   Done in 0.11s.

.. note::

   Pomocí ``run`` příkazu lze spouštět i příkazy nainstalované spolu s balíčky.

config
^^^^^^

config list
"""""""""""

Zobraz nastavení::

   $ yarn config list
   yarn config v0.27.5
   info yarn config
   { 'version-tag-prefix': 'v',
     'version-git-tag': true,
     'version-git-sign': false,
     'version-git-message': 'v%s',
     'init-version': '1.0.0',
     'init-license': 'MIT',
     'save-prefix': '^',
     'ignore-scripts': false,
     'ignore-optional': false,
     registry: 'https://registry.yarnpkg.com',
     'strict-ssl': true,
     'user-agent': 'yarn/0.27.5 npm/? node/v8.1.2 linux x64' }
   info npm config
   {}
   Done in 0.04s.

config get
""""""""""

Zobraz konkrétní nastavení::

   $ yarn config get init-version
   1.0.0

config set
""""""""""

Změn konkrétní nastavení::

   $ yarn config set init-version 0.1.0
   yarn config v0.27.5
   success Set "init-version" to "0.1.0".
   Done in 0.04s.
