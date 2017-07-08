============
 Setuptools
============
--------------------------------------
 Nástroj pro vytváření Python balíčků
--------------------------------------

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

.. tip::

   Nainstaluj vlastní balíček s balícím skriptem v editačním módu::

      $ pip install -e .

   Nainstalovaný vlastní balíček v editačním módu se bude automaticky měnit v
   závilosti na struktuře projektu.

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

  * manuální seznam modulů, které půjdou po instalaci naimportovat::

       setup(
           packages=[
               "foo",
           ],
       )

  * automatický seznam modulů::

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

.. note::

   Závislosti se pišou v duchu Requirements formátu.

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