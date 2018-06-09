=========
 RipGrep
=========
--------------------------------------------------------
 Nejrychlejší inteligentní vyhledávač textu v souborech
--------------------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ cargo install ripgrep

.. note::

   ``cargo`` je součastí ``rustup`` toolchainu, který lze stáhnout a
   nainstalovat pomocí příkazu::

      $ curl https://sh.rustup.rs -sSf | sh

   Poté je nutné zkontrolovat, zda se v bash profilu nachází cesta
   pro nainstalované binárky přes ``cargo`` příkaz::

      export PATH="$HOME/.cargo/bin:$PATH"

.. tip::

   Velikost ``rg`` binárky lze osekat o debugovací symboly pomocí  ``strip``
   příkazu::

      $ ls -lht ~/.cargo/bin | grep -w "rg"
      -rwxr-xr-x 1 davie davie 43M čen  9 10:34 rg
      $ strip ~/.cargo/bin/rg
      $ ls -lht ~/.cargo/bin | grep -w "rg"
      -rwxr-xr-x 1 davie davie 3,9M čen  9 10:40 rg

Příkaz
======

rg
--

Vyhledej pattern v aktuálním adresáři včetně vnořených adresářů::

   $ rg "Lorem ipsum"
   editor/vim.rst
   140:   Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur nostrud

Vyhledej pattern v daném adresáři včetně vnořených adresářů::

   $ rg "Lorem ipsum" editor/
   editor/vim.rst
   140:   Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur nostrud

Vyhledej pattern v daném souboru::

   $ rg "Lorem ipsum" editor/vim.rst
   editor/vim.rst
   140:   Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur nostrud

.. note::

   ``rg`` automaticky respektuje soubor ``.gitignore``. Taktéž defaultně
   ignoruje skryté a binární soubory.

.. tip::

   Vyhledávat lze i na více místech zároveň::

      $ rg dir1/ dir2/ dir3/ file1 file2 file3

rg -h (--help)
^^^^^^^^^^^^^^

Zobraz nápovědu příkazu::

   $ rg --help

rg -c (--count)
^^^^^^^^^^^^^^^

Vyhledej pattern a ve výstupu zobraz jen počet nalezených řádků v souborech::

   $ rg -c lorem
   miscellaneous/ripgrep.rst:10
   editor/plugins/html/emmet.rst:3

rg --colors
^^^^^^^^^^^

Vyhledej pattern a nastav barvy výstupu::

   $ rg --colors 'path:style:bold' --colors 'path:fg:green' --colors 'line:style:bold' --colors 'line:fg:yellow'

.. note::

   Barevné nastavení je jen dočasné, proto je třeba jej uložit jako alias::

      $ export rg=""

   Ripgep defaultně umí detekovat, kdy má ve výstupu použít barvy a kdy naopak
   ne, např. při přesměrování výstupu.

rg -C (--context)
^^^^^^^^^^^^^^^^^

Vyhledej pattern a zobraz kontext okolo najitého řádku ve výstupu::

   $ rg lorem
   miscellaneous/ripgrep.rst
   99:   $ rg -i lorem
   $ rg -C 3 lorem
   miscellaneous/ripgrep.rst
   96-
   97-Vyhledej pattern s ignorancí rozdílu velkých a malých písmen::
   98-
   99:   $ rg -i lorem
   100-
   101-rg --vimgrep
   102-^^^^^^^^^^^^

.. note::

   Pokud se pattern nachází vícekrát v jednom souboru daleko od sebe, tak se
   defaultně jako oddělovátko použije ``--``::

      $ rg -C 1 lorem
      editor/plugins/html/emmet.rst
      211-
      212:* ``lorem`` + ``<C-Y>,``
      213-
      --
      215-
      216:       p>lorem
      217-
      --
      228-
      229:      ul>li*3>lorem1
      230-

.. tip::

   Pro zobrazení řádku před nebo po najitém řádku lze použít volby ``-B``,
   respektive ``-A``::

      $ # before
      $ rg -B 3 lorem  # or --before-context
      editor/plugins/html/emmet.rst
      209-Generování náhodných slov
      210--------------------------
      211-
      212:* ``lorem`` + ``<C-Y>,``
      $ # after
      $ rg -A 3 lorem  # or --after-context
      editor/plugins/html/emmet.rst
      212:* ``lorem`` + ``<C-Y>,``
      213-
      214-  * vlož náhodný text o délce 30 slov::
      215-

rg -e (--regexp)
^^^^^^^^^^^^^^^^

Vyhledej několik patternů najednou::

   $ cat test.txt
   foo
   bar
   baz
   $ rg foo test.txt
   1:foo
   $ rg -e foo test.txt
   1:foo
   $ rg -e foo -e bar -e baz test.txt
   1:foo
   2:bar
   3:baz

.. note::

   Výstup hledání se zobrazí, když existuje výsledek alespoň pro jeden
   definovaný pattern pomocí volby ``-e``.

rg -F (--fixed-strings)
^^^^^^^^^^^^^^^^^^^^^^^

Vyhledej pattern jako obyčejný text bez interpolace speciálních znaků, jako
u regulárních výrazů::

   $ rg "^C"
   LICENSE
   5:Creative Commons Corporation ("Creative Commons") is not a law firm and
   $ rg -F "^C"
   container/docker.rst
   1114:      ^P^C

rg -g (--glob)
^^^^^^^^^^^^^^

Vyhledej pattern jenom v souborech splňující daný glob::

   $ rg -g "*.rst" lorem

.. note::

   Pomocí vykričníku lze inverzeně obrátit glob::

      $ rg -g "!*.min.js" txt

rg -i (--ignore-case)
^^^^^^^^^^^^^^^^^^^^^

Vyhledej pattern s ignorancí rozdílu velkých a malých písmen::

   $ rg -i lorem

rg --sort-files
^^^^^^^^^^^^^^^

Vyhledej pattern a seřaď abecedně výstup::

   $ rg --sort-files lorem

.. note::

   Defaultně výstup není seřazen podle cesty k souboru, neboť vyhledávání
   probíhá paralelně.

rg -t (--type)
^^^^^^^^^^^^^^

Vyhledej pattern jen v daným typech souborů::

   $ rg -t rst -t md text

.. note::

   Seznam podporovaných typů souboru lze zobrazit pomocí volby
   ``--type-list``::

      $ rg --type-list

rg -T (--type-not)
^^^^^^^^^^^^^^^^^^

Vyhledej pattern mimo dané typy souborů::

   $ rg -T py text

rg -u (--unrestricted)
^^^^^^^^^^^^^^^^^^^^^^

Vyhledej pattern a ignoruj ``.gitignore``::

   $ rg -u text

Vyhledej pattern kromě ignorace ``.gitignore`` souboru i ve skrytých
souborech::

   $ rg -uu text

rg -v (--invert-match)
^^^^^^^^^^^^^^^^^^^^^^

Vyhledej obraceně pattern::

   $ cat text.txt
   # comment
   a = 1
   # comment
   b = 2
   # comment
   c = 3
   $ rg "#" text.txt
   1:# comment
   3:# comment
   5:# comment
   $ rg -v "#" text.txt
   2:a = 1
   4:b = 2
   6:c = 3

rg -V (--version)
^^^^^^^^^^^^^^^^^

Zobraz verzi vyhledávače::

   $ rg -V
   ripgrep 0.8.1

rg --vimgrep
^^^^^^^^^^^^

Vyhledej pattern a výstup ulož ve formátu pro Vim::

   $ rg --vimgrep lorem
   miscellaneous/ripgrep.rst:99:12:   $ rg -i lorem

rg -w
^^^^^

Vyhledej pattern jako samostatné slovo v textu::

   $ ls ~/.cargo/bin/
   cargo  cargo-fmt  rg  rls  rustc  rustdoc  rustfmt  rust-gdb  rust-lldb  rustup
   $ ls ~/.cargo/bin/ | rg rg
   cargo
   cargo-fmt
   rg
   $ ls ~/.cargo/bin/ | rg -w rg
   rg

rg -x (--line-regexp)
^^^^^^^^^^^^^^^^^^^^^

Vyhledej pattern, který existuje samostatně na řádku::

   $ cat test.txt
   foo foo
   bar
   baz
   $ rg -x foo test.txt
   $ rg -x bar test.txt
   2:bar
