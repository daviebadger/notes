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
