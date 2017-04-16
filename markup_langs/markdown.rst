==========
 Markdown
==========
----------------------------------------------------------------------
 Jednoduchý textový formát pro psání poznámek, článků, prezentací aj.
----------------------------------------------------------------------

:Abstract:

   `Markdown`_ (zkráceně MD) vznikl v roce 2004 s cílem vytvořit takový
   formát, který by byl jednoduchý pro jak pro psaní, tak i čtení. Vytvořil
   ho John Gruber.

   Tento formát se začal masivně používat v diskusních příspěvcích na
   stránkách jako jsou `Github`_, `StackOverflow`_ či `Reddit`_. Na tento
   módní trend navázalo několik nástrojů, které umožňují použít Markdown
   pro psání článků (včetně primitivního webu), technické dokumentace nebo
   knih.

   Nevýhody Markdownu:

   1. nabizí jen základní formátování textu (bez použití různých rozšíření)
   2. není přesně definována, respektiva standardizována syntaxe

   O standardizaci tohoto jazyka se snaží skupina lidí z výše uvedených
   stránek pod značkou `CommonMark`_.

   Markdown (respektive CommonMark) lze vyzkoušet online na stránce
   http://spec.commonmark.org/dingus/.

.. contents:: Obsah

Formátování textu
=================

Text s Markdown značkami se píše do souboru s koncovkou ".md".

Nadpisy
-------

Pro označení nadpisů se používá mřížka "#"::

   # Nadpis první úrovně
   ## Nadpis druhé úrovně
   ### Nadpis třetí úrovně
   #### Nadpis čtvrté úrovně
   ##### Nadpis páté úrovně
   ###### Nadpis šesté úrovně

Za mřížkou vždy následuje mezera a až pak samotný nadpis. Pod nadpisem se
pak vkládá prázdný řádek.

Příklad se dvěmi nadpisy za sebou::

   # Titulek

   ## Úvod

   Blabla.

.. note::

   Nadpis první a druhé úrovně (více už ne) lze zapsat jako v reStructuredTextu
   a to jako::

      Nadpis první úrovně
      ===================

      Nadpis druhé úrovně
      -------------------

Odstavce
--------

Klasika, jeden souvislý text přes několik řádků::

   Toto je první odstavec.

   Toto je druhý odstavec.

Mezi odstavce se standardně vkládá jeden prázdný řáddek pro oddělení. Pokud
by tam nebyl, tak při konverzi do HTML budou obě věty vedle sebe (jeden
odstavec).

Pro potřeby zalomení textu je třeba použít na koncí řádku zpětné lomítko nebo
dvě mezery::

   Toto je první řádek. \
   Toto je druhý řádek

   Toto je první řádek.-- (místo -- budou dvě mezery)
   Toto je druhý řádek.

.. note::

   V GitHubu nefunguje zpětně lomítko, jen dvě tečky pro zalámování řádku.

Zvýraznění textu
----------------

Markdown v základní verzi bez rozšiřujích doplňků podporuje jen kurzívu a
tučné písmo.

1. kurzíva

   * na kraj slova / textu je třeba vložit hvězdičky "*" nebo podtržítka "_"::

        *kurzíva* nebo _text kurzívou_

2. tučné písmo

   * zde to budou už dvě hvězdičky nebo dvě podtržítka::

        **tučné** nebo **text tučným písmem**

Pro kombinaci obou zvýraznění se nejdříve použije označení pro tučné písmo
pomocí dvou hvězdiček a uvnitř jedno podtržítko pro kurzívu::

   **_text kurzívou a tučným písmem_**

.. tip::

   Pokud text vyžaduje podtržítko nebo hvězdičku a já ho nechci zvýrazňovat,
   tak musím před tyto znaky použít zpětné lomítko pro deaktivaci::

      \*Toto není text kurzívou. Hvězdička na začátku řádku půjde normálně
      vidět.

Seznamy
-------

Neseřazené
^^^^^^^^^^

Na výběr je několik znaků, pomocí kterých lze značít neseřazené seznamy. Jedná
se o hvězdičku "*", plusko "+" a pomlčku "-". Nejpoužívanější se zdá být
hvězdička::

   * ananas
   * banán
   * citrón

   + Audi
   + BMW
   + Citroen

   - Praha
   - Brno
   - Ostrava

Seznamy lze samozřejmě vnořovat (není třeba střídat označení). Velikost
odsazení je buď čtyři mezery nebo jeden tabulátor::

   * ananas
       + Audi

Dovnitř vnořených seznamů lze taktéž vkládat odstavce či blokové citace.
Principiálně se používá stejná velikost odsazení::

   - Praha

       To je hlavní město.

V případě vkládání zdrojových kódů bez označení jazyka je třeba použít osm
mezer nebo dva tabulátory::

   * ananas

           import time

           print(time.time())

To ovšem neplatí pro blok schovaný v "```" znacích::

   * ananas

       ```python
       import time

       print(time.time())
       ```

Číslované
^^^^^^^^^

Jako označení se používá převážně tečka "." nebo i zavírající závorka ")" za
čísly::

   1. jedna
   2. dva
   3. tři

   1) one
   2) two
   3) three

Číselné a neseřazené seznamy lze navzájem kombinovat::

   1. jedna
       - a
       - b
       - c
   2. dva

Odkazy
------

Existují dva způsoby značení:

1. mít odkaz v textu::

      Klikni na odkaz [ZDE](https://github.com).

2. odkázat na odkaz na konci souboru::

      Klikni na odkaz [ZDE][github]

      [github]: https://github.com

V obou variantách uživatel uvidí odkaz schovaný v textu "ZDE".

Výhodou druhé varianty je, že stejný odkaz (proměnnou) lze použít několikrát
v textu. Jako název proměnné lze použít i čísla (indexy).

Obrázky
-------

Tvoří se úplně stejně jako odkazy, jen se použije na začátku vykričník "!"::

   ![ZDE](https://example.org/noname.jpg)

   ![ZDE](obrázek)
   .
   .
   .
   ![obrázek]: https://example.org/noname.jpg)

Obrázky s formátem "jpg", "png" či "gif" by měli v pořádku fungovat.

Citace
------

Citovaný text se značí znakem ">" na začátku řádku::

   > Cituji text od člověka X.

Pokud potřebuji citovat delší text s odstavcemi, tak místo prázdného řádku
mezi odstavci bude znak ">"::

   > Toto je první citovaný odstavec.
   >
   > Toto je druhý citovaný odstavec.

Dělící čára
-----------

Alias horizontální čára se vkládá pomocí tří pomlček za sebou "---" nebo
taktéž hvězdiček::

   Toto je text před dělící čárou.

   ---

   Toto je text za pomlčekovou dělící čárou.

   ***

   Toto je text na hvězdičkovou dělící čárou.

Zdrojové kódy
-------------

1. jednořádkové

   * kód je uvnitř textu a značí na se kraji zpětnou jednoduchou uvozovkou::

        Stiskni klávesovou zkratku `CTRL + LSHIFT + V`.

2. víceřádkové

   * jak už název napovídá, jedná o se kód přes několik řádků
   * zde je na výběr se dvou značení:

     a) bez zvýraznění syntaxe, pokud se jedná o programovací / značkovací
        jazyk::

           ....Toto je zdrojový text, který musí být odsazen čtyřmi mezerami
           ....(místo těch teček tady vlevo) nebo jedním tabulátorem.

     b) se zvýrazněním syntaxe::

           ```python
           import time

           print(time.time())
           ```

.. note::

   Uvnitř zdrojového textu budou jakékoliv Markdown značky nefunkční.

.. _Markdown: https://en.wikipedia.org/wiki/Markdown
.. _GitHub: https://github.com/
.. _StackOverflow: http://stackoverflow.com/
.. _Reddit: https://www.reddit.com/
