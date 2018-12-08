============
 Setuptools
============
--------------------------------------
 Nástroj pro vytváření Python balíčků
--------------------------------------

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

   $ pip install --user setuptools

.. note::

   ``setuptools`` je zpravidla nainstalovaný uvnitř virtualenvu.

Balící skript
=============

Minimální verze balícího skriptu ``setup.py``::

   from setuptools import setup, find_packages

   setup(
       name="nazev-balicku",
       version="0.1.0",
       packages=find_packages(),
   )

.. note::

   Vlastní projekt lze nainstalovat pomocí ``pip`` příkazu nebo přes balící
   skript::

      $ pip install .
      $ python setup.py install

.. tip::

   Pro vývoj je však vhodně nainstalovat projekt v editačním módu, aby se
   reflektovala každá změna v souboru nez nutností opětovně instalace::

      $ pip install -e .
      $ python setup.py develop

Informace o balíčku
-------------------

* ``name``

  * název balíčku::

       setup(
           name="foo",
       )

* ``version``

  * číslo verze::

       setup(
           version="1.2.3",
       )

* ``description``

  * krátký popisek o balíčku::

       setup(
           description="CLI app for downloading images",
       )

* ``long_description``

  * dlouhý popisek o balíčku, zpravidla obsah ``README.rst`` souboru::

       with open("README.rst") as file:
           long_description = file.read()

       setup(
           long_description=long_description,
       )

* ``author``

  * jméno autora balíčku::

       setup(
           author="John Doe",
       )

* ``author_email``

  * email na autora balíčku::

       setup(
           author_email="john.doe@gmail.com",
       )

* ``url``

  * domovská stránka projektu, zpravidla GitHub repozitář::

       setup(
           url="https://github.com/foo/foo,
       )

* ``license``

  * typ licence pro používání balíčku::

       setup(
           license="MIT License",
       )

Zdrojové kódy
-------------

* ``packages``

  * manuální seznam adresářů (balíčků), které půjdou po instalaci naimportovat::

       setup(
           packages=[
               "foo",
           ],
       )

  * automatický seznam balíčků včetně vnořených, jsou-li nějaké v projektu::

       from setuptools import find_packages

       setup(
           packages=find_packages(),
       )

* ``package_data``

  * soubory, které se mají taktéž zabalit vedle zdrojových kódů::

       setup(
           package_data={
               "": "*.rst",
               "foo": ["*.txt"],
           }
       )

* ``py_modules``

  * manuální seznam modulů, které půjdou po instalaci naimportovat::

       setup(
           py_modules=["foo"]
       )

Spustitelné soubory
-------------------

* ``entry_points``

  * seznam konzolových / grafických (GUI) skriptů::

       setup(
           entry_points={
               "console_scripts": [
                   "foo = foo.__main__:main_func",
               ],
               "gui_scripts": [
                   "bar = foo.bar:main_func",
               ]
           }
       )

Závislosti
----------

* ``install_requires``

  * seznam externích balíčků, které se mají spolu s daným projektem
    nainstalovat::

       setup(
           install_requires=[
               "requests",
           ],
       )

* ``extras_require``

  * seznam externích balíčků, které lze dobrovolně doinstalovat::

       setup(
           extras_require={
               "dev": [
                   "flake8",
               ],
           },
       )

.. note::

   Dobrovolné závilosti lze nainstalovat pomocí ``pip`` instalátoru::

      $ pip install package[dev]

.. tip::

   Závislosti lze psát v duchu Requirements formátu::

      setup(
          install_requires=[
               "requests == 2.0.0"
          ],
      )

Klasifikátory
-------------

Volitelná metadata pro snažší filtrování balíčků na PyPI::

   setup(
       classifiers=[
           "Development Status :: 5 - Production/Stable",
           "Environment :: Console",
           "Intended Audience :: Developers",
           "Programming Language :: Python :: 3.6",
           "License :: OSI Approved :: MIT License",
           "Operating System :: POSIX :: Linux",
       ]
   )

.. note::

   Seznam klasifikátorů lze nalézt na
   https://pypi.python.org/pypi?%3Aaction=list_classifiers.

Balení a nahrávání
==================

Balení balíčku
--------------

Vytvoř nezbuildovaný balíček (archív)::

   $ python setup.py sdist

Vytvoř zbuildovaný balíček (wheel)::

   $ python setup.py bdist_wheel

.. note::

   V ``dist/`` adresáři vzniknou nové soubory::

      $ ls
      foo-0.1.0-py3-none-any.whl  foo-0.1.0.tar.gz

Nahrání balíčku na PyPI
-----------------------

Nahrej balíčky na produkční PyPI::

   $ twine upload dist/foo-0.1.0-py3-none-any.whl dist/foo-0.1.0.tar.gz
   $ # or
   $ twine upload dist/*

Nahrej balíčky na testovací PyPI::

   $ twine upload -r testpypi dist/*
   $ # or
   $ twine upload --repository testpypi dist/*

.. note::

   Twine je Python balíček určený pro bezpečné nahrávání balíčků na PyPI.
   Instaluje se příkazem::

      $ pip install twine

Odbočka k PyPI
^^^^^^^^^^^^^^

Pro nahrávání balíčků do centrálního PyPI repozitáře je třeba mít vytvořený
účet a konfigurační soubor ``.pypirc`` v domovském adresáři::

   $ cat ~/.pypirc
   [distutils]
   index-servers = pypi testpypi

   [pypi]
   repository = https://upload.pypi.org/legacy/
   username = johndoe

   [testpypi]
   repository = https://test.pypi.org/legacy/
   username = johndoe

.. note::

   Adresy PyPI serverů pro registraci účtu (nutno ještě potvrdit email):

   * produkční (https://pypi.org/)
   * testovací (https://test.pypi.org/)
