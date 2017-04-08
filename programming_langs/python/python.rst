========
 Python
========
------------------------------------------------------
 Jednoduchý programovací jazyk se všeobecným využítím
------------------------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:Licence: CC BY-SA 4.0

:Abstract:

   `Python`_ je interpretovaný programovací jazyk, který se překládá až za běhu
   programu. Vytvořil jej v roce 1991 Guido van Rossum. Jeho hlavní filosofií
   je, aby byl kód dobře čitelný.

   Mezi jeho další vlastnostní patří, že je dynamicky typovaný (sám si zjistí,
   zda je hodnota číslo a podle toho alokuje pamět), a podporuje mnoho
   programovacích paradigmat (jak se má strukturovat a psát kód).

   Jeho silnou doménou je také velká standardní knihovna spolu s externími
   baličky snad na všechno, co by programátor mohl potřebovat pro práci. Díky
   své jednoduchosti se hodně vyučuje i v akademické sféře pro začínající
   programátory.

   Existuje taktéž někokolik odnoží, jako je Cython (kombinace s C a C++), PyPy
   (o něco rychlejší běh programu) či MicroPython (využítí v Pythonu v
   jednodeskových počítačích). Důležité je vědět, že hlavní implemtace Pythonu
   běží přes CPython interpret.

   Poslední hlavní verze je č. 3 s vedlejší verzí 3.6.

.. contents:: Obsah

Instalace
=========

Defaultně v Ubuntu je už Python nainstalovaný. Stačí ověřit příkazem::

   $ python3 --version

Tento příkaz by měl vrátit / zobrazit řádek s aktulní verzí::

   Python 3.5.2+

První program
=============

Pro napsaní a spuštení prvního programů existují dva způsoby, jak toho docílit:

1. pomocí konzole / interpretu
2. pomocí souboru / skriptu

Interpret
---------

Je interaktivní konzole, kde se okamžitě vykonávájí příkazy řádek po řádků. Lze
ji spustit příkazem::

   $ python3

   # nebo taktéž:

   $ python3.5

Po spuštění by se měl zobrazit následující text::

   Python 3.5.2+ (default, Sep 22 2016, 12:18:14)
   [GCC 6.2.0 20160927] on linux
   Type "help", "copyright", "credits" or "license" for more information.
   >>>

Pro vykonání našeho prvního příkazu (programu) je třeba napsat na řádek s ">>>"
znaky následující kód::

   >>> print("Hello world!")

a následně stiknout klávesu ENTER pro exekuci tohoto kódu. Interpret by měl
vypsat na další řádek následující text::

   Hello world!
   >>>

Konzola se ukončí / vypne buď klávesovou zkratkou CTRL + D nebo příkazem::

   quit()

Výhody a nevýhody interpreteru
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Výhody:

* okamžitá exekuce kódu (nemusím kód nejdřívě ukládat do souboru a až pak ho
  spouštět)
* vhodný pro rychlé otestování zamýšleného kódu (ověřím si, jestli se program
  chová tak, jak očekávám) ještě předtím, než se natvrdo napíše do souboru

Nevýhody:

* kód nelze znovupoužít po vypnutí konzole (musím jej znovu napsat)
* nemohu jen tak vložit nějaký víceřádkový zkopírovaný kód a spustit ho
  (musím vypsat řádek po řádku)

Skript
------

Je varianta, kdy se kód nejprve uloží do souboru (znovupoužitelnost) a až pak
se teprvé spustí. Soubory s Python kódem mají koncovku ".py". Pro ukázku,
vytvořme soubor "hello.py" a vněm mějme kód::

   print("Hello world!")

Kód v tomto souboru pak spustím příkazem::

   $ python3 hello.py

Měl bych opět výstup s textem::

   Hello wordl!

Aby se soubor dal plně kvalifikovat jako "skript", je třeba na začátek souboru
napsat tento text::

   #!/usr/bin/env python3

   print("Hello world!")

.. note::

   Prázdné řádky v souboru Python ignoruje (přeskakuje) při exekucí kódu.

Dále ještě jej označit jako spustitelný soubor (je třeba mít alespoň základní
znalost Unixu / Linuxu)::

   $ chmod +x hello.py

Nyní půjde tento soubor / skript sputit zkráceně pomocí příkazu::

   $ ./hello.py

.. note::

   Na základě hlavičky (onen první řádek v souboru) bude systém vědět, že má
   tento soubor spustit pomocí Pythonu.

.. tip::

   Do budoucna, pokud budu mít v adresáři více Python souborů (kódy jsou
   přehledně rozloženy zvlášť do souborů a mezi sebou importovány), tak onu
   hlavičku použiju jen u toho souboru, který je spoušťen přímo (jako skript).

Výhody a nevýhody skriptu
^^^^^^^^^^^^^^^^^^^^^^^^^

Výhody:

* kód je uložený v souboru na disku, tak jej mohu kdykoliv znovu spustit
* mohu lehce vložit (záleží relativně na editoru) zkopírovaný víceřádkový kód
* pokud používám chytrý textový / grafický editor, tak mohu být varován, že
  nějaké části kódu je něco špatně

Nevýhody:

* žádné mne nenapadají

Základní syntaxe
================

.. note::

   Pokud příklady níže v textu mají na začátku řádku ">>> ", tak jsou
   považovány, jako by se spouštěli v interpreteru.

Komentáře
---------

Alias vlastní poznámky / vysvětlivky v kódu, které budou při exekuci kódu
ignorovány. Pravdivost tohoto tvrzení si mohu ověřit, pokud napíšu kód::

   # Hello Python.

   print("Hello world!")

Po spuštění tohoto kódu bude skutečně vidět jen text "Hello world!" a nikoliv
i "Hello Python.".

.. tip::

   Komentáře se zpravidla používájí tam, kde je třeba vysvětlit, proč byl
   vybrán takový postup / algoritmus a nikoliv, co ten algoritmus má dělat.

   Typický příklad špatného komentáře je::

      print("Hello world!")  # Zobraz uživateli text "Hello world!".

   Kód zpravidla čte někdo, kdo už v Pythonu něco umí a tudíž mu bude zřejmé i
   bez komentáře za printem, co ten řádek má udělat.

   Pokud vysvětlení algoritmu vyžaduje delší text, než kolik se vejde na řádek
   (doporučená maximální délka je 79 znaků), tak není problém opět řádek
   začít se znakem mřížky::

      # Toto je první řádek popisku algoritmu,
      # který se nachází pod tímto komentářem
      # namísto třech teček.

      ...

Proměnné
--------

Tak jako v matematice, tak i v programování lze ukládat hodnoty do proměnných::

   x = 1
   y = 4

Přepisovat je::

   x = 1
   x = 2
   x = 3

Odkazovat na obsah jiné proměnné::

   x = 5
   y = x

.. tip::

   Přehazování hodnot mezi dvěmi různými proměnnými::

      >>> x = 0
      >>> y = 1
      >>> x, y = y, x
      >>> x
      1
      >>> y
      0

   Pozor, v souborech nelze takto lehce zobrazit obsah proměnné, pouze v
   interpreteru, pokud napíšu název proměnné / konstanty. U skriptů musím
   obsah zobrazovat pomocí funkce "print"::

      x = 1
      print(x)

Pokud se hodnota nějaké proměnné nebude vůbec měnit, tak se nejedná již o
proměnnou, ale o konstantu::

   PI = 3.141592653589793

.. note::

   Bystřejší lidé si již všimli, že zatímco proměnné jsou pojmenované malými
   písmeny, tak konstanty naopak velkými. Další konvencí v Pythonu je
   používat podtržítka, pokud je název proměnné / konstanty delší::

      favorite_programming_language = "Python"
      FAVORITE_PROGRAMMING_LANGUAGE = "Python"

Doporučení do budoucna:

1. používat rozumné názvy proměnných / konstant, aby jiný člověk, který bude
   číst kód, věděl o správném významu
2. používat anglické pojmenování proměnných / konstant, zejména pokud bude
   náš kód číst někdo cizí, kdo nerozumí češtině (angličtina je hlavní
   dorozumivací jazyk i v programování)

Rezervovaná klíčová slova
^^^^^^^^^^^^^^^^^^^^^^^^^

Názvy proměnných, konstant, ale do budoucna i dalších objektů (vlastní funkce
aj.) nesmít obsahovat tyto názvy::

   False               def                 if                  raise
   None                del                 import              return
   True                elif                in                  try
   and                 else                is                  while
   as                  except              lambda              with
   assert              finally             nonlocal            yield
   break               for                 not
   class               from                or
   continue            global              pass

Pokud nedopatřaním pojmenují např. proměnnou s klíčovým slovem "pass" a budu
ji chtít příradit hodnotu "2", tak program zahlásí chybu::

   >>> pass = 2
     File "<stdin>", line 1
       pass = 2
            ^
   SyntaxError: invalid syntax

Z této chybové hlášky lze vyčíst, že se jedná o kategorii "SyntaxError" se
zprávou "invalid syntax" a že se chyba nachází na první řádku v prostoru
se znaménkem "=".

.. note::

   Pokud spustím program, ve které se vyskytuje chyba, tak se v tomto místě
   program ukončí a zbytek kódu nebude vůbec exekutuován.

Typy hodnot
^^^^^^^^^^^

Přesnějí datové typy, kterých může nabývat hodnota v proměnných či konstant. Ty
nejzákladnější jsou:

Čísla:

* int (integer)

  * celá čísla::

       x = 123456789
       y = -5

* float

  * desetinná čísla::

      x = 3.14

* bool (boolean)

  * hodnoty s pravdou (1) a nepravdou (0)::

      x = True
      y = False

Řetězce:

* str (string):

  * posloupnost znaků (písmena, čísla, symboly, interpunkční znaménka aj.)::

       >>> day_of_week = "Today is Monday."
       >>> print(day_of_week)
       Today is Monday.

    .. note::

       Pokud potřebuji uvnitř řetězce použít dvojité uvozovky, tak musím
       řetězce na krajích označit jednoduchými uvozkami a naopak::

          a = 'Někdo řekl: "Stůj!".'
          b = "Někdo řekl: 'Stůj!'."

       Bez těchto opačných uvozovek v řetězci záhlasí syntaxtickou chybu::

          >>> print("Někdo řekl: "Stůj!".")
            File "<stdin>", line 1
              print("Někdo řekl: "Stůj!".")
                                     ^
          SyntaxError: invalid syntax

       Další možnost využítí tzv. escapování, tedy použítí speciálních znaků,
       které se ve finalé převedou na námi požadovaný znak. V rámci uvozovek
       by to bylo::

          >>> print("Někdo řekl: \"Stůj!\"")
          Někdo řekl: "Stůj!".

       Další základní escapovací znaky jsou:

       * \\

         * vložení zpětného lomítka do řetězce::

              >>> print("\\")
              \

         * bez vložení druhého lomítka by si Python myslel, že chci použít
           escapování pro dvojité uvozovky, avšak jednalo by se o neplatný
           řetězec, nebo chybí uvozovka na konci::

              >>> print("\")
                File "<stdin>", line 1
                  print("\")
                           ^
              SyntaxError: EOL while scanning string literal

       * \n

         * zalomení řádku::

              >>> print("První řádek.\nDruhý řádek.")
              První řádek.
              Druhý řádek.

       * \t

         * vložení tabulátoru::

              >>> print("1\t2")
              1       2

       Pro vypnutí chování těchto speciálních znaků je třeba před řetězec
       napsat preffix "r"::

          >>> print(r"První řádek.\nDruhý řádek")
          První řádek.\nDruhý řádek.

Sekvence:

* list

  * neuspořádáný (neseřazený) seznam prvků (můžou se i opakovat)::

       car = ["Audi", "BMW", "Citroen", "Dacia"]

Slovník:

* dict (dictionary)

  * neuspořádané páry hodnot::

       person = {
           "first_name": "Davie",
           "last_name": "Badger",
           "sex": "male
       }

    .. note::

       V Pythonu se používá pro odsazení 4 mezery (v chytrých editorech lze
       nastavit, aby po stisknutí tabulátoru se přemenil tabulátor na 4
       mezery).

Množina:

* set

  * neuspořádána kolekce prvků::

       x = {1, 2, 3}

    .. note::

       Pokud se v množině nacházejí duplicitní prvky, tak se odstraní::

          >>> x = {1, 1}
          >>> x
          {1}

Nezařaditelné:

* NoneType

  * prázdná hodnota (nic neobsahuje)::

    >>> x = None
    >>> x
    >>>

Operátory
---------

Aritmetické
^^^^^^^^^^^

Z Python interpretu si lze také udělat kalkulačku, pokud použiju správné
znaménka:

* sčítání::

     >>> 1 + 1
     2
     >>> x = 1
     >>> y = 1
     >>> x + y
     2

* odčítání::

     >>> 10 - 5
     5

* násobení::

     >>> 2 * 2
     4
     >>> print("2 x 2 je", 2 * 2)
     2 x 2 je 4
     >>> x = 2 * 2
     >>> print("2 x 2 je", x)
     2 x 2 je 4

  .. note::

     Do funkce "print" mohu zadat více hodnot (správně se říka argumenty),
     pokud je oddělím čárkou. Python si sám doplní mezeru mezi nimi.

     Taktéž lze zadat jen jedním argumentem, nicméně musím převést výsledek
     převést na řetězec pomocí funkce "str" a tyto dva řetězce spojit::

        >>> print("2 x 2 je " + str(2 * 2))
        2 x 2 je 4
        >>> str(2 * 2)
        '4'

     Pokud budu chtít sečíst dva různé datové typy, tak Python zahlásí typovou
     chybu::

        >>> 1 + "a"
        Traceback (most recent call last):
          File "<stdin>", line 1, in <module>
        TypeError: unsupported operand type(s) for +: 'int' and 'str'

     Něco jiného už ale bude, pokud budu chtít nějaký řetězec vynásobit celým
     číslem::

        >>> 3 * "bla"
        blablabla

* umocnění::

     >>> 2 ** 3
     8

* dělení::

     >>> 4 / 2
     2.0

  .. note::

     Python po klasickém dělení vrátí vždy desetinné číslo, i kdyby se jednalo
     o dvě celá čísla jako v předchozím případě.

     Pro převední výsledku zpět na celé číslo se volá funkce "int"::

        >>> int(4 / 2)
        2
        >>> x = 4 / 2
        >>> int(x)
        2

     Zpět na desetinné číslo by to bylo přes funkci "float"::

        >>> float(2)
        2.0
        >>> float(int(4 / 2))
        2.0

* celočíselné dělení::

     >>> 4 // 3
     1

* zbytek po dělení::

     >>> 4 // 3
     0

  .. note::

     Pokud zbytek po dělení je nula, tak se jedná o sudé číslo, jinak o liché.

U výpočtů mohu také použít klasické závorky pro dávání přednosti::

   >>> (10 + 2) / 3 + 2
   6.0

Pořadí operací je vyhodnocováno stejně jako v matematice, tj.:

1. závorky
2. umocňování

   * zde pozor na vícenásobné umocňování, kde postupuje obráceně zprava
     doleva::

        >>> 2 ** 3 ** 2
        512
        >>> 2 ** (3 ** 2)
        512

3. násobení a dělení
4. sčítání a odčítání

Relační
^^^^^^^

Pro zjišťování pravdivosti a nepravdivosti výrazů:

* větší::

     >>> 1 > 0
     True
     >>> 1 > 2
     False

* menší::

     >>> 1.1 < 2
     True
     >>> 2.2 < 1
     False

* větší nebo rovno::

     >>> (1 + 1) >= 1
     True

* menší nebo rovno::

     >>> x = -5
     >>> x < 0
     True

* rovná se::

     >>> 1 == 1
     True
     >>> 1 == 1.0
     True

* nerovná se::

     >>> x = "a"
     >>> y = "b"
     >>> x != y
     True

Logické
^^^^^^^

Pro spojování více výrazů s relačními operátory:

* a

  * oba výrazy musí být pravdivé (může jich být i více za sebou)::

     >>> 1 == 1 and 2 == 2
     True

* nebo

  * stačí, aby alespoň jeden výraz byl pravdivý::

     >>> 0 != 0 and 1 > 0
     True

Množinové
^^^^^^^^^

* sjednocení

  * spojení všech prvků v obou množinách::

     >>> {1, 2} | {3}
     {1, 2, 3}

* průnik

  * společné prvky v obou množinách::

     >>> {1, 2} & {1}
     {1}

* rozdíl

  * prvky, které se nenacházejí v druhé množině::

     >>> {1, 2} - {1}
     {2}

* doplněk

  * přebytečné prvky, které jsou jen v množině A a v B už ne::

     >>> {1, 2, 3} ^ {1}
     {2, 3}

TODO
====

* help() v interpreteru
* patička u skriptů spolu s main() funkcí, kde je return s nulou::

     if __name__ == "__main__":
        sys.exit(main())

* datové typy bytes, bytearray, memoryview, complex čísla, frozenset, tuple,
  mutable vs immutable
* převody datových typů (zatím jen int, float, str)
* zkrácené zápisy operátoru, např v rámci cyklů::

     x = x + 1
     x += 1

* idiomatické relační operátory (in, is) ukázat u podmínek
* víceřádkové řetězce
* not u podmínek
* zalomení řádku pří dlouhém kódu

.. _Python: https://en.wikipedia.org/wiki/Python_(programming_language)
