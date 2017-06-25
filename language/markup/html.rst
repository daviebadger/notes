======
 HTML
======
--------------------------------------------
 Značkový jazyk pro tvorbu webových stránek
--------------------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Základní značky
===============

Nadpisy
-------

Vlož nadpisy různé úrovně::

   <h1>První úroveň</h1>
   <h2>Druhá úroveň</h2>
   <h3>Třetí úroveň</h3>
   <h4>Čtvrtá úroveň</h4>
   <h5>Pátá úroveň</h5>
   <h6>Šestá úroveň</h6>

Odbočka ke struktuře dokumentu
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

HTML dokument se člení do následujících částí:

* verze dokumentu
* obsah dokumentu:

  * hlavička dokumentu (metadata)
  * tělo dokumentu

::

   <!DOCTYPE html>
   <html lang="cs">
     <head>
       <meta charset="utf-8">
       <title>Titulek dokumentu</title>
     </head>
     <body>
       <h1>Nadpis</h1>
     </body>
   </html>

Odstavce
--------

Vlož odstavce::

   <p>První odstavec</p>
   <p>Druhý odstavec</p>

.. tip::

   Je-li třeba zalomit text, použije se v místě zalomení tag ``br``::

      <p>
        První řádek<br>
        Druhý řádek<br>
        Třetí řádek
      </p>

Formátování textu
-----------------

Označ text kurzívou::

   <em>Text kurzívou.</em>

Označ text tučným písmem::

   <strong>Text tučným písmem.</strong>

.. note::

   Text kurzívou a tučným písmem zároveň::

      <em><strong>Text kurzívou a tučným písmem zároveň.</strong></em>
      <strong><em>Text kurzívou a tučným písmem zároveň.</em></strong>

.. tip::

   Označ text horním indexem::

      <sup>Horní index</sup>

   Označ text dolním indexem::

      <sub>Dolní index</sub>

Seznamy
-------

Neseřazené
^^^^^^^^^^

Vytvoř neseřazený seznam::

   <ul>
     <li>ananas</li>
     <li>banán</li>
     <li>citrón</li>
   </ul>

Vytvoř neseřazený vnořený seznam::

   <ul>
     <li>ovoce
       <ul>
         <li>ananas</li>
         <li>banán</li>
         <li>citrón</li>
       </ul>
     </li>
     <li>zelenina</li>
   </ul>

Číslované
^^^^^^^^^

Vytvoř číslovaný seznam::

   <ol>
     <li>jedna</li>
     <li>dva</li>
     <li>tři</li>
   </ol>

Vytvoř kombinaci číslovaného a neseřazeného seznamu::

   <ol>
     <li>jedna
       <ul>
         <li>a</li>
         <li>b</li>
         <li>c</li>
       </ul>
     </li>
     <li>dva</li>
   </ol>

Odkazy
------

Vlož hypertextový odkaz::

   <a href="https://google.com">Google</a>

Obrázky
-------

Vlož obrázek::

   <img src="tux.png" alt="Tux logo" width="100" height="100">

Citace
------

Vlož citaci::

   <blockquote>Citovaný text</blockquote>

Dělící horizontální čára
------------------------

Odděl text dělící horizontální čarou::

   <p>Text před dělící horizontální čarou.</p>

   <hr>

   <p>Text za dělící horizontální čarou.</p>

Zdrojové kódy
-------------

Vlož zdrojový kód::

   <pre>import this</pre>

.. note::

   V případě víceřádkové kódu je nutné vynechat odsazení uvnitř tagu, pokud
   osazení od začátku řádku není žádané::

      <pre>
      import this

      print(this)
      </pre>

Pokročilé značky
================

Komentáře
---------

Vlož komentář::

   <!-- Komentovaný text. -->

.. tip::

   Schovej tag(y) do komentáře::

      <!-- Do not display this paragraph
      <p>Schovaný text.</p>
      -->

TODO
====

* id + class selektory
