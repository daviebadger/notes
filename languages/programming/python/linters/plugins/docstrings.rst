============
 Docstrings
============
---------------------
 Kontrola docstringů
---------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user flake8-docstrings

Ukázka
======

::

   $ cat file.py
   class Class(object):

       def public_method(self):
           pass

       def _private_method(self):
           pass


   def public_function():
       pass


   def _private_function():
       pass
   $ flake8 file.py
   file.py:1:1: D100 Missing docstring in public module
   file.py:1:1: D101 Missing docstring in public class
   file.py:3:1: D102 Missing docstring in public method
   file.py:10:1: D103 Missing docstring in public function

.. note::

   Chybové hlášky ``pydocstyle`` kontrolovače lze najít
   `ZDE <http://www.pydocstyle.org/en/2.1.1/error_codes.html>`_.

.. tip::

   Pluginu lze nastavit, podle jaké konvence má kontrolovat docstringy. Na
   výběr jsou možnosti jen ``pep257`` nebo ``numpy``, přičemž ``google``
   varianta není zatím podporována::

      [flake8]
      # D200: One-line docstring should fit on one line with quotes
      # D413: Missing blank line after last section
      ignore = D200, D413

      [pydocstyle]
      convention = numpy
