==================
 reStructuredText
==================
---------------------------------------------------------
 Lightweight Markup Language for Technical Documentation
---------------------------------------------------------

:Author: `Davie Badger`_
:Contact: davie.badger@gmail.com
:Copyright: `Creative Commons Attribution 4.0 International Public License`_

.. contents::

.. sectnum::
   :depth: 3
   :suffix: .

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

#. a directive without arguments, options and body elements:

   .. code:: rst

      .. contents::

#. a directive with an argument:

   .. code:: rst

      .. include:: path/to/file

#. a directive with an argument and an option without a value:

   .. code:: rst

      .. include:: path/to/file
         :literal:

#. a directive with an argument and an option with a value:

   .. code:: rst

      .. image:: path/to/image
         :alt: Alternate text description

#. a directive with an argument, an option with a value and a body element:

   .. code:: rst

      .. figure:: path/to/image
         :scale: 50 %

         Image title rendered below the image

#. a directive with a body element:

   .. code:: rst

      .. tip::

         This tip helps you save your money.



Roles
=====

Interpreted text roles are the second extension mechanism, how to extend inline
markup in |RST|. |RST| has several built-in roles. The syntax of roles is:

.. code:: rst

   :role-name:`role-content` (with spaces around except for punctuation marks)

Examples of using roles:

#. a role at the edge of a sentence:

   .. code:: rst

      It is too :strong:`hot`.

#. a role inside a sentence:

   .. code:: rst

      Do :strong:`not` forget to make your bed!

#. a role inside a word:

   .. code:: rst

      Thisis\ :strong:`one`\ word, where the word "one" will be formatted as bold text.


Literal Role
------------

Create an inline code sample which respects escaped backslashes:

.. code:: rst

   The text inside enclosed double backquotes (:literal:`\`\`...\`\``) is treated as an inline code sample.


Math Role
---------

Create an inline mathematical formula in LaTeX format:

.. code:: rst

   Create a graph of a function :math:`f(x) = x^2`.


Sub Role
--------

Create a subscript:

.. code:: rst

   H\ :sub:`2`\ O is one of the famous chemical formulas.


Sup Role
--------

Create a superscript:

.. code:: rst

   E=mc\ :sup:`2` is one of the famous physics formulas.


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
