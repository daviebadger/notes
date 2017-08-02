=======
 Emmet
=======
----------------------
 Expanze HTML zkratek
----------------------

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

   Plug 'mattn/emmet-vim'

Ovládání
========

Vytvoření kostry dokumentu
--------------------------

* ``html:5`` + ``<C-Y>,``

  * vlož kostru HTML 5 dokumentu::

       html:5

       <!DOCTYPE html>
       <html lang="en">
       <head>
         <meta charset="UTF-8">
         <title></title>
       </head>
       <body>

       </body>
       </html>

Tvorba tagů
-----------

* ``<C-Y>,``

  * vytvoř tag(y) z dané zkratky::

       div>ul>li.foo.bar.baz#$*3

       <div>
         <ul>
           <li id="1" class="foo bar baz"></li>
           <li id="2" class="foo bar baz"></li>
           <li id="3" class="foo bar baz"></li>
         </ul>
       </div>

Odbočka k Emmet zkratkám
^^^^^^^^^^^^^^^^^^^^^^^^

Elementy
""""""""

Vytvoř z názvu elementu tag::

   p    ->   <p></p>
   br   ->   <br>
   a    ->   <a href=""></a>

Vnoření elementů
""""""""""""""""

* ``>``

  * vlož vnořený element::

       ul>li

       <ul>
         <li></li>
       </ul>

* ``+``

  * vlož sourozenecký element::

       p+p

       <p></p>
       <p></p>

* ``^``

  * vrať se o úroveň výš pro vložení dalšího elementu::

       p>span^p

       <p><span></span></p>
       <p></p>

* ``*``

  * vlož N-krát element::

       ul>li*3>a

       <ul>
         <li><a href=""></a></li>
         <li><a href=""></a></li>
         <li><a href=""></a></li>
       </ul>

* ``()``

  * seskup elementy::

       div>(header>ul>li*2>a)+footer>p

       <div>
         <header>
           <ul>
             <li><a href=""></a></li>
             <li><a href=""></a></li>
           </ul>
         </header>
         <footer>
           <p></p>
         </footer>
       </div>

Atributy elementů
"""""""""""""""""

* ``#``

  * vlož ID atribut (může být jen jednou)::

       div#foo

       <div id="foo"></div>

* ``.``

  * vlož class atribut (může být několikrát)::

       div#id.foo.bar.baz

       <div id="id" class="foo bar baz"></div>

* ``[]``

  * vlož vlastní atributy s / bez hodnot::

       input[type=submit value]

       <input type="submit" value="">

* ``$``

  * vlož do elementu dynamicky čísla::

       ul>li#item_$$$@*3

       <ul>
          <li id="item_001"></li>
          <li id="item_002"></li>
          <li id="item_003"></li>
       </ul>

.. tip::

   Pomocí kombinace ``$`` a ``@`` lze změnit směr počítání čísel nebo začátek
   prvního čísla::

      ul>li#item_$@-*3

      <ul>
         <li id="item_3"></li>
         <li id="item_2"></li>
         <li id="item_1"></li>
      </ul>

      ul>li#item_$@3*3

      <ul>
         <li id="item_3"></li>
         <li id="item_4"></li>
         <li id="item_5"></li>
      </ul>

Text elementu
"""""""""""""

* ``{}``

  * vlož dovnitř elementu obsah daného textu::

       p{John Doe}

       <p>John Doe</p>

Generování náhodných slov
-------------------------

* ``lorem`` + ``<C-Y>,``

  * vlož náhodný text o délce 30 slov::

       p>lorem

       <p>
          Ipsum officia nihil amet nostrum qui corrupti? Ex expedita quia
          eaque saepe tempore harum Repellendus ducimus itaque nisi illo quam
          Nulla neque similique exercitationem quasi repellat? Provident
          perferendis accusantium vel.
       </p>

.. tip::

   Vlož náhodný text s konkrétním počtem slov::

      ul>li*3>lorem1

      <ul>
         <li>Dolor.</li>
         <li>Ipsum</li>
         <li>Adipisicing.</li>
      </ul>

Aktualizace tagů
----------------

* ``<C-Y>u``

  * aktualizuj daný tag::

       <p>test</p>

       <p id="test">test</p>

.. note::

   Pro aktualizaci tagu je třeba být s kurzorem v místě tagu.

.. tip::

   Pokud nějakému tagu chybí hodnota v atributu nebo samotný obsah tagu, lze
   na toto místo skočit pomocí ``<C-Y>n``, respektive zpětně ``<C-Y>N``.

Označení tagů
-------------

* ``<C-Y>d``

  *

Odstranění tagů
---------------

* ``<C-Y>k``

  * odstraň daný tag::

       <li><a href=""></a></li>

       <li></li>

Zakomentování tagů
------------------

* ``<C-Y>/``

  * zakomentuj / odkumentuj daný tag::

       <div class="foo"></div>

       <!-- <div class="foo"></div> -->
