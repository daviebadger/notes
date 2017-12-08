===========
 UltiSnips
===========
--------------------------------------------------
 Expanze zkratek do předem připraveného kusu kódu
--------------------------------------------------

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

   Plug 'vim-airline/vim-airline'

Ovládání
========

Tvorba snippetů
---------------

Snippety se tvoří v nakonfigurovaném adresáři, např.::

   css.snippets
   html.snippets
   python.snippets

.. note::

   Pokud je daný typ souboru otevřen ve Vimu, lze příkazem otevřít zdrojové
   kód snippetů v dalším okně po konfiguraci::

      :UltiSnipsEdit

.. tip::

   Snippety mohou dědit z jiných snippetů::

      # html.snippets

      snippet h1
          <h1>$1</h1>

      # htmldjango.snippets

      extends html

      # jinja.snippets

      extends html, htmldjango

Syntaxe
-------

Vytvoř obyčejný snippet::

   snippet hw
       print("Hello World!")

Vytvoř obyčejný snippet včetně popisku snippetu::

   snippet hw "Print 'Hello World'"
       print("Hello World!")

Vytvoř snippet, ve kterém se po expanzi snippetu objeví kurzor na konkrétním
místě::

   snippet hw
       $0print("Hello World!")

Vytvoř snippet s proměnnou včetně placeholderu, který se může přepsat::

   snippet hw
       print("Hello ${0:name}!")

Vytvoř snippet s vícero proměnnými (nulový index je finální skok)::

   snippet for
      for $1 in $2:
          $0

Vytvoř snippet s vícero proměnnými včetně placeholderů::

   snippet for
       for ${1:item} in ${2:items}:
           $0

Vytvoř snippet s několika referencemi na stejnou proměnnou (ostatní reference
se automaticky doplní na základě první reference)::

   snippet bio
       First Name: $1
       Last Name: $2
       Full Name: $1 $2

Vytvoř snippet, ve kterém může být proměnná naplněna z označeného textu z
Visual módu::

   snippet def
       def ${1:func_name}(${2:params}):
           ${0:${VISUAL}}

.. note::

   Pokud je třeba ve snippetech použít znaky ``$``, ``{``, ``\`` nebo zpětnou
   uvozovku, tak je třeba tyto znaky escapovat pomocí ``\``::

      \`
      \$
      \{
      \\

.. tip::

   Snippety musí být za sebou bez prázdných řádků, jinak se nechtěně objeví
   prázdné řádky v souboru jako součast snippetu::

      snippet hw
          print("Hello World!")
      snippet hwn
          print("Hello ${0:name}!")

Konfigurace
===========

::

   " vlož do souborů daný snippet

   let g:UltiSnipsExpandTrigger="<C-j>"

   " skoč na další / předchozí input ve snippetu

   let g:UltiSnipsJumpForwardTrigger="<C-l>"
   let g:UltiSnipsJumpBackwardTrigger="<C-h>"

   " otevři v horizontálním okně zdrojový kód snippetu

   let g:UltiSnipsEditSplit="horizontal"
   let g:UltiSnipsSnippetsDir="~/.vim/snippets"
