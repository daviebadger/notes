============
 TOML 1.0.0
============
-----------------------------------
 Minimal Configuration File Format
-----------------------------------

:Author: `Davie Badger`_
:Contact: davie.badger@gmail.com
:Copyright:
   `Creative Commons Attribution-ShareAlike 4.0 International Public License`__

.. contents::

.. sectnum::
   :suffix: .

__ https://creativecommons.org/licenses/by-sa/4.0/

.. _Davie Badger: https://github.com/daviebadger



Keys
====

Possible key formats.

Key/Value Pairs
---------------

Add a key with a value in a:

* bare format:

  .. code:: toml

     key = "value"
     key-with-dashes = "value"
     key_with_underscores = "value"

* quoted format:

  .. code:: toml

     "key with spaces" = "value"

* dotted format:

  .. code:: toml

     state.a = "value"
     state.b = "value"
     state.c = "value"

Tables
------

Wrap key/value pairs under a table:

.. code:: toml

   [dev]
   host = "localhost"
   port = 5000

   [test]
   host = "domain"
   port = 5001

Array of Tables
---------------

Wrap key/value pairs under a table array:

.. code:: toml

   [[dns]]
   ip = "1.1.1.1"

   [[dns]]
   ip = "8.8.8.8"



Values
======

Types of values that keys may contain.

Strings
-------

Use a string:

* basic (with escaping):

  * inline:

    .. code:: toml

       key = "I'm David"
       escaped = "\""

  * multi-line:

    .. code:: toml

       key = """
       This is a
       multi-line
       basic string"""

* literal (without escaping):

  * inline:

    .. code:: toml

       key = 'Cannot use single quotes inside'

  * multi-line:

    .. code:: toml

       key = '''
       This is a
       multi-line
       literal string'''

Integers
--------

Use an integer:

* positive:

  .. code:: toml

     key = 1

* positive with underscores:

  .. code:: toml

     key = 1_000_000

* negative:

  .. code:: toml

     key = -1

* negative with underscores:

  .. code:: toml

     key = -1_000_000

Floats
------

Use a float:

* positive:

  .. code:: toml

     key = 1.0

* positive infinity:

  .. code:: toml

     key = inf

* positive scientific notation:

  .. code:: toml

     key = 1e+0

* positive with underscores:

  .. code:: toml

     key = 1.123_456_789

* negative:

  .. code:: toml

     key = -1.0

* negative infinity:

  .. code:: toml

     key = -inf

* negative scientific notation:

  .. code:: toml

     key = -1e+0

* negative with underscores:

  .. code:: toml

     key = -1.123_456_789

Booleans
--------

Use a boolean:

* true:

  .. code:: toml

     key = true

* false:

  .. code:: toml

     key = false

Date-Times
----------

Use a date-time:

* local:

  * with T delimiter:

    .. code:: toml

       key = 2020-01-31T12:30:00

  * without T delimiter:

    .. code:: toml

       key = 2020-01-31 12:30:00

* offset:

  * in UTC with T delimiter:

    .. code:: toml

       key = 2020-01-31T12:30:00Z

  * in UTC without T delimiter:

    .. code:: toml

       key = 2020-01-31 12:30:00Z

  * not in UTC with T delimiter:

    .. code:: toml

       key = 2020-01-31T12:30:00+01:30

  * not in UTC without T delimiter:

    .. code:: toml

       key = 2020-01-31 12:30:00+01:30

Dates
-----

Use a local date:

.. code:: toml

   key = 2020-01-31

Times
-----

Use a local time:

.. code:: toml

   key = 12:30:00

Inline Tables
-------------

Use an inline table:

.. code:: toml

   key = { name = "David", age = 25 }

Arrays
------

Use an array:

* inline:

  .. code:: toml

     key = [ 1, 2, 3 ]

* multi-line:

  .. code:: toml

     key = [
       1,
       2,
       3,
     ]



Other
=====

Syntax neither related to keys nor values.

Commnets
--------

Add a comment:

* inline:

  .. code:: toml

     key = "value"  # This is an inline comment.

* full-line:

  .. code:: toml

     # This is a full-line comment
     # over two lines.
     key = "value"
