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

Specifikace JSONu
=================

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

Specifikace JSON schémat
========================

Pomocí `JSON schémat <https://json-schema.org/>`_ lze popsat strukturu, jak
mají správně vypadat výsledná data v JSONu. Tyto popsaná schémata lze také
využít k validačním účelům.

.. note::

   Aktuální hrubá pracovní verze je
   `Draft 7 <https://json-schema.org/specification-links.html#draft-7>`_.

.. tip::

   V Pythonu pro validaci JSON schémat existuje externí balíček
   `jsonschema <https://github.com/Julian/jsonschema>`_.

Datové typy
-----------

null
^^^^

Povol jen prázdné hodnoty::

   $ cat null.json
   {
     "type": "null"
   }
   $ cat test_1.json
   null
   $ jsonschema -i test_1.json null.json
   $
   $ cat test_2.json
   0
   $ jsonschema -i test_2.json null.json
   0: 0 is not of type 'null'

.. note::

   JSON schémata jsou zpravidla vždy JSON objekty, ve kterých se nachází
   speciální klíčová slova jako ``type``, pomocí kterých lze popsat a
   nastavovat validační pravidla.

boolean
^^^^^^^

Povol jen booleovské hodnoty::

   $ cat boolean.json
   {
     "type": "boolean"
   }
   $ cat test.json
   true
   $ jsonschema -i test.json boolean.json
   $

.. tip::

   Jednotlivé datové typy lze spolu kombinovat::

      $ cat boolean.json
      {
        "type": ["boolean", "null"]
      }
      $ cat test_1.json
      false
      $ jsonschema -i test_1.json boolean.json
      $
      $ cat test_2.json
      null
      $ jsonschema -i test_2.json boolean.json
      $

number
^^^^^^

Povol jen čísla::

   $ cat number.json
   {
     "type": "number"
   }
   $ cat test_1.json test_2.json test_3.json
   -1
   0
   1.1
   $ jsonschema -i test_1.json number.json
   $ jsonschema -i test_2.json number.json
   $ jsonschema -i test_3.json number.json

Povol jen čísla, které jsou >= minimu X::

   $ cat number.json
   {
     "type": "number",
     "minimum": 0
   }
   $ cat test_1.json
   0
   $ jsonschema -i test_1.json number.json
   $
   $ cat test_2.json
   -1.1
   $ jsonschema -i test_2.json number.json
   -1.1: -1.1 is less than the minimum of 0

Povol jen čísla, které jsou > než minimum X::

   $ cat number.json
   {
     "type": "number",
     "exclusiveMinimum": 0
   }
   $ cat test_1.json
   1
   $ jsonschema -i test_1.json number.json
   $
   $ cat test_2.json
   0
   $ jsonschema -i test_2.json number.json
   0: 0 is less than or equal to the minimum of 0

Povol jen čísla, které jsou <= maximu X::

   $ cat number.json
   {
     "type": "number",
     "maximum": 3
   }
   $ cat test_1.json
   3
   $ jsonschema -i test_1.json number.json
   $
   $ cat test_2.json
   4
   $ jsonschema -i test_2.json number.json
   4: 4 is greater than the maximum of 3

Povol jen čísla, které jsou < než maximum X::

   $ cat number.json
   {
     "type": "number",
     "exclusiveMaximum": 3
   }
   $ cat test_1.json
   2
   $ jsonschema -i test_1.json number.json
   $
   $ cat test_2.json
   3
   $ jsonschema -i test_2.json number.json
   3: 3 is greater than or equal to the maximum of 3

Povol jen čísla, jež jsou násobkem čísla X::

   $ cat number.json
   {
     "type": "number",
     "multipleOf": 3
   }
   $ cat test_1.json
   9
   $ jsonschema -i test_1.json number.json
   $
   $ cat test_2.json
   -3
   $ jsonschema -i test_2.json number.json
   $
   $ cat test_3.json
   1
   $ jsonschema -i test_3.json number.json
   1: 1 is not a multiple of 3

.. note::

   Jednotlivé omezení lze dohromady kombinovat::

      {
        "type": "number",
        "minimum": 0,
        "maximum": 10
      }

.. tip::

   Povol jen celá čísla::

      $ cat integer.json
      {
        "type": "integer"
      }
      $ cat test_1.json
      -1
      $ jsonschema -i test_1.json integer.json
      $
      $ cat test_2.json
      1.1
      $ jsonschema -i test_2.json integer.json
      1.1: 1.1 is not of type 'integer'

   Jako integer se považují i desetinná čísla, která však mají za desetinnou
   čárkou nulu.

string
^^^^^^

Povol jen textové řetězce::

   $ cat string.json
   {
     "type": "string"
   }
   $ cat test_1.json
   "test"
   $ jsonschema -i test_1.json string.json
   $
   $ cat test_2.json
   ""
   $ jsonschema -i test_2.json string.json
   $

Povol jen textové řetězce o minimální délce X::

   $ cat string.json
   {
     "type": "string"
     "minLength": 1
   }
   $ cat test_1.json
   "t"
   $ jsonschema -i test_1.json string.json
   $
   $ cat test_2.json
   ""
   $ jsonschema -i test_2.json string.json
   : '' is too short

Povol jen textové řetězce o maximální délce X::

   $ cat string.json
   {
     "type": "string"
     "maxLength": 4
   }
   $ cat test_1.json
   "test"
   $ jsonschema -i test_1.json string.json
   $
   $ cat test_2.json
   "test test test"
   $ jsonschema -i test_2.json string.json
   test test test: 'test test test' is too long

Povol jen textové řetězce vyhovující danému regulárnímu výrazu::

   $ cat string.json
   {
     "type": "string"
     "pattern": "^ab+c$"
   }
   $ cat test_1.json
   "abbbc"
   $ jsonschema -i test_1.json string.json
   $
   $ cat test_2.json
   "ac"
   $ jsonschema -i test_2.json string.json
   ac: 'ac' does not match '^ab+c$'

.. note::

   Některé regulární výrazy není třeba znovu vynalézat, neboť knihovny, které
   implementují JSON schémata, mohou v sobě obsahovat podporu pro tyto
   speciální formáty dat, ačkoliv jsou defaultně vypnuté::

      $ python3
      >>> from jsonschema import validate, FormatChecker
      >>> FormatChecker.checkers.keys()
      dict_keys(['email', 'ip-address', 'ipv4', 'ipv6', 'host-name', 'hostname', 'regex', 'date', 'time'])
      >>> schema = {"type": "string", "format": "ipv4"}
      >>> validate("a.b.c.d", schema, format_checker=FormatChecker())
      ...

      jsonschema.exceptions.ValidationError: 'a.b.c.d' is not a 'ipv4'

      Failed validating 'format' in schema:
          {'format': 'ipv4', 'type': 'string'}

      On instance:
          'a.b.c.d'

array
^^^^^

Povol jen pole::

   $ cat array.json
   {
     "type": "array"
   }
   $ cat test_1.json
   []
   $ jsonschema -i test_1.json array.json
   $
   $ cat test_2.json
   [0]
   $ jsonschema -i test_2.json array.json
   $

Povol jen pole o minimální velikost X prvků::

   $ cat array.json
   {
     "type": "array",
     "minItems": 1
   }
   $ cat test_1.json
   [1]
   $ jsonschema -i test_2.json array.json
   $
   $ cat test_1.json
   []
   $ jsonschema -i test_2.json array.json
   []: [] is too short

Povol jen pole o maximální velikosti X prvků::

   $ cat array.json
   {
     "type": "array",
     "maxItems": 1
   }
   $ cat test_1.json
   []
   $ jsonschema -i test_1.json array.json
   $
   $ cat test_1.json
   [1, 2]
   $ jsonschema -i test_1.json array.json
   [1, 2]: [1, 2] is too long

Povol jen unikátní pole::

   $ cat array.json
   {
     "type": "array",
     "uniqueItems": true
   }
   $ cat test_1.json
   [1, 2, 3]
   $ jsonschema -i test_1.json array.json
   $
   $ cat test_2.json
   [1, 1, 1]
   $ jsonschema -i test_2.json array.json
   [1, 1, 1]: [1, 1, 1] has non-unique elements

Povol jen pole s přirozenými čísly::

   $ cat array.json
   {
     "type": "array",
     "items": {
       "type": "integer",
       "exclusiveMinimum": 0
     }
   }
   $ cat test_1.json
   [1, 2, 3]
   $ jsonschema -i test_1.json array.json
   $
   $ cat test_2.json
   [1.1, 2, 3]
   $ jsonschema -i test_2.json array.json
   1.1: 1.1 is not of type 'integer'

Povol jen pole, ve kterém prvky od začátku kopírují povolené typy a od nich
jakékoliv hodnoty::

   $ cat array.json
   {
     "type": "array",
     "items": [
       {
         "type": "string"
       },
       {
         "type": "number"
       }
     ]
   }
   $ cat test_1.json
   []
   $ jsonschema -i test_1.json array.json
   $
   $ cat test_2.json
   ["Davie", 23, "male"]
   $ jsonschema -i test_2.json array.json
   $
   $ cat test_3.json
   [23, 23]
   $ jsonschema -i test_3.json array.json
   23: 23 is not of type 'string'

Povol jen omezené pole (n-tice), ve kterém prvky od začátku kopírují povolené
typy a od nich žádné další hodnoty::

   $ cat array.json
   {
     "type": "array",
     "items": [
       {
         "type": "string"
       },
       {
         "type": "number"
       }
     ],
     "additionalItems": false
   }
   $ cat test_1.json
   []
   $ jsonschema -i test_1.json array.json
   $
   $ cat test_2.json
   ["Davie", 23]
   $ jsonschema -i test_2.json array.json
   $
   $ cat test_3.json
   ["Davie", 23, "male"]
   $ jsonschema -i test_3.json array.json
   ['Davie', 23, 'male']: Additional items are not allowed ('male' was unexpected)

object
^^^^^^

Povol jen objekty::

   $ cat object.json
   {
     "type": "object"
   }
   $ cat test_1.json
   {}
   $ jsonschema -i test_1.json object.json
   $
   $ cat test_2.json
   true
   $ jsonschema -i test_2.json object.json
   True: True is not of type 'object'

Povol jen objekty s minimálním počtem klíčů::

   $ cat object.json
   {
     "type": "object",
     "minProperties": 1
   }
   $ cat test_1.json
   {"name": "Davie", "age": 23}
   $ jsonschema -i test_1.json object.json
   $
   $ cat test_2.json
   {"name": "Davie"}
   $ jsonschema -i test_2.json object.json
   $
   $ cat test_3.json
   {}
   $ jsonschema -i test_3.json object.json
   {}: {} does not have enough properties

Povol jen objekty s maximálním počtem klíčů::

   $ cat object.json
   {
     "type": "object",
     "maxProperties": 2
   }
   $ cat test_1.json
   {}
   $ jsonschema -i test_1.json object.json
   $
   $ cat test_2.json
   {"name": "Davie", "age": 23}
   $ jsonschema -i test_2.json object.json
   $
   $ cat test_3.json
   {"name": "Davie", "age": 23, "gender": "male"}
   $ jsonschema -i test_3.json object.json
   {'name': 'Davie', 'age': 23, 'gender': 'male'}: {'name': 'Davie', 'age': 23, 'gender': 'male'} has too many properties

Povol jen objekty, které obsahují dané povinné klíče a jakékoliv další klíče::

   $ cat object.json
   {
     "type": "object",
     "required": ["name"]
   }
   $ cat test_1.json
   {"name": "Davie"}
   $ jsonschema -i test_1.json object.json
   $
   $ cat test_2.json
   {"name": "Davie", "age": 23}
   $ jsonschema -i test_2.json object.json
   $
   $ cat test_3.json
   {}
   $ jsonschema -i test_3.json object.json
   {}: 'name' is a required property

Povol jen objekty, které mohou obsahovat jakékoliv klíče, přičemž definované
klíče musí splňovat dané omezení, pokud se vyskystují v instanci::

   $ cat object.json
   {
     "type": "object",
     "properties": {
       "name": {
         "type": "string"
       }
     }
   }
   $ cat test_1.json
   {}
   $ jsonschema -i test_1.json object.json
   $
   $ cat test_2.json
   {"name": "Davie", "age": 23}
   $ jsonschema -i test_2.json object.json
   $
   $ cat test_3.json
   {"name": false}
   $ jsonschema -i test_3.json object.json
   False: False is not of type 'string'

Povol jen objekty, které mohou obsahovat jenom dané definované klíče a žádné
jiné::

   $ cat object.json
   {
     "type": "object",
     "properties": {
       "name": {
         "type": "string"
       }
     },
     "additionalProperties": false
   }
   $ cat test_1.json
   {}
   $ jsonschema -i test_1.json object.json
   $
   $ cat test_2.json
   {"name": "Davie"}
   $ jsonschema -i test_2.json object.json
   $
   $ cat test_3.json
   {"name": "Davie", "age": 23}
   $ jsonschema -i test_3.json object.json
   {'name': 'Davie', 'age': 23}: Additional properties are not allowed ('age' was unexpected)

Generická klíčová slova
-----------------------

Povol jen konstatní hodnotu::

   $ cat const.json
   {
     "type": number,
     "const": 1
   }
   $ cat test_1.json
   1
   $ jsonschema -i test_1.json const.json
   $
   $ cat test_2.json
   2
   $ jsonschema -i test_2.json const.json
   2: 1 was expected

Povol jen množinu hodnot::

   $ cat enum.json
   {
     "type": "string",
     "enum": ["yes", "no"]
   }
   $ cat test_1.json
   "yes"
   $ jsonschema -i test_1.json enum.json
   $
   $ cat test_2.json
   "y"
   $ jsonschema -i test_2.json enum.json
   y: 'y' is not one of ['yes', 'no']

.. note::

   Tyto generická klíčová slova platí pro jakékoliv datové typy.

Metadata
--------

Přidej titulek do schématu::

   {
     "title": "Person",
     "type": "object"
   }

Přidej popisek do schématu::

   {
     "title": "Person",
     "description": "Person details"
     "type": "object"
   }

Přidej defaultní hodnotu do schématu::

   {
     "type": "integer",
     "default": 0
   }

Přidej ukázky hodnot do schématu::

   {
     "title": "Fruit"
     "type": "string",
     "examples": [
       "apple",
       "banana",
     ]
   }

.. note::

   Všechny tato metadata maji pouze informační charaktor a nelze na ně
   uplatnit validaci, vyjma výchozích hodnot, pokud to implementační
   knihovna nějakým způsobem umožňuje.

.. tip::

   Přidej odkaz na konkrétní verzi JSON schématu, vůči které se má automaticky
   provádat validace::

      {
        "$schema": "http://json-schema.org/draft-07/schema#"
      }

   Přidej odkaz, kde lze nalézt dané schéma veřejně, pokud je to možné::

      {
        "$id": "http://example.com/schemas/person.json"
      }

Kombinace schémat
-----------------

Povol jen jedno schéma z možných schémat::

   $ cat oneof.json
   {
     "oneOf": [
       {
         "type": "array"
       },
       {
         "type": "object"
       }
     ]
   }
   $ cat test_1.json
   []
   $ jsonschema -i test_1.json oneof.json
   $
   $ cat test_2.json
   {}
   $ jsonschema -i test_2.json oneof.json
   $
   $ cat test_3.json
   null
   $ jsonschema -i test_3.json oneof.json
   None: None is not valid under any of the given schemas

.. note::

   Existují i další povolené kombinace ``anyOf``, ``allOf`` a ``not``, které
   spíše zesložiťují, než simplifikují dané JSON schémata a JSON instance.

Znovupoužítí schémat
--------------------

Znovypoužij dané předdefinované schéma::

   $ cat definitions.json
   {
     "definitions": {
       "weather": {
         "type": "object",
         "properties": {
           "name": {"type": "string"},
           "description": {"type": "string"},
           "temperature": {"type": "number"}
         },
         "required": ["name", "temperature"],
         "additionalProperties": false
       }
     },
     "type": "object",
     "properties": {
       "Monday": {"$ref": "#/definitions/weather"},
       "Tuesday": {"$ref": "#/definitions/weather"},
       "Wednesday": {"$ref": "#/definitions/weather"}
     },
     "required": ["Monday", "Tuesday", "Wednesday"],
     "additionalProperties": false
   }
   $ cat test_1.json
   {
     "Monday": {
       "name": "Sunny",
       "temperature": 10
     },
     "Tuesday": {
       "name": "Windy",
       "temperature": 0
     },
     "Wednesday": {
       "name": "Snowy",
       "temperature": -10.5
     }
   }
   $ jsonschema -i test_1.json definitions.json
   $
   $ cat test_2.json
   {}
   $ jsonschema -i test_2.json definitions.json
   {}: 'Monday' is a required property
   {}: 'Tuesday' is a required property
   {}: 'Wednesday' is a required property

.. note::

   Reference na konkrétní schéma se řídí podle standardizovaného JSON Pointeru,
   viz :RFC:`6901`.

.. tip::

   Reference může vést absolutně (viz předchozí RFC), tak i relativně
   (nadstavba pro JSON schémata), na jiné definice a schémata::

      {"$ref": "http://example.com/schemas/address.json"}
      {"$ref": "http://example.com/schemas/meal.json#/definitions/dinner"}

      {"$ref": "address.json"}
      {"$ref": "definitions/meal.json#/definitions/dinner"}

   V případě relativních cest je třeba v implementační knihovně správně
   nakonfigurovat resolver pro hodnoty v ``$ref`` klíči.
