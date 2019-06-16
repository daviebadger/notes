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
      :optional-directive-option: directive-option-value

      optional-directive-body-elements

Examples:

.. code:: rst

   1. directive without arguments, options and body elements::

         .. contents::

   2. directive with an argument::

         .. include:: path/to/file

   3. directive with an argument and an option::

         .. image:: path/to/image
            :alt: Alternate text description

   4. directive with an argument, an option and a body element::

         .. figure:: path/to/image
            :scale: 50 %

            Image title rendered below the image

   5. directive with a body element::

         .. tip::

            This tip helps you save your money.



Roles
=====

Interpreted text roles are the second extension mechanism, how to extend inline
markup in |RST|. |RST| has several built-in roles. The syntax of roles is:

.. code:: rst

   :role-name:`role-content` (with spaces around)

Examples:

.. code:: rst

   * This :strong:`word` will be formatted as bold text.
   * Thisis\ :strong:`one`\ word, where the word "one" will be formatted as bold text.



.. |RST| replace:: reStructuredText
