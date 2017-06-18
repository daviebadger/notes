==========
 Surround
==========
-------------------------------------
 Obklopovač uvozovek, závorek a tagů
-------------------------------------

https://github.com/tpope/vim-surround

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Ovládání
========

.. note::

   Pro práci s obklopenými uvozovkami, závorkami a tagy je třeba byt uvnitř
   těchto obklopovačů.

Přidání obklopení
-----------------

* Visual mód + ``S`` + uvozovka nebo závorka nebo tag

  * přidej uvozovky nebo závorky nebo tagy na označený text::

       Hello world!

       vis"

       "Hello world!"

  * lze použít všechny tři způsoby Visual módu (``v``, ``V``, ``CTRL + v``)

Změna obklopení
---------------

* ``cs`` + stará uvozovka nebo závorka + nová uvozovka nebo závorka nebo tag

  * změn staré uvozovky nebo závorky na nové uvozovky nebo závorky nebo tagy::

       "Hello world!"

       cs"'

       'Hello world!'

       cs')

       (Hello world!)

       cs)<p>

       <p>Hello world!</p>

* ``cst`` + nová uvozovka nebo závorka nebo tag

  * změn tag na uvozovky nebo závorky nebo jiný tag::

       <p>Hello world!</p>

       cst"

       "Hello world!"

* ``cs`` + číslo + ``t`` + nová uvozovka nebo závorka nebo tag

  * změn Ntý tag v pořádí na uvozovky nebo závorky nebo jiný tag::

       <div><p>Hello world!</p></div>

       cs2t<section>

       <section><p>Hello world!</p></section>

* ``cS`` + stará uvozovka nebo závorka + nová uvozovka nebo závorka nebo tag

  * změn staré uvozovky nebo závorky na nové uvozovky nebo závorky nebo tagy,
    přičemž toto nové obklíčení bude zvlášť na řadcích::

       "Hello world!"

       cS"<p>

       <p>
       Hello world!
       </p>

Klasický Vim:

   * ``ci`` + uvozovka nebo závorka

     * přepiš text uvnitř uvozovek nebo závorek::

          (Hello world!)

          ci)

          ()

   * ``ca`` + uvozovka nebo závorka

     * přepiš text uvnitř uvozovek nebo závorek a i samotné uvozovky nebo
       závroky::

          (Hello world!)

          ca)

Odstranění obklopení
--------------------

* ``ds`` + uvozovka nebo závorka

  * odstraň nejbližší uvozovky nebo závorky::

       "Hello world!"

       ds"

       Hello world!

* ``dst``

  * odstraň nejbližší tag::

       <div><p>Hello world!</p></div>

       dst

       Hello world!

* ``ds`` + číslo + ``t``

  * odstraň Ntý tag v pořádí::

       <div><p>Hello world!</p></div>

       ds2t

       <p>Hello world!</p>

Klasický Vim:

   * ``di`` + uvozovka nebo závorka

     * smaž text uvnitř uvozovek nebo závorek::

          (Hello world!)

          di)

          ()

   * ``da`` + uvozovka nebo závorka

     * smaž text uvnitř uvozovek nebo závorek a i samotné uvozovky nebo
       závorky::

          (Hello world!)

          da)
