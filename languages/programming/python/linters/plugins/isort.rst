=======
 Isort
=======
-------------------------
 Kontrola pořadí importů
-------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user flake8-isort

Ukázka
======

::

   $ cat file.py
   from os import chdir, path
   import flake8
   from local import (A,
                      B,
                      C)
   import os
   import sys
   import local
   $ flake8 --ignore F file.py
   file.py:1:1: I001 isort found an import in the wrong position
   file.py:2:1: I001 isort found an import in the wrong position
   file.py:2:1: I201 Missing newline before sections or imports.
   file.py:3:1: I001 isort found an import in the wrong position
   file.py:3:1: I201 Missing newline before sections or imports.
   file.py:4:1: I001 isort found an import in the wrong position
   file.py:5:1: I001 isort found an import in the wrong position
   file.py:6:1: I100 Import statements are in the wrong order. import os should be before from local
   file.py:6:1: I201 Missing newline before sections or imports.
   file.py:8:1: I003 isort expected 1 blank line in imports, found 0
   file.py:8:1: I003 isort expected 1 blank line in imports, found 0
   file.py:8:1: I201 Missing newline before sections or imports.

.. note::

   Plugin lze nakonfigurovat, aby byly importy seřazeny lexikograficky a na
   jednom řádku byl jen jeden import::

      [isort]
      force_single_line = true
      force_sort_within_sections = true

.. tip::

   Samotný ``isort`` lze použít jako příkaz pro automatické seřazení importů
   v souborech::

      $ isort --diff file.py
      --- /home/davie/github/notes/languages/programming/python/file.py:before	2018-01-15 20:11:17.532946
      +++ /home/davie/github/notes/languages/programming/python/file.py:after	2018-01-15 20:20:21.045832
      @@ -1,8 +1,11 @@
      -from os import chdir, path
      +import os
      +from os import chdir
      +from os import path
      +import sys
      +
       import flake8
      -from local import (A,
      -                   B,
      -                   C)
      -import os
      -import sys
      +
       import local
      +from local import A
      +from local import B
      +from local import C
      $ isort file.py
      $ cat file.py
      import os
      from os import chdir
      from os import path
      import sys

      import flake8

      import local
      from local import A
      from local import B
      from local import C

   Taktéž lze seřadit všechny importy v projektu::

      $ isort -rc .
      $
