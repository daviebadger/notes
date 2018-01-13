==========
 Bugbear
==========
-----------------------------------------------------------------------------
 Dodatečné varování, které se nehodí ke kontrolovačům pycodestyle a pyflakes
-----------------------------------------------------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user flake8-bugbear

Ukázka
======

::

   $ cat file.py
   def function(mutable=[]):
       try:
           for number in range(10):
               mutable.method()
       except:
           pass
   $ flake8 file.py
   file.py:1:22: B006 Do not use mutable data structures for argument defaults. All calls reuse one instance of that data structure, persisting changes between them.
   file.py:3:13: B007 Loop control variable 'number' not used within the loop body. If this is intended, start the name with an underscore.
   file.py:5:5: E722 do not use bare except'
   file.py:5:5: B001 Do not use bare `except:`, it also catches unexpected events like memory errors, interrupts, system exit, and so on.  Prefer `except Exception:`.  If you're sure what you're doing, be explicit and write `except BaseException:`.
