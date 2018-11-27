======
 JSON
======
--------------------------------------------------------
 Textový formát pro výměnu dat mezi klientem a serverem
--------------------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Specifikace
===========

Objekt
------

Objekt obsahuje zpravidla neseřazené klíče s hodnotami::

   {
     "name": "Davie",
     "age": 23
   }

.. note::

   Názvy klíču jsou zpravidla ve tvaru `camelCase`, neboť s JSONem se primárně
   pracuje na straně klienta v prohlížeči v Javascriptu, kde je tento tvar
   standardem v pojmenování proměnných, funkcí, objektů atd.

   Sekundárně lze JSON použít v RPC komunikaci mezi klintem a serverem nebo
   také jako konfigurační soubory.

.. tip::

   Ačkoliv JSON nemá standardizované odsazení, tak lze opět použít standard
   z Javascriptu a to o velikosti dvou mezer, případně v Pythonu klasicky
   čtyři mezery::

      $ apt install jq
      $ echo "{\"name\": \"Davie\", \"age\": 23}" | jq  # bez barev s -M přepínačem
      {
        "name": "Davie",
        "age": 23
      }
      $ python3
      >>> import json
      >>> print(json.dumps({"name": "Davie", "age": 23}, indent=4))
      {
          "name": "Davie",
          "age": 23
      }

   Pomocí nástroju pro zpracování JSONu lze i abecedně seřazovat klíče v
   objektu::

      $ echo "{\"name\": \"Davie\", \"age\": 23}" | jq -S
      {
        "age": 23,
        "name": "Davie"
      }
      $ python3
      >>> import json
      >>> print(json.dumps({"name": "Davie", "age": 23}, indent=4, sort_keys=True))
      {
          "age": 23,
          "name": "Davie"
      }

Hodnoty klíčů v objektu
^^^^^^^^^^^^^^^^^^^^^^^

Klíče v objektu mohou nabývat těchto hodnot::

   {
      "truthy_boolean": true,
      "falsy_boolean": false,
      "positive_integer": 1,
      "negative_integer": -1,
      "positive_float": 1.0,
      "negative_float": -1.0,
      "text": "text",
      "object": {
        "text": "text",
      }
      "empty_object": {},
      "array": [{
         "text": "text",
      }],
      "empty_array": [],
      "null": null,
   }

.. note::

   Objekty by se měly co nejméně zanořovat do sebe. Výjimky platí jen pro
   objekty, které tvoří relaci na jiný objekt, kdy se místo ID objektu zobrazí
   celý relační objekt.

   V případě hluboké zanoření se komplikuje cesta k danému objektu a program
   může být více nachýlný na chyby::

      $ python3
      >>> x = {"x": {"x": {"x": {"x": {"x": 0}}}}}
      >>> x["x"]["x"]["x"]["x"]["x"]
      0
      >>> x.get("x", {}).get("x", {}).get("x", {}).get("x", {}).get("x", 0)
      1

.. tip::

   Klíče s nulovými hodnotami `null` by se zpravidla neměly v objektu vůbec
   vyskytovat, pokud samotné klíče nejsou povinné např. jako sloupce v tabulce.

   Zejména v dynamických jazycích může docházet k nepříjemnostem::

      $ python3
      >>> x = {"x": None}
      >>> x.get("x", False)  # Vychozi hodnota, pokud klic neexistuje
      >>>
      >>> x.get("x", False) or False
      False

Pole
----

Pole tvoří seznam objektů::

   [{"x": 0}, {"y": 1}, {"z": 2}]

.. note::

   Pole jsou zpravidla seřazená podle ID, případně jiného klíče v objektu,
   např. podle datumu.

.. tip::

   Velikost JSONu, respektive textového souboru lze snížít pomocí minifikace::

      $ echo "{\"name\": \"Davie\", \"age\": 23}" | jq -c
      {"name":"Davie","age":23}
      $ python3
      >>> import json
      >>> print(json.dumps({"name": "Davie", "age": -23.4}, separators=(",", ":")))
      {"name":"Davie","age":-23.4}
