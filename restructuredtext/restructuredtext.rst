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


Admonition Directive
--------------------

Add a custom admonition with the given title to a text:

.. code:: rst

   .. admonition:: See also

      www.example.com for more examples.

Attention Directive
-------------------

Add attentive information to a text:

.. code:: rst

   .. attention::

      The previous example is not possible to create via inline literal markup.

Caution Directive
-----------------

Add cautious information to a text:

.. code:: rst

   .. caution::

      Use wisely the overloaded ``raw-*`` roles.


Danger Directive
----------------

Add dangerous information to a text:

.. code:: rst

   .. danger::

      Do not try this at home!


Default-Role Direcive
---------------------

Set a new default role in a document (a `title` role is by default):

.. code:: rst

   .. default-role:: math

      `f(x) = x^2` == :math:`f(x) = x^2`


Hint Directive
--------------

Add a hint to a text:

.. code:: rst

   .. hint::

      Look at already existing roles.


Important Directive
-------------------

Add important information to a text:

.. code:: rst

   .. important::

      Be consistent with heading levels through a document.


Note Directive
--------------

Add a note to a text:

.. code:: rst

   .. note::

      Code samples using ``::`` markup are not highlighted at all.


Role Directive
--------------

Create a new role in several ways:

#. a dummy role only for styling purposes:

   .. code:: rst

      .. role:: strikethrough

      I do :strikethrough:`not` like reStructuredText.

#. an overloaded ``code`` role with a specific language for inline syntax
   highlighting:

   .. code:: rst

      .. role:: python(code)
         :language: python

      Have you ever tried to run :python:`import this` in your Python interpreter?

#. an overloaded ``raw`` role for a specific output format:

   .. code:: rst

      .. role:: raw-html(raw)
         :format: html

      I do :raw-html:`<del>not</del>` like reStructuredText.

#. an aliased role to built-in roles or custom roles:

   .. code:: rst

      .. role:: strikethrough
      .. role:: strike(strikethrough)

      I do :strike:`not` like reStructuredText.


Tip Directive
-------------

Add a tip to a text:

.. code:: rst

   .. tip::

      Subscripts are ideal candidates for substitutions.


Warning Directive
-----------------

Add a warning to a text:

.. code:: rst

   .. warning::

      Do not exceed the recommended daily dose.



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
