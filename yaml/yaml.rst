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



Collections
===========

Collections are data containers, which contain scalars or also nested
collections.

Mappings
--------

Sequences
---------
