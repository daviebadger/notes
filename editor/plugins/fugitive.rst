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

Ulož změny v souboru a zároveň změn jeho stav (add)::

   :Gwrite
   :Gwrite [path]

.. tip::

   Je-li třeba zároveň i zavřít okno::

      :Gwq

Gread
^^^^^

Zahoď změny v souboru (checkout)::

   :Gread

Gvdiff
^^^^^^

Zobraz vertikálně diff u aktuálního souboru::

   :Gvdiff
   :Gvdiff --staged

.. note::

   Pokud je soubor v konfliktu, tak zobraz vlevo verzi v aktuální větvi,
   uprostřed aktuální obsah souboru a vpravo verzi z mergované větve.

.. tip::

   Pomocí ``^`` lze zobrazit rozdíl oproti poslednímu commitu, pokud v
   aktuálním souboru nejsou žádné změny::

      :Gvdiff ^

Gcommit
^^^^^^^

Vytvoř commit::

   :Gcommit [args]

Gremove
^^^^^^^

Smaž navždy daný soubor (rm)::

   :Gremove

Gmove
^^^^^

Přesuň nebo přejmenuj aktuální soubor::

   :Gmove {destination}

Glog
^^^^

Zobraz historii commitů týkajících se aktuálního souboru::

   :Glog [args]

Zobraz veškerou historii commitů::

   :Glog [args] --

Gmerge
^^^^^^

Vykonej merge::

   :Gmerge [args]

.. note::

   Při konfliktu se vytvoří nové horizontální okno s přehledem konfliktních
   souborů::

      || Auto-merging file.txt
      file.txt|^<<<<<<<| content
      || Automatic merge failed; fix conflicts and then commit the result.

.. tip::

   Při změně obsahu souboru kvůli mergi je dobré znovunačíst soubor pomocí
   ``L`` volby při výzvě::

      W11: Warning: File "file.txt" has changed since editing started
      See ":help W11" for more info.
      [O]K, (L)oad File:

Gfetch
^^^^^^

Vykonej fetch::

   :Gfetch [args]

Gpull
^^^^^

Vykonej pull::

   :Gpull [args]

Gpush
^^^^^

Vykonej push::

   :Gpush [args]

Ggrep
^^^^^

Vykonej grep::

   :Ggrep [args]

Gblame
^^^^^^

Vykonej blame a výsledek zobraz vlevo ve vertikálním okně::

   :Gblame

Ovládání blame okna:

====  ======
Znak  Význam
====  ======
q     zavři okno
A     zobraz jen commity a autory
C     zobraz jen commity
D     zobraz commity, autory a datum s časem
o     zobraz detail commitu v novém horizontálním okně dole
O     zobraz detail commitu v nové záložce
====  ======
