==============
 Cookiecutter
==============
-----------------------------------------------
 CLI aplikace pro vytváření projektů ze šablon
-----------------------------------------------

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

   $ pip install --user cookiecutter

.. note::

   Pokud není ``pip`` instalován, tak lze nainstalovat pomocí příkazu::

      $ sudo apt install python3-pip

Vytvoření projektu
==================

Vytvoř v aktuálním adresáři projekt z dané šablony::

   $ cookiecutter https://github.com/daviebadger/cookiecutter-python

.. note::

   Po spuštení příkazu se zobrazí prompty pro zadání hodnot, na základě kterých
   se nakonfiguruje projekt.

.. tip::

   Je-li šablona zveřejněna na GitHubu, lze použít zkrácenou referenci na
   šablonu::

      $ cookiecutter gh:daviebadger/cookiecutter-python

   Taktéž lze použít jako argument cestu do adresáře, ve kterém se nachází
   šablona::

      $ cookiecutter ~/templates/cookiecutter-python

Vytvoření šablony
=================

Konfigurační soubor
-------------------

V konfiguračním souboru ``cookiecutter.json`` lze nastavit konfigurační
hodnoty, se kterými lze dále pracovat v rámci šablonování. Uvnitř
konfiguračních hodnot lze použít taktéž šablonování::

   {
     "project_name": "Project",
     "project_slug": "{{ cookiecutter.project_name.lower().replace(' ', '_').replace('-', '_') }}",
     "author": "John Doe"
   }

.. note::

   Hodnoty jednotlivých klíčů jsou defaultní hodnoty, pokud je uživatel
   nepřepíše při zobrazení promptu. Je-li defaultní hodnotou seznam položek,
   tak uživatel si bude moct vybrat položku, přičemž defaultní je první položka.

.. tip::

   Pokud se některé soubory nemají renderovat, neboť obsahují své šablonovací
   značky, které jsou však v konfliktu s ``cookiecutter`` šablonováním, lze
   tyto soubory explicitně vyloučit z renderování::

      {
        "_copy_without_render": [
          "*.html"
        ]
      }

   Jestlíže se nemá renderovat jenom část textu v souboru, lze dané šablonovací
   značky escapovat::

      # inline

      {{ "{{" }} test {{ "}}" }}

      # block

      {% raw %}
      {{ test }}
      {% endraw %}

Šablonování
-----------

Pro práci s dynamickými daty se používá šablonovací systém `jinja`_, do kterého
se nahraje kontext konfiguračního souboru, který je přístupný přes objekt
``cookiecutter`` v šablonách::

   {{ cookiecutter.author.upper() }}

.. note::

   ``cookiecutter`` defaultně v sobě obsahuje šablonovaí rozšíření
   `jinja2-time`_ pro práci s časem a datumem z externí knihovny ``arrow``::

      Today is {% now 'local', '%d-%m-%Y'%}

   Vlastní rozšíření lze zaregistrovat v konfiguračním souboru::

      {
        "_extensions": ["jinja2_time.TimeExtension"]
      }

.. tip::

   Při testování generování projektu lze použít u příkazu ``cookiecutter``
   volbu ``-f``, která násilně přepíše předchozí vygenerováný projekt s téže
   jménem::

      $ cookiecutter -f ~/templates/cookiecutter-python

   Pokud se konfigurační hodnoty nezměnili oproti naposledy vygenerovaného
   projektu, lze použít volbu ``--replay`` pro argumentů při přechozím
   vygenerování projektu::

      $ cookiecutter -f --replay ~/templates/cookiecutter-python

Skripty
-------

Pomocí skriptů lze upravit chování vytvoření projektu ze šablony. Skript lze
sputit jak před vytvořením projektu, tak i po jeho vytvoření. Skripty je
třeba vytvořit v adresáři ``hooks``::

   hooks/
     pre_gen_project.py
     post_gen_project.py
   cookiecutter.json

.. note::

   Pokud exitový kód skriptu není nula, tak se proces vytváření projektu
   zastaví::

      # post_gen_project.py

      import sys

      sys.exit(1)

.. tip::

   I uvnitř skriptů lze přistupovat k hodnotám, které zadal uživatel pro
   ``cookiecutter``, neboť ``pre`` a ``post`` skripty se spustí až po dokončení
   zadávání hodnot uživatelem::

      # pre_gen_project.py

      print("Wait a second {{ cookiecutter.author }} ...")

.. _jinja: https://github.com/pallets/jinja
.. _jinja2-time: https://github.com/hackebrot/jinja2-time
