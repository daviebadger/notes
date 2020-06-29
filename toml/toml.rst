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



Values
======

Strings
-------

Use a string:

* basic:

  * inline:

    .. code:: toml

       key = "I'm David"

  * multine:

    .. code:: toml

       key = """
       This is a
       multi-line
       basic string"""

* literal

  * inline:

    .. code:: toml

       key = 'Cannot use single quotes'

  * multine:

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

Commnets
--------

Add a comment:

* full-line:

  .. code:: toml

     # This is a full-line comment
     # over two lines.
     key = "value"

* inline:

  .. code:: toml

     key = "value"  # This is an inline comment.
