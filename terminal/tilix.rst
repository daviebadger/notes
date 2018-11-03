=======
 Tilix
=======
--------------------------------
 Terminálový emulátor pro Linux
--------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

Tilix je defaultně nainstalovaný a nastavený jako terminálový emulátor v Ubuntu
Budgie::

   $ tilix --version
   Versions
      Tilix version: 1.7.7
      VTE version: 0.52
      GTK Version: 3.22.30

   Tilix Special Features
      Notifications enabled=0
      Triggers enabled=0
      Badges enabled=0

Klávesové zkratky
=================

Obecné
------

* ``F11``

  * zobraz Tilix přes celou obrazovku nebo také ukonči toto zobrazení

* ``CTRL + SHIFT + n``

  * otevři další Tilix

Kopírování a vkládání textu
^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``CTRL + SHIFT + c``
* ``CTRL + SHIFT + v``

Hledání v textu
^^^^^^^^^^^^^^^

* ``CTRL + SHIFT + f``

Pro skákání na další / předchozí výskyt hledaného výrazu:

* ``CTRL + SHIFT + g``
* ``CTRL + SHIFT + h``

Zvětšování a zmenšování textu
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``CTRL + +``
* ``CTRL + -``

Pro návrat do původního stavu:

* ``CTRL + 0``

Terminál
--------

Otevření nového okna
^^^^^^^^^^^^^^^^^^^^

* ``CTRL + ALT + d``

  * otevři dole další okno terminálu

* ``CTRL + ALT + r``

  * otevři vpravo další okno terminálu

Přepínaní mezi okny
^^^^^^^^^^^^^^^^^^^

* ``ALT + UP``
* ``ALT + DOWN``
* ``ALT + LEFT``
* ``ALT + RIGHT``

Přepínání na konkrétní okna:

* ``ALT + 1``
* ``ALT + 2``
* ``ALT + 3``

Přepínání podle pořádí oken:

* ``CTRL + TAB``
* ``CTRL + SHIFT + TAB``

Změna velikosti okna
^^^^^^^^^^^^^^^^^^^^

* ``SHIFT + ALT + UP``
* ``SHIFT + ALT + DOWN``
* ``SHIFT + ALT + LEFT``
* ``SHIFT + ALT + RIGHT``

Zavření okna
^^^^^^^^^^^^

* ``CTRL + SHIFT + w``

Session
-------

Otevření nové session
^^^^^^^^^^^^^^^^^^^^^

* ``CTRL + SHIFT + t``

Pokud už nějaká session existuje a je uloženo její nastavení (JSON soubor):

* ``CTRL + SHIFT + o``

Uložení nové session
^^^^^^^^^^^^^^^^^^^^

* ``CTRL + SHIFT + s``

.. note::

   Session je třeba uložit explicitně jako JSON soubor, např. `test.json`.

Zobrazení session přehledu
^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``F12``

  * zobraz v bočním panelu přehled a náhled všech otevřených session

Přepínání mezi session
^^^^^^^^^^^^^^^^^^^^^^

Přepínání na konkrétní session:

* ``CTRL + ALT + 1``
* ``CTRL + ALT + 2``
* ``CTRL + ALT + 3``

Přepínání podle pořádí session:

* ``CTRL + PAGE UP``
* ``CTRL + PAGE DOWN``

Zavření session
^^^^^^^^^^^^^^^

* ``CTRL + SHIFT + q``
