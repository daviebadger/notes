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
        <figcaption>Tux logo</figcaption>
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

.. note::

   Buňky v tabulce jdou spojit:

   * horizontálně pomocí ``colspan`` atributu::

        <table>
          <tr>
            <th colspan="2">Jméno</th>
          </tr>
          <tr>
            <td>Davie</td>
            <td>Badger</td>
          </tr>
        </table>

   * vertikálně pomocí ``rowspan`` atributu::

        <table>
          <tr>
            <th rowspan="2">Jméno</th>
            <td>Davie</td>
          </tr>
          <tr>
            <td>Badger</td>
          </tr>
        </table>

.. tip::

   Tabulka s viditelným popiskem nad tabulkou::

      <table>
        <caption>Tabulka</caption>

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

Data v HTML hlavičce, které se nezobrazí uživateli, ale jsou vhodná pro
prohlížeče a vyhledávače:

* kódování stránky::

     <meta charset="UTF-8">

* název stránky v záložce prohlížeče::

     <title>Test</title>

* popisek stránky ve vyhledávači::

     <meta name="description" content="Bla bla bla">

* ikonka webu v záložce prohlížeče (favicon)::

     <link rel="shortcut icon" href="favicon.ico">

.. note::

   Favicon je zpravidla obrázek s přejmenovanou koncovkou na ``.ico``.

.. tip::

   V hlavičce lze také nastavit přízpůsobení stránky pro mobilní zařízení::

      <meta name="viewport" content="width=device-width, initial-scale=1">

Styly
-----

Pomocí kaskádových stylů (CSS) jde upravit vzhled tagů::

   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <title>Styly</title>

     <style>
     p {
       color: green;
     }
     </style>
   </head>
   <body>
     <p>Test stylu</p>
   </body>
   </html>

Kromě nanesení stylů na tagy jako takové lze uplatnit pomocné identifikátory:

* id

  * aplikuj styl jen na ten tag, který obsahuje ``id`` atribut::

      <style>
      #test-me {
        color: green;
      }
      </style>

      <p id="test-me">Test stylu<p>

* class

  * aplikuj styl na všechny tagy, které obsahují ``class`` atribut::

      <style>
      .background {
        background: black;
      }
      .color {
        color: white;
      }
      </style>

      <h1 class="background color">Nadpis</p>
      <p class="background color">Odstavec</p>

.. note::

   Styly se zpravidla nacházejí zvlášť v css souborech, na které jsou posléze
   vedeny odkazy v hlavičce::

      <head>
        <link rel="stylesheet" href="styles.css">
      </head>

Skripty
-------

Pomocí Javascriptu jde nastavit chování webu::

   <script>
   console.log("Hello World!");
   </script>

.. note::

   Javascriptový kód se taktéž může nacházet zvlášť v js souborech, na
   které lze odkazovat::

      <script src="index.js"></script>

.. tip::

   Skripty se zpravidla umísťují na konec HTML dokumentu pro urychlení
   zobrazení (vyrendrování) stránky::

      <body>
        <h1>Nadpis</h1>

        <script src="index.js"></script>
      </body>

   Pokud Javascriptový kód nezbytný pro správné zobrazení stránky, lze jej
   umístit i do hlavičky::

      <head>
        <script src="index.js"></script>
      </head>

TODO
====

* entity (&lt) -> https://www.w3schools.com/html/html_entities.asp
* symboly (&copy;) -> https://www.w3schools.com/html/html_symbols.asp
