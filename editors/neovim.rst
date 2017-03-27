========
 Neovim
========
-------------------------------------------------
 Zrefaktorovaný Vim editor s několika vylepšením
-------------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:Licence: CC BY-SA 4.0

:Abstract:

   `Neovim` vznikl s cílem zejména zjednodušit zdrojóvý kód samotného Vimu,
   který obsahuje přes 300 tisíc řádků a je psán v zastaralém C89, kterému
   rozumí jen pár lidí.

   Při refaktorování kódů došlo taktéž k opravě několika chyb ve Vimu (např.
   delší prodleva při opakovaném vkládání několika znaků z Insert módu) a
   zjednodušení kódu tak, aby byl lepé spravovatelný a každý se mohl zapojit
   do vývoje.

   Neovim nabízí navíc od Vimu:

   - podporu asychronizace
   - zabudovaný terminál
   - simplifikováné API, které může použít jakýkoliv programovací jazyk

   `Online dokumentace`_ Neovimu je vesměs stejná jako u původního Vimu).

Instalace
=========

1. přidat PPA repozitář:

   * pro Ubuntu ve verzi 16.04::

        $ sudo add-apt-repository ppa:neovim-ppa/stable

   * pro jiné verze Ubuntu::

        $ sudo add-apt-repository ppa:neovim-ppa/unstable

2. aktualizovat seznam balíčků::

      $ sudo apt update

3. nainstalovat Neovim::

      $ sudo apt install neovim

Úspěšnou instalaci Neovimu ověřím příkazem::

   $ nvim

po kterém by se měl spustit samotný editor.

Přechod z Vimu
==============

Plug
----

Manažer pluginů jak pro Vim, tak i Neovim. Stáhne se příkazem::

   $ curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

Konfigurační soubor
-------------------

Neovim má konfigurační soubory na jiném místě a to::

   ~/.config/nvim

Do Neovimu lze naimportovat konfigurační soubor jinak určený jen pro Vim,
stačí provést následující příkazy::

   mkdir -p ~/.config/nvim
   ln -s ~/.vim/ ~/.config/nvim/
   ln -s ~/.vimrc ~/.config/nvim/init.vim

.. note::

   Změna obsahu souboru na jednom místě se projeví i na druhém.

Terminál
--------

Neovim má v sobě zabudovaný živý terminál, aniž bych musel opouštět okno
editoru.

Spouští se příkazem::

   :te

Ve výchozím stavu nelze lehce opustit Terminal mód. Je třeba použít dvě
klávesové zkratky za sebou a to:

   CTRL + \
   CTRL + n

Zpátky do Terminal módu se vrací klasicky přes písmenko "i".

.. tip::

   Pro usnadnění opouštění Terminal módu je dobré přemapovat ony dvě
   klávesové zkratky na klásicky ESC::

      if exists(':tnoremap')
          :tnoremap <Esc> <C-\><C-n>
      endif

.. _Neovim: https://neovim.io
.. _Online dokumentace: https://neovim.io/doc/user/
