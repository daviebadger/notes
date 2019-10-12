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



Markup
======

Markup is a set of special constructs in a document which help to define its
structure.

Block Markup
------------

Block markup are constructs which start on a new unindented or indented line
depending on its context.

Block Quotes
^^^^^^^^^^^^

Add a block quote:

#. quote without attribution:

   .. code:: rst

      This is an ordinary paragraph.

         This is a quoted paragraph
         over two lines.

#. quote with attribution:

   .. code:: rst

      This is an ordinary paragraph.

         This is a quote.

         -- X Y

#. multiple quotes:

   .. code:: rst

      Famous quotes from X Y:

         First quote.

      ..

         Second quote.

      ..

         Third quote.

Citations
^^^^^^^^^

Add a citation for a citation reference elsewhere in text:

.. code:: rst

   .. [CVE] CVE terminology and information; https://www.cvedetails.com/cve-help.php

Comments
^^^^^^^^

Add a comment:

.. code:: rst

   .. This is a comment
      over two lines.

      This paragraph is also a part of the comment.

Doctest Blocks
^^^^^^^^^^^^^^

Add a doctest block:

.. code:: rst

   Example from Python:

   >>> print("Hello World")
   Hello World

Footnotes
^^^^^^^^^

Add a footnote for a footnote reference elsewhere in text:

#. manual:

   .. code:: rst

      .. [1] Master documents are special ``index.rst`` files in directories, which
         serve as introductory pages.

#. auto-numbered:

   .. code:: rst

      .. [#] Master documents are special ``index.rst`` files in directories, which
         serve as introductory pages.

Literal Blocks
^^^^^^^^^^^^^^

Add a literal block:

#. marked on a standalone line:

   .. code:: rst

      Example from Python:

      ::

         def hello(name="World"):
             print(f"Hello {name}")


         hello()
         hello("Davie")

#. marked at the end of a text:

   .. code:: rst

      Example from Python::

         hello()

Substitution Definitions
^^^^^^^^^^^^^^^^^^^^^^^^

Add a substitution definition for a substitution reference elsewhere in text:

.. code:: rst

   .. |RST| replace:: reStructuredText

Tables
^^^^^^

Simple Tables
"""""""""""""

Add a simple table:

#. with a table header:

   .. code:: rst

      =========  ========  ======  ===
      Firstname  Lastname  Gender  Age
      =========  ========  ======  ===
      Davie      Badger    Male    24
      Jacob      Badger    Male    19
      =========  ========  ======  ===

#. without a table header:

   .. code:: rst

      =====  ======  ====  ==
      Davie  Badger  Male  24
      Jacob  Badger  Male  19
      =====  ======  ====  ==

#. with an empty table cell:

   .. code:: rst

      =========  ========  ======  ===
      Firstname  Lastname  Gender  Age
      =========  ========  ======  ===
      Davie      Badger    Male    24
      Jacob      Badger    Male    \
      =========  ========  ======  ===

Grid Tables
"""""""""""

Add a grid table:

#. with a table header:

   .. code:: rst

      +------------+--------------------+----------+
      | Header A   | Header B           | Header C |
      +============+====================+==========+
      | A1         | B1 + C1 (column span)         |
      +------------+--------------------+----------+
      | A2 + A3    | * first item       | C2       |
      | (row span) | * second item      |          |
      |            | * third item       |          |
      |            +--------------------+----------+
      |            | C3 is **empty**    |          |
      +------------+--------------------+----------+

#. without a table header:

   .. code:: rst

      +------------+-------------------------------+
      | A1         | B1 + C1 (column span)         |
      +------------+--------------------+----------+
      | A2 + A3    | * first item       | C2       |
      | (row span) | * second item      |          |
      |            | * third item       |          |
      |            +--------------------+----------+
      |            | C3 is **empty**    |          |
      +------------+--------------------+----------+


Transitions
^^^^^^^^^^^

Add a transition (horizontal line):

.. code:: rst

   This is a paragraph.

   ----

   This is a completely different paragraph.


Inline Markup
-------------

Inline markup is a set of special constructs used inside body elements, which
cannot begin or end with whitespace.

Citation Refereces
^^^^^^^^^^^^^^^^^^

Add a citation reference (must be paired with a citation):

.. code:: rst

   CVE is a shortcut for Common Vulnerabilities and Exposures, which is a list
   of software bugs that allow hackers to get into a system or network. [CVE]_

Footnote References
^^^^^^^^^^^^^^^^^^^

Add a footnote reference (must be paired with a footnote):

#. manual:

   .. code:: rst

      This section adornment style is used in master documents [1]_ in Sphinx.

#. auto-numbered:

   .. code:: rst

      This section adornment style is used in master documents [#]_ in Sphinx.

Standalone Hyperlinks
^^^^^^^^^^^^^^^^^^^^^

Add a standalone hyperlink:

#. URI:

   .. code:: rst

      Python documentation is located on https://docs.python.org/.

#. email address:

   .. code:: rst

      Contact me on email davie.badger@gmail.com.

Substitution References
^^^^^^^^^^^^^^^^^^^^^^^

Add a substitution reference (must be paired with a substitution definition):

#. in a line:

   .. code:: rst

      |RST| is really long to type, so it is better to use a word shortcut via
      substitutions.

#. in a line with a hyperlink reference:

   .. code:: rst

      |RST|_ is really long to type, so it is better to use a word shortcut via
      substitutions.

#. in a word:

   .. code:: rst

      Thisis\ |one|\ word



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

Code Directive
--------------

Add a code sample with syntax highlighting:

.. code:: rst

   .. code:: py

      print("Hello World")

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

Supported options:

* ``:depth: number`` - visible section levels (up to)

Csv-Table Directive
-------------------

Add a table in CSV format:

#. CSV table without a header:

   .. code:: rst

      .. csv-table:: Users

         "David", "Badger", "Male", 24
         "Jacob", "Badger", "Male", 19

#. CSV table with a header:

   .. code:: rst

      .. csv-table:: Users
         :header: "Firstname", "Lastname", "Gender", "Age"

         "David", "Badger", "Male", 24
         "Jacob", "Badger", "Male", 19

#. external CSV table without a header:

   .. code:: rst

      .. csv-table::
         :file: data.csv

      .. csv-table::
         :url: www.example.com/data.csv

#. external CSV table with a header in the first row:

   .. code:: rst

      .. csv-table::
         :file: data.csv
         :header-rows: 1

      .. csv-table::
         :url: www.example.com/data.csv
         :header-rows: 1

#. external CSV table with a header in the first column:

   .. code:: rst

      .. csv-table::
         :file: data.csv
         :stub-columns: 1

      .. csv-table::
         :url: www.example.com/data.csv
         :stub-columns: 1

Supported options:

* ``:align: value`` - table alignment (``left``, ``center`` or ``right``)
* ``:delim: character`` - character for separating values (``,``)
* ``:header: "comma-separated-headers"`` - table header in an embedded CSV table
* ``:escape: character`` - escape character for quotes (``""``)
* ``:file: path`` - path to a local CSV table
* ``:header-rows: number`` - number of rows as a table header
* ``:quote: character`` - quote for multi-word values (``"``)
* ``:stub-columns: number`` - number of columns as a table header
* ``:url: address`` - a URL address to a CSV table
* ``:widths: value`` - ``auto`` column widths

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

* ``:align: value`` - figure alignment (either no alignment or ``center``)
* ``:alt: text`` - alternate image text
* ``:figclass: class-names`` - HTML classes to a figure
* ``:figwidth: number`` - width of an image and a caption
* ``:height: number`` - different image height
* ``:scale: percentage`` - proportional image scale (``100 %`` by default)
* ``:target: address`` - hyperlink target
* ``:width: number`` - different image width

Highlights Directive
--------------------

Add a summary of a document or a section:

.. code:: rst

   .. highlights::

      A summary of the story:

      * a
      * b
      * c

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

* ``:align: value`` - image alignment (either no alignment or ``center``)
* ``:alt: text`` - alternate image text
* ``:height: number`` - different image height
* ``:scale: percentage`` - proportional image scale (``100 %`` by default)
* ``:target: address`` - hyperlink target
* ``:width: number`` - different image width

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

Supported options:

* ``:code: language`` - included file as a code block
* ``:literal:`` - included file as a literal block

__ http://docutils.sourceforge.net/docs/ref/rst/definitions.html#character-entity-sets

List-Table Directive
--------------------

Add a list-like table:

#. without a table header:

   .. code:: rst

      .. list-table:: Users

         * - Davie
           - Badger
           - Male
           - 24
         * - Jacob
           - Badger
           - Male
           - 19

#. with a table header in the first row:

   .. code:: rst

      .. list-table:: Users
         :header-rows: 1

         * - Firstname
           - Lastname
           - Gender
           - Age
         * - Davie
           - Badger
           - Male
           - 24
         * - Jacob
           - Badger
           - Male
           - 19

#. with a table header in the first column:

   .. code:: rst

      .. list-table::
         :stub-columns: 1

         * - Name
           - reStructuredText
         * - Shortcut
           - rst
         * - Parser
           - Docutils

Supported options:

* ``:align: value`` - table alignment (``left``, ``center`` or ``right``)
* ``:header-rows: number`` - number of rows as a table header
* ``:stub-columns: number`` - number of columns as a table header
* ``:widths: value`` - ``auto`` column widths

Math Directive
--------------

Add a mathematical formula in LaTeX format with AMS extensions:

.. code:: rst

   .. math::

      f(x) = x^2

Meta Directive
--------------

Add HTML meta tags:

.. code:: rst

   .. meta::
      :author: Davie Badger
      :description: reStructuredText is a markup language used for documentation.

Supported options:

* ``:author: name`` - Document author
* ``:description: text`` - Short document description

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

Supported options:

* ``:file: path`` - Raw content from a file
* ``:url: address`` - Raw content from a URL address

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

Supported options:

* ``:language: code`` -  Language syntax highlighting (only overloaded ``code`` role)
* ``:format: output-formats`` - Render only for the formats (only overloaded ``raw`` role)

Rubric Directive
----------------

Add an informal heading invisible in a table of contents:

.. code::

   .. rubric:: Footnotes

   .. [#] text

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

Supported options:

* ``:depth: number`` - section levels for numbering (up to)
* ``:suffix: characters`` - suffix for numbers (no suffix by default)

Table Directive
---------------

Wrap a simple or a grid table with an optional title:

.. code:: rst

   .. table:: Users

      =========  ========  ======  ===
      Firstname  Lastname  Gender  Age
      =========  ========  ======  ===
      Davie      Badger    Male    24
      Jacob      Badger    Male    19
      =========  ========  ======  ===

Supported options:

* ``:align: value`` - table alignment (``left``, ``center`` or ``right``)
* ``:widths: value`` - ``auto`` column widths

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

Topic Directive
---------------

Add a topic container without a need to create another (sub)section:

.. code:: rst

   Section Title
   =============

   ...

   .. topic:: Idea

      Blah blah blah

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

Supported options:

* ``:ltrim:`` - trim whitespace before a Unicode character
* ``:rtrim:`` - trim whitespace after a Unicode character
* ``:trim:`` - trim whitespace before and after a Unicode character

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

  :title:`How to Title My Book` is the most selling book in the world.

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
