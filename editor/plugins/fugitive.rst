=========
 Fugitive
=========
----------------------
 Ovládání Gitu z Vimu
----------------------

https://github.com/tpope/vim-fugitive

Ovládání
========

Příkazy
-------

Git
^^^

Spusť libovolný Git příkaz jako v terminálu::

   :Git status

.. tip::

   Na aktuálně otevřený soubor lze odkázat pomocí znaku ``%``::

      :Git add %

Gstatus
^^^^^^^

Zobraz v novém okně status repozitáře::

   :Gstatus

   ...

   # On branch master
   #
   # Initial commit
   #
   # Untracked files:
   #   (use "git add <file>..." to include in what will be committed)
   #
   #	file.txt
   #
   nothing added to commit but untracked files present (use "git add" to track)

Po najetí kurzoru na ``#`` u jednotlivých souborů lze použít další znaky k
manipulaci s danými soubory:

=====  ======
Znak   Význam
=====  ======
q      zavři status okno
r      znovunačti status
ENTER  otevři soubor v novém bufferu
o      otevři soubor v novém horizontálním okně
S      otevři soubor v novém vertikálním okně
O      otevři soubor v nové záložce
-      přesuň soubor do jiného stavu nebo vrať do předchozího stavu
dv     zobraz vertikálně diff
U      zahoď změny v souboru nebo jej smaž
cc     vytvoř commit
ca     zahrň soubor do předchozího commitu
cA     zahrň soubor do předchozího commitu a neměn zprávu commitu
=====  ======

.. tip::

   Pomocí ``CTRL + n`` lze skočit ve statusu na další soubor a ``CTRL + p`` na
   předchozí soubor.

Gwrite
^^^^^^

Gread
^^^^^

Gcommit
^^^^^^^

Vytvoř commit::

   :Gcommit [args]

Glog
^^^^

Gmerge
^^^^^^

Gfetch
^^^^^^

Gpull
^^^^^

Gpush
^^^^^
