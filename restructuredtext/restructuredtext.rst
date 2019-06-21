==================
 reStructuredText
==================
---------------------------------------------------------
 Lightweight Markup Language for Technical Documentation
---------------------------------------------------------

:Author: `Davie Badger`_
:Contact: davie.badger@gmail.com
:Copyright: `Creative Commons Attribution 4.0 International Public License`_

.. _Creative Commons Attribution 4.0 International Public License: https://creativecommons.org/licenses/by/4.0/
.. _Davie Badger: https://github.com/daviebadger



Directives
==========

Directives are the first extension mechanism, how to extend block elements in
|RST|. |RST| has many built-in directives. The syntax of directives is:

.. code:: rst

   .. directive-name:: optional-directive-arguments (on a separate line)
      :optional-directive-option: optional-directive-option-value

      optional-directive-body-elements

Some examples of directive configurations:

.. code:: rst

   1. a directive without arguments, options and body elements::

         .. contents::

   2. a directive with an argument::

         .. include:: path/to/file

   3. a directive with an argument and an option without a value::

         .. include:: path/to/file
            :literal:

   4. a directive with an argument and an option with a value::

         .. image:: path/to/image
            :alt: Alternate text description

   5. a directive with an argument, an option with a value and a body element::

         .. figure:: path/to/image
            :scale: 50 %

            Image title rendered below the image

   6. a directive with a body element::

         .. tip::

            This tip helps you save your money.



Roles
=====

Interpreted text roles are the second extension mechanism, how to extend inline
markup in |RST|. |RST| has several built-in roles. The syntax of roles is:

.. code:: rst

   :role-name:`role-content` (with spaces around except for punctuation marks)

Examples of using roles in sentences:

.. code:: rst

   * This :strong:`word` will be formatted as bold text.
   * Thisis\ :strong:`one`\ word, where the word "one" will be formatted as bold text.
   * It is too :strong:`hot`.


Literal Role
------------

Math Role
---------


Sub Role
--------

Create a subscript:

.. code:: rst

   H\ :sub:`2`\ O is one of the famous chemical formulas.


Sup Role
--------

Create a superscript:

.. code:: rst

   E=mc\ :sup:`2` is one of the famous phyhics formulas.


Title Role
----------

Create a title of a work (book, chapter, other text materials):

.. code:: rst

  `title:`How to Title My Book` is the most selling book in the world.


PEP Role
--------

Create a hyperlink to a specific PEP (Python Enhanced Proposal):

.. code:: rst

   See :PEP:`8` for Python style guide.


RFC Role
--------

Create a hyperlink to a specific RFC (Request For Comments):

.. code:: rst

   See :RFC:`3339` for standardized date and time formats on the Internet.



.. |RST| replace:: reStructuredText
