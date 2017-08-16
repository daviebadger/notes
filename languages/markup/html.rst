======
 HTML
======
--------------------------------------------
 Značkový jazyk pro tvorbu webových stránek
--------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

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

.. note::

   Pomocí ``lang`` atributu v ``html`` tagu se definuje jazyk webu. Taktéž lze
   uvést dialekt jazyka::

      <html lang="en-US"></html>

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

.. note::

   Defaultně se odkaz (stránka) otevře v aktuální záložce. Je-li třeba otevřít
   odkaz v jiné záložce, použije se ``target`` atribut s hodnotou ``_blank``::

      <a href="https://google/.com" target="_blank">Google</a>

.. tip::

   Pomocí ``#`` lze odkazovat na tag na stránce, který má v sobě atribut id::

      <p id="test"></p>

      <a href="#test">TEST</a>

   Po kliknutí na tento odkaz prohlížeč automaticky scrolluje stránku tak, aby
   byl první vidět daný tag s id.

Obrázky
-------

Vlož obrázek::

   <img src="tux.png" alt="Tux logo" width="100" height="100">

Vlož hypertextový obrázek::

   <a href="/image">
     <img src="tux.png" alt="Tux logo" width="100" height="100">
   </a>

.. note::

   Není-li uvedena výška a šířka, obrázek bude mít velikost jako v daném
   souboru. Velikost obrázku lze dodatečně nastavit (přepsat) pomocí
   kaskádových stylů (CSS).

.. tip::

   Obrázek s viditelným popiskem pod obrázkem::

      <figure>
        <img src="tux.png" alt="Tux logo" width="100" height="100">
        <figcaption>Tux logo</figcatpion>
      </figure>

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
   odsazení od začátku řádku není žádané::

      <pre>
      import this

      print(this)
      </pre>

Tabulky
-------

Vytvoř klasickou tabulku, kde první řádek je popis sloupců::

   <table>
      <tr>
         <th>Jméno</th>
         <th>Příjmení</th>
         <th>Věk</th>
      </tr>
      <tr>
         <td>Davie</td>
         <td>Badger</td>
         <td>22</td>
      </tr>
   </table>

Slovník pojmů
-------------

Vytvoř slovník pojmů::

   <dl>
      <dt>HTML</dt>
      <dd>Značkový jazyk pro tvorbu webových stránek</dd>

      <dt>Python</dt>
      <dd>Skriptovací programovací jazyk</dd>
   </dl>

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

Pomocné tagy
------------

div
span

Sémantické tagy
---------------

section
article
aside
nav

header
footer

Formuláře
---------

https://www.w3schools.com/html/html_forms.asp

Metadata
--------

https://www.w3schools.com/html/html_head.asp

Styly
-----

* id + class selektory

<style>

<link rel="stylesheet" href="styles.css">

Skripty
-------

<script src="script.js"></script>

<noscript></noscript>

TODO
====

* entity (&lt) -> https://www.w3schools.com/html/html_entities.asp
* symboly (&copy;) -> https://www.w3schools.com/html/html_symbols.asp
