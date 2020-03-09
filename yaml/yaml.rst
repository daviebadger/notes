==========
 YAML 1.2
==========
------------------------------------------
 Human-Readable Data Serialization Format
------------------------------------------

:Author: `Davie Badger`_
:Contact: davie.badger@gmail.com
:Copyright:
   `Creative Commons Attribution-ShareAlike 4.0 International Public License`__

.. contents::

.. sectnum::
   :suffix: .

__ https://creativecommons.org/licenses/by-sa/4.0/

.. _Davie Badger: https://github.com/daviebadger



Scalars
=======

Scalars are primitive data structures used as values in collections.

Strings
-------

Use a string:

* flow style:

  * plain (no escape characters):

    .. code:: yaml

       text

  * single-quoted (no escape characters, only double single quotes):

    .. code:: yaml

       'I''m David'

  * double-quoted with escape characters:

    .. code:: yaml

       "Hello\nWorld"

* block style:

  * literal style:

    * clip (a newline at the end):

      .. code:: yaml

         |
           pwd
           ls
           touch file.txt

    * strip (no newline at the end)

      .. code:: yaml

         |-
           pwd
           ls
           touch file.txt

  * folded style:

    * clip (a newline at the end):

      .. code:: yaml

         >
           This is
           the first paragraph.

           This is the second paragraph
           after a line break.

    * strip (no newline at the end)

      .. code:: yaml

         >-
           This is
           the first paragraph.

           This is the second paragraph
           after a line break.

Integers
--------

Use an integer:

* positive:

  .. code:: yaml

     1

* negative:

  .. code:: yaml

     -1

Floating Points
---------------

Use a floating point:

* positive:

  .. code:: yaml

     1.0

* positive infinity:

  .. code:: yaml

     .inf

* positive scientific notation:

  .. code:: yaml

     1e+0

* negative:

  .. code:: yaml

     -1.0

* negative infinity:

  .. code:: yaml

     -.inf

* negative scientific notation:

  .. code:: yaml

     -1e+0

Booleans
--------

Use a boolean:

* true:

  .. code:: yaml

     true

* false:

  .. code:: yaml

     false

Null
----

Use a null:

.. code:: yaml

   null

Timestamps
----------

Use a timestamp:

* ISO date:

  .. code:: yaml

     2020-02-20

* ISO datetime:

  .. code:: yaml

     2020-02-20T00:00:00

* ISO datetime with a time zone:

  .. code:: yaml

     2020-02-20T00:00:00+02:30

* spaced datetime:

  .. code:: yaml

     2020-02-20 00:00:00

* spaced datetime with a time zone:

  .. code:: yaml

     2020-02-20 00:00:00 -1



Collections
===========

Collections are data containers, which contain scalars or also nested
collections.

Mappings
--------

Use a mapping:

* flow style:

  .. code:: yaml

     {x: 0, y: 1}

* block style:

  .. code:: yaml

     boolean: true
     floating point: 1.0
     flow_string: "text"
     integer: 1
     NestedBlockMapping:
       blockString: |-
         text
       NestedFlowMapping: {x: 0, y: 1}
     null: null
     timestamp: 2020-02-20

Sequences
---------

Use a sequence:

* flow style:

  .. code:: yaml

     [0, 1]

* block style:

  .. code:: yaml

     - false
     - -1.0
     - "text"
     - -1
     - flowSequence: [0, 1]
       NestedBlockMapping:
         block string: >-
           text
         blockSequence:
           - {x: 0, y: 1}
           - {x: 1, y: 2}
           - {x: 2, y: 3}
     - null
     - 2020-02-20
