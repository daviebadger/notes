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
   :suffix: .

.. _Creative Commons Attribution 4.0 International Public License: https://creativecommons.org/licenses/by/4.0/
.. _Davie Badger: https://github.com/daviebadger



Directives
==========

Directives are the first extension mechanism, how to extend block markup in
|RST|. |RST| has many built-in directives. The syntax of directives is:

.. code:: rst

   .. directive-name:: optional-directive-arguments (on a separate line)
      :optional-directive-option: optional-directive-option-value

      optional-directive-body-elements

Some examples of using directives:

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


Class Directive
---------------

Add HTML classes right to the immediately following:

#. element except for block quotes:

   .. code:: rst

      .. class:: heading color-red

      Section Title
      =============

#. block quotes (a special case which needs a comment right after the
   directive):

   .. code:: rst

      .. class:: block-quote
      ..

         This is a block quote.

#. elements inside of the directive:

   .. code:: rst

      .. class:: blink

         This paragraph has the "blink" class.

         This another paragraph also has the "blink" class.


Contents Directive
------------------

Generate a table of contents (TOC) from sections:

#. using a default title for the TOC:

   .. code:: rst

      .. contents::

      ----

      Contents

      * Section A
        * Subsection AA
          * Subsubsection AAA
      * Section B

#. using a custom title for the TOC:

   .. code:: rst

      .. contents:: Table of Contents

      ----

      Table of Contents

      * Section A
        * Subsection AA
          * Subsubsection AAA
      * Section B

#. limiting section levels in the TOC:

   .. code:: rst

      .. contents::
         :depth: 2

      ----

      Contents

      * Section A
        * Subsection AA
      * Section B


Danger Directive
----------------

Add dangerous information to a text:

.. code:: rst

   .. danger::

      Do not try this at home!


Date Directive
--------------

Substitute for a date(time) using a format string for the `time.strftime`_
function in Python:

.. code:: rst

   .. |date| date::
   .. |time| date:: %H:%M:%S

   Last update: |date| at |time|

.. _time.strftime: https://docs.python.org/3/library/time.html#time.strftime


Default-Role Direcive
---------------------

Set a new default role in a document (a `title` role is by default):

.. code:: rst

   .. default-role:: math

      `f(x) = x^2` == :math:`f(x) = x^2`


Figure Directive
----------------

Add an image with a caption:

.. code:: rst

   .. figure:: path/to/image.png

      Caption for the image.

Supported options:

* ``align`` - figure alignment (either no alignment or ``center``)
* ``alt`` - alternate image text
* ``figclass`` - HTML classes to a figure
* ``figwidth`` - width of an image and a caption
* ``height`` - different image height
* ``scale`` - proportional image scale (``100 %`` by default)
* ``target`` - hyperlink target
* ``width`` - different image width


Hint Directive
--------------

Add a hint to a text:

.. code:: rst

   .. hint::

      Look at already existing roles.


Image Directive
---------------

Add an image:

#. from a local filesystem:

   .. code:: rst

      .. image:: path/to/image.png

#. from a remote location:

   .. code:: rst

      .. image:: www.example.com/image.jpg

Supported options:

* ``align`` - image alignment (either no alignment or ``center``)
* ``alt`` - alternate image text
* ``height`` - different image height
* ``scale`` - proportional image scale (``100 %`` by default)
* ``target`` - hyperlink target
* ``width`` - different image width


Important Directive
-------------------

Add important information to a text:

.. code:: rst

   .. important::

      Be consistent with heading levels through a document.


Include Directive
-----------------

Load text from a file to the given place:

#. a custom |RST| document:

   .. code:: rst

      .. include:: path/to/file.rst

#. a file rendered as literal code:

   .. code:: rst

      .. include:: test.py
         :literal:

#. a file rendered as code with syntax highlighting:

   .. code:: rst

      .. include:: test.py
         :code: py

#. a `built-in document`__ with substitution definitions:

   .. code:: rst

      .. include:: <isonum.txt>

      Copyright |copy| Davie Badger 2019.

__ http://docutils.sourceforge.net/docs/ref/rst/definitions.html#character-entity-sets


Meta Directive
--------------

Add HTML meta tags:

.. code:: rst

   .. meta::
      :author: Davie Badger
      :description: reStructuredText is a markup language used for documentation.
      :keywords: rst, reST, reStructuredText


Note Directive
--------------

Add a note to a text:

.. code:: rst

   .. note::

      Code samples using ``::`` markup are not highlighted at all.


Raw Directive
-------------

Bypass parsing text for the given output formats separated by a space:

#. a text inside the directive:

   .. code:: rst

      .. raw:: html

         <iframe id="video-player" width="200" height="200" src="www"></iframe>

#. a text in a local file:

   .. code:: rst

      .. raw:: html
         :file: index.html

#. a text via a URL address:

   .. code:: rst

      .. raw:: html
         :url: www.example.com/file.html


Replace Directive
-----------------

Substitute for a text:

.. code:: rst

   .. |RST| replace:: reStructuredText

   |RST| is too long to type.


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


Sectnum Directive
-----------------

Automatically number section titles:

#. without any options:

   .. code:: rst

      .. sectnum::

      ----

      * 1 Section A
      * 1.1 Subsection AA
      * 1.1.1 Subsubsection AAA
      * 2 Section B

#. with a suffix:

   .. code:: rst

      .. sectnum::
         :suffix: .

      ----

      * 1. Section A
      * 1.1. Subsection AA
      * 1.1.1. Subsubsection AAA
      * 2. Section B

#. with limited section levels:

   .. code:: rst

      .. sectnum::
         :depth: 2

      ----

      * 1 Section A
      * 1.1 Subsection AA
      * 2 Section B


Tip Directive
-------------

Add a tip to a text:

.. code:: rst

   .. tip::

      Subscripts are ideal candidates for substitutions.


Title Directive
---------------

Set a different HTML document title for a browser tab:

.. code:: rst

   **************
   Document Title
   **************

   .. title:: Alternative Document Title


Unicode Directive
-----------------

Substitute for a Unicode character using its code:

#. substituting without trims:

   .. code:: rst

      .. |copy| unicode:: 0xA9 .. copyright sign

      Copyright |copy| Davie Badger 2019.

#. substituting with a left trim (``:ltrim:``) or a right trim (``:rtrim``) or
   both (``:trim:``):

   .. code:: rst

      .. |TM| unicode:: U+2122
         :ltrim:

      Davie Badger |TM| will be rendered like ``Davie Badger^TM``.


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
