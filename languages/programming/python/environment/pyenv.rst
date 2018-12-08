=======
 Pyenv
=======
------------------------------
 Manažer různých Python verzí
------------------------------

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

   $ git clone https://github.com/pyenv/pyenv.git ~/.pyenv

.. note::

   Jelikož se nejedná o klasický Python balíček, ale o shell skripty, je třeba
   ještě nakonfigurovat shellové proměnné::

      export PYENV_ROOT="$HOME/.pyenv"
      export PATH="$PYENV_ROOT/bin:$PATH"

      if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi

Příkazy
=======

pyenv
-----

install
^^^^^^^

Nainstaluj a zkompiluj ze zdroje konkrétní verzi Pythonu::

   $ pyenv install 3.5.5
   Downloading Python-3.5.5.tar.xz...
   -> https://www.python.org/ftp/python/3.5.5/Python-3.5.5.tar.xz
   Installing Python-3.5.5...
   WARNING: The Python bz2 extension was not compiled. Missing the bzip2 lib?
   WARNING: The Python readline extension was not compiled. Missing the GNU readline lib?
   ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?

   Please consult to the Wiki page to fix the problem.
   https://github.com/pyenv/pyenv/wiki/Common-build-problems


   BUILD FAILED (Ubuntu 17.10 using python-build 1.2.1-17-g907a86b)

   Inspect or clean up the working tree at /tmp/python-build.20180209140248.17929
   Results logged to /tmp/python-build.20180209140248.17929.log

   Last 10 log lines:
   (cd /home/davie/.pyenv/versions/3.5.5/share/man/man1; ln -s python3.5.1 python3.1)
   if test "xupgrade" != "xno"  ; then \
      case upgrade in \
         upgrade) ensurepip="--upgrade" ;; \
         install|*) ensurepip="" ;; \
      esac; \
       ./python -E -m ensurepip \
         $ensurepip --root=/ ; \
   fi
   Ignoring ensurepip failure: pip 9.0.1 requires SSL/TLS

.. note::

   Pro úspěšnou kompilaci je třeba mít nainstalované potřebné systémové
   balíčky, zvláště:

   * ``libbz2-dev``
   * ``libreadline-dev``
   * ``libssl-dev``
   * ``libsqlite3-dev``

   Po úspěšné kompilaci se spustitelné soubory budou nacházet v adresáři
   ``~/.pyenv/versions/<version>/bin``::

      $ ls ~/.pyenv/versions/3.5.5/bin/
      2to3          easy_install-3.5  idle3.5  pip3.5  pydoc3.5  python3.5         python3.5m-config  pyvenv
      2to3-3.5      idle              pip      pydoc   python    python3.5-config  python3-config     pyvenv-3.5
      easy_install  idle3             pip3     pydoc3  python3   python3.5m        python-config
      $ ~/.pyenv/versions/3.5.5/bin/python
      Python 3.5.5 (default, Feb  9 2018, 14:36:29)
      [GCC 7.2.0] on linux
      Type "help", "copyright", "credits" or "license" for more information.
      >>>

install --list
""""""""""""""

Zobraz všechny možné verze Pythonu (CPython) a ostatních interpreterů, které
lze nainstalovat::

   $ pyenv install --list | grep 3.5
     3.3.5
     3.5.0
     3.5-dev
     3.5.1
     3.5.2
     3.5.3
     3.5.4
     3.5.5
     3.5.5rc1
     anaconda3-5.0.0
     anaconda3-5.0.1
     pypy3.3-5.2-alpha1-src
     pypy3.3-5.2-alpha1
     pypy3.3-5.5-alpha-src
     pypy3.3-5.5-alpha
     pypy3.5-c-jit-latest
     pypy3.5-5.7-beta-src
     pypy3.5-5.7-beta
     pypy3.5-5.7.1-beta-src
     pypy3.5-5.7.1-beta
     pypy3.5-5.8.0-src
     pypy3.5-5.8.0
     pypy3.5-5.9.0-src
     pypy3.5-5.9.0
     pypy3.5-5.10.0-src
     pypy3.5-5.10.0
     pypy3.5-5.10.1-src
     pypy3.5-5.10.1
     stackless-3.3.5
     stackless-3.5.4

versions
^^^^^^^^

Zobraz nainstalované verze Pythonu::

   $ pyenv versions
   * system (set by /home/davie/.pyenv/version)
     3.5.5

shell
^^^^^

Nastav konkrétní verzi Pythonu pro aktuální shell::

   $ python3 --version
   Python 3.6.3
   $ pyenv shell 3.5.5
   $ python3 --version
   Python 3.5.5
   $ pyenv shell --unset
   $ python3 --version
   Python 3.6.3

uninstall
^^^^^^^^^

Odinstaluj konkrétní verzi::

   $ pyenv uninstall 3.5.5
   pyenv: remove /home/davie/.pyenv/versions/3.5.5? y
