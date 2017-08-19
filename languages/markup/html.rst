======
 HTML
======
----------------------------------------------------
 Značkový jazyk pro tvorbu webových stránek (.html)
----------------------------------------------------

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

Vlož SVG obrázek::

   <svg height="100" width="100">
     <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
     Sorry, your browser does not support inline SVG.
   </svg>

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

Sémantické tagy
---------------

Tagy pro lepší rozvržení webu do logických celků:

* header

  * hlavička webu, zpravidla s navigací::

       <header>
         <nav>
           <ul>
             <li><a href="#1">jedna</a></li>
             <li><a href="#2">dva</a></li>
             <li><a href="#3">tři</a></li>
           </ul>
         </nav>
       </header>

* nav

  * navigace webu

* main

  * hlavní část webu mezi hlavičkou (header) a zápatím (footer)

* section

  * označení části webu, zpravidla lišta s informacemi::

      <section>
        <h2>info</h2>
        <p>info o infu</p>
        <img src="image.jpg" alt="image">
      </section>

* article

  * označení článku::

       <article>
         <p>článek</p>
       </article>

* aside

  * postranní panel, zpravidla navigace vedle článku (nutno nastylovat pomocí
    CSS, aby se skutečně šel vidět panel vlevo / vpravo od článku)

* footer

  * patička webu::

       <footer>
         <p>&copy; Davie Badger</p>
       </footer>

.. note::

   Znaky mimo klávesnici je třeba zakódovat::

      &copy; (ikonka copyrightu)
      &reg; (ikonka registrované značky)

   To samé platí i pro rezervované znaky v HTML::

      > -> &gt; nebo &#62;
      < -> &lt; nebo &#60;

.. tip::

   Nesémantické pomocné tagy:

   * div

     * pro zaobalení tagů, na které lze aplikovat pomocí CSS další styly::

          <style>
          div {
            border: 3px solid black;
            font-size: 22px;
          }
          </style>

          <div>
            <h1>nadpis</h1>
            <p>test</p>
          </div>

   * span

     * pro zaobalení části textu v odstacích, na které lze taktéž aplikovat
       styly::

          <style>
          p {
            color: black;
          }

          #first-name {
            color: red;
          }
          </style>

          <p>
            <span id="first-name">Davie</span>
            Badger
          </p>

Formuláře
---------

Vytvoř přihlašovací formulář::

   <form action="/user/login" method="POST">
     <label for="email">Email:</label>
     <input type="email" id="email" name="email">

     <label for="password">Password:</label>
     <input type="password" id="password" name="password" >

     <input type="submit" value="Přihlásit se">
   </form>

Legenda:

==============  ======
Syntaxe         Význam
==============  ======
action=""       URL adresa, který se má zavolat po stisknutí na submit tlačítko
method=""       HTTP metoda pro odeslání formulářových dat (GET nebo POST)
label for=""    spárování labelu (popisku) pro konkrétní input s ID atributem
input type=""   typ formulářového pole
input name=""   pojménování formulářového pole (povinné pro odesílání dat)
input value=""  hodnota v input poli
==============  ======

.. note::

   Některé inputy, např. pro email, mají defaultně vlastní validaci a styly,
   pokud je hodnota v inputu neplatná. Toto chování lze zamezit pomocí
   ``novalidate`` atributu v ``form`` tagu::

      <form novalidate></form>

.. tip::

   Zpravidla se labely a inputy dohromady zaobaolují do ``div`` či ``li``
   tagu pro lepší nastylování::

      <form action="/user/login" method="POST">
        <ul>
          <li>
            <label for="email">Email:</label>
            <input type="email" id="email" name="email">
          </li>
          <li>
            <label for="password">Password:</label>
            <input type="password" id="password" name="password" >
          </li>
        </ul>

        <input type="submit" value="Přihlásit se">
      </form>

Formulářové pole
^^^^^^^^^^^^^^^^

Typy formulářových polí:

* ``input``

  * pole pro vstup dat od uživatelovy klávesnice
  * typy vstupů:

    * ``text``

      * jednořádkový text::

           <input type="text" name="text">

      * jednořádkový text s výchozí hodnotou::

           <input type="text" name="name" value="Davie">

      * jednořákový text s popiskem uvnitř pole, který po kliknutí zmizí::

           <input type="text" name="name" placeholder="First name">

    * ``password``

      * schované heslo pomocí hvězdiček::

           <input type="password" name="password">

      * schované heslo jako povinná hodnota (uživatel musí vyplnit)::

           <input type="password" name="password" required>

    * ``email``

      * emailová adresa (na mobilu se zobrazí klávesnice se zavináčem)::

           <input type="email" name="email">

      * emailová adresa s maximálním počtem znaků::

           <input type="email" name="email" maxlength="50">

    * ``search``

      * text k vyhledání (na mobilu se přejmenuje Enter klávesa na Search)

    * ``number``

      * číslo (na mobilu se nezobrazí číselná klávesnice)::

           <input type="number" name="number">

      * číslo s minimální hodnotou::

           <input type="number" name="number" min="1">

      * číslo s maximální hodnotou::

           <input type="number" name="number" max="3">

    * ``tel``

      * telefonní číslo (na mobilu se zobrazí číselná klávesnice)

    * ``range``

      * posuvník pro čísla v rozmezí od - do::

           <input type="range" name="range" min="0" max="100">

    * ``radio``

      * kolečka pro vybrání jediné hodnoty z několika hodnot::

           <input type="radio" name="gender" value="male">
           <input type="radio" name="gender" value="female">

    * ``checkbox``

      * rámečky bez fajfky::

           <input type="checkbox" name="married">

      * rámeček s fajfkou::

           <input type="checkbox" name="married" checked>

    * ``date``

      * textové pole pro datum (na mobilu se zobrazí nativní výběrčí datumu)

    * ``datetime``
    * ``datetime-local``
    * ``time``
    * ``week``
    * ``month``
    * ``file``

      * nahrání souboru::

           <input type="file" name="cv">

      * nahrání více souborů najednou::

           <input type="file" name="receipts" multiple>

  * speciální inputy (tlačítka):

    * submit

      * pro odeslání formulářových dat::

           <input type="submit" value="Odeslat">

    * reset

      * pro vymazání / vyresetování všech hodnot ve formuláři::

           <input type="reset">

* select

  * výběr hodnoty ze seznamu::

       <select name="auta">
         <option value="audi">Audi</option>
         <option value="bmw">BMW</option>
         <option value="citroen">Citroen</option>
       </select>

  * výběr hodnoty ze seznamu s defaultní hodnotou pomocí atributu
    ``selected``::

       <select name="auta">
         <option value="audi">Audi</option>
         <option value="bmw" selected>BMW</option>
         <option value="citroen">Citroen</option>
       </select>

  * výběr hodnoty ze seskupeného seznamu::

       <select name="auta">
         <optgroup label="A-C">
           <option value="audi">Audi</option>
           <option value="bmw">BMW</option>
           <option value="citroen">Citroen</option>
         </optgroup>
         <optgroup label="O-R">
           <option value="opel">Opel</option>
           <option value="porsche">Porsche</option>
           <option value="renault">Renault</option>
         </optgroup>
       </select>

* textarea

  * multiřádkové textové pole (input je jen jednořákový) s možností nastavení
    velikosti řádků a sloupců (znaků na řádek)::

       <textarea name="text" cols="11" rows="3">
       bla bla bla
       bla bla bla
       bla bla bla
       </textarea>

.. note::

   Při práci se soubory ve formuláři je třeba přidat do ``form`` tagu atribut
   ``enctype``, aby se souboury odeslaly na server::

      <form enctype="multipart/form-data"></form>

.. tip::

   Kromě submit tlačítka existuje i obyčejný tlačítko ``button``::

      <button>klikni na mě</button>

   Rozdíly oproti submit tlačítku:

   1. lze vnořit dovnitř další tagy, např. obrázek
   2. lze použít mimo formulář
   3. po kliknutí se nic nebude dít (žádný refresh stránky jako u submitu),
      není-li použit Javascript

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

* ``id``

  * aplikuj styl jen na ten tag, který obsahuje ``id`` atribut::

      <style>
      #test-me {
        color: green;
      }
      </style>

      <p id="test-me">Test stylu<p>

* ``class``

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

.. tip::

   Atributy ``id`` a ``class`` se zpravidla nacházejí mezi prvnímu atributy
   v tagu, za které pak následují ostatní::

      <input id="email" class="input-email" type="email" placeholder="email">

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

   Aby načtení Javascriptového souboru neblokovalo vyrendrování stránky,
   lze použít následující atributy:

   * async

     * skript se spustí po jeho načtení tak, aby neblokoval rendrování::

          <script src="index.js" async></script>

   * defer

     * skript se spustí až bude kompletně celá stránka vyrendrována::

          <script src="index.js" defer></script>
