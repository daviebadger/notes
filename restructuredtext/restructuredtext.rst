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
