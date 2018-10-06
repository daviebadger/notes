========
 Python
========
--------------------------------------
 Skriptovací programovací jazyk (.py)
--------------------------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

.. highlight:: python

Instalace
=========

Python je defaultně nainstalovaný v Ubuntu:

.. code:: none

   $ python3
   Python 3.6.2

.. note::

   Samotný příkaz ``python`` odkazuje na starou verzi:

   .. code:: none

      $ python --version
      Python 2.7.13

První program
=============

Program v Pythonu lze spustit dvěmi způsoby:

1. pomocí konzole / interaktivního shellu
2. pomocí souboru / skriptu

Interaktivní shell
------------------

Spusť interaktivní shell:

.. code:: none

   $ python3
   Python 3.6.2 (default, Aug  4 2017, 14:35:04)
   [GCC 7.1.0] on linux
   Type "help", "copyright", "credits" or "license" for more information.
   >>>

Každý řádek v shellu za ``>>>`` je okamžitě exekutován po stisknutí klávesy
``ENTER``::

   >>> print("Hello world!")
   Hello world!
   >>>

Shell lze vypnout klávesovou zkratkou ``CTRL + D`` nebo zavoláním funkce
``quit``, která funguje jen uvnitř shellu:

.. code:: none

   >>> quit()
   $

.. note::

   Při vypnutí shellu zanikne i historie použitých příkazů, není-li použít
   jiný interaktivní shell, např. `IPython`_.

   Samotnou historii příkazů v shellu lze zobrazit pomocí šipky nahoru.

.. tip::

   Uvnitř shellu lze použít klávesu ``TAB`` pro automatické dokončování slov,
   je-li to možné::

      >>> a
      abs(     all(     and      any(     as       ascii(   assert ) ) ) )

Skript
------

Spusť skript:

.. code:: none

   $ cat hello.py
   print("Hello world!")
   $ python3 hello.py
   Hello world!

.. tip::

   Skript lze spustit i jako spustitelný soubor:

   1. přidat hlavičku (shebang) na začátek souboru::

         #!/usr/bin/env python3

         print("Hello world!")

   2. přidat oprávnění pro exekuci souboru:

      .. code:: none

         $ chmod +x hello.py

   3. spustit soubor:

      .. code:: none

         $ ./hello.py
         Hello world!

Základní syntaxe
================

Komentáře
---------

Vlož komentář, který bude Pythonem ignorován při exekuci kódu:

.. code:: none

   $ cat hello.py
   # print("Hello")

   print("Hello world!")
   $ python3 hello.py
   Hello world!
   $

.. note::

   Komentáře se zpravidla používájí jen tam, kde je třeba vysvětlit úmysl,
   proč je právě použít daný kód, neboť ten nemusí být každému zřejmý při
   čtení kódu.

   V žádném případě by neměl zbytečně popisovat kód jak funguje, neboť se
   očekává, že ten kdo bude kód číst sám rozumí Pythonu.

Proměnné
--------

Vytvoř proměnné::

   >>> first_name = "Davie"
   >>> last_name = "Badger"
   >>> age = 22

Vytvoř proměnné se stejnou hodnotou::

   >>> x = y = z = 1
   >>> x
   1
   >>> y
   1
   >>> z
   1

Změn hodnotu v proměnné::

   >>> age = 22
   >>> age
   22
   >>> age = 23
   >>> age
   23

Odkaž na hodnotu v jiné proměnné::

   >>> number = age
   >>> number
   23
   >>> print(number)
   23

Přehoď hodnoty proměnných::

   >>> x = 0
   >>> y = 1
   >>> x, y = y, x
   >>> print(x, y)
   1 0
   >>> x, y = y, x
   >>> print(x, y)
   0 1

Smaž proměnnou::

   >>> del number
   >>> number
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   NameError: name 'number' is not defined

.. note::

   Pokud se hodnota v proměnné nebude měnit, jedná se konstantu::

      PI = 3.14159265359

.. tip::

   Kód se zpravidla píše tak, aby mu jiní lidé rozumněli, nikoliv jen pro
   počítače::

      x = 22

      # vs

      age = 22

Rezervovaná klíčová slova
^^^^^^^^^^^^^^^^^^^^^^^^^

Názvy proměnných nesmí obsahovat tyto názvy::

   False               def                 if                  raise
   None                del                 import              return
   True                elif                in                  try
   and                 else                is                  while
   as                  except              lambda              with
   assert              finally             nonlocal            yield
   break               for                 not
   class               from                or
   continue            global              pass

Při použítí klíčového slova v názvu proměnná vznikne syntaktický error::

   >>> from = "Czech Republic"
     File "<stdin>", line 1
       from = "Czech Republic"
            ^
   SyntaxError: invalid syntax

.. note::

   Pokud ve skriptu vznikne error, tak se celý program ukončí a žádný
   další kód nebude exekutován:

   .. code::

      $ cat hello.py
      from = "Czech Republic"
      print(from)
      $ python3 hello.py
        File "hello.py", line 1
          from = "Czech Republic"
               ^
      SyntaxError: invalid syntax
      $

.. tip::

   Pokud nelze vymyslet jiný název pro proměnnou, aby neobsahovala klíčové
   slovo, tak lze za klíčové slovo doplnit podtržítko, aniž by vznikl error::

      >>> from_ = "Czech Republic"
      >>> from_
      'Czech Republic'

Typy hodnot
^^^^^^^^^^^

Čísla
"""""

* celá (``int``)::

     >>> python_version = 3
     >>> type(python_version)
     <class 'int'>

* desetinná (``float``)::

     >>> temperature_celsius = 21.0
     >>> type(temperature_celsius)
     <class 'float'>

* booleovské hodnoty (``bool``)::

     >>> is_married = False
     >>> is_young = True
     >>> type(is_married)
     <class 'bool'>

.. note::

   Od verze 3.6 lze v proměnné dobrovolně definovat její typ::

      age: int = 22

.. tip::

   Komentáře lze psát i za kód::

      temperature = 21.0  # Celsius

   Mezi kódem a komentářem jsou zpravidle 2 mezery.

Řetězce
"""""""

Posloupnost libovolných znaků (``str``)::

     >>> name = "Davie Badger"
     >>> type(name)
     <class 'str'>

.. note::

   Je-li potřeba použít uvnitř řetězce dvojité uvozovky, je nutné je zakódovat
   (escapovat) pomocí zpětného lomítka nebo použít jednoduché uvozovky::

      >>> print("He said: \"yes\"")
      He said: "yes"
      >>> print("She said: 'Yes'")
      She said: 'yes'

   Samotné zpětné lomítko se escapuje pomocí dalšího zpětného lomítka::

      >>> print("\\")
      \

   Escapování lze deaktivovat pomocí písmena ``r`` před řetězcem::

      >>> print(r"\\")
      \\

.. tip::

   V případě dlouhých řetězců je vhodné je rozdělit do několika řádků::

      >>> random_text = (
      ...    "Lorem nulla voluptas eius repellat tempora. "
      ...    "Pariatur rerum incidunt nisi expedita delectus vero!"
      ... )
      >>> print(random_text)
      Lorem nulla voluptas eius repellat tempora. Pariatur rerum incidunt nisi expedita delectus vero!

   Pro zamezení chybějících mezer na konci předešlých řádků lze použít
   alternativní postup::

      " ".join((
          "Lorem nulla voluptas eius repellat tempora.",
          "Pariatur rerum incidunt nisi expedita delectus vero!",
      ))

   Stejný princip lze aplikovat v případě, kdy by se měl každý řádek kódu v
   řetězci zalomit na novém řádku pomocí escapovacího kódu ``\n``::

      >>> random_text = "\n".join((
      ...    "Lorem nulla voluptas eius repellat tempora.",
      ...    "Pariatur rerum incidunt nisi expedita delectus vero!",
      ... ))
      >>> print(random_text)
      Lorem nulla voluptas eius repellat tempora.
      Pariatur rerum incidunt nisi expedita delectus vero!

Seznamy
"""""""

Seznam položek s libovolnou hodnotou (``list``)::

     >>> cities = ["Prague", "Brno", "Ostrava"]
     >>> type(cities)
     <class 'list'>

.. note::

   Položky v seznamu se mohou opakovat::

      numbers = [1, 1, 1]

.. tip::

   Pro seznam unikátních položek je třeba použít množiny (``set``)::

      >>> random_numbers = {1, 1, 1, 2, 3, 5, 8}
      >>> random_numbers
      {1, 2, 3, 5, 8}
      >>> type(random_numbers)
      <class 'set'>

Slovníky
""""""""

Seznam párových položek, kde každému klíčí náleží jeho libovolná hodnota
(``dict``)::

     >>> person = {
     ...     "first_name": "Davie",
     ...     "last_name": "Badger",
     ...     "age": 22,
     ...     "hobbies": ["programming"]
     ... }
     >>> type(person)
     <class 'dict'>

.. note::

   Jako odsazení se používájí zpravidla 4 mezery.

.. tip::

   Pokud je slovník rozložen do více řádků, je vhodné zakončit každý řádek
   čárkou::

      person = {
          "first_name": "Davie",
          "last_name": "Badger",
          "age": 22,
          "hobbies": ["programming"],
      }

   Tato prevence zabrání častému výskytu syntax erroru z důvodu chybějící čárky
   při změně kódu. Stejný princip lze uplatnit i u seznamů nebo množin.

Převody hodnot
""""""""""""""

Převeď hodnotu na jiný typ, je-li to možné::

   >>> int(1.0)
   1
   >>> int("3")
   3
   >>> float("1.0")
   1.0
   >>> float(3)
   3.0
   >>> str(3)
   '3'
   >>> str(1.0)
   '1.0'
   >>> list("abc")
   ['a', 'b', 'c']
   >>> set("aaa")
   {'a'}
   >>> int("text")
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   ValueError: invalid literal for int() with base 10: 'text'

Operátory
---------

Aritmetické
^^^^^^^^^^^

* sčítání (``+``)::

     >>> 1 + 1
     2
     >>> x = 1
     >>> y = 1
     >>> x + y
     2
     >>> "a" + "b" + "c"
     'abc'
     >>> [] + [1, 2, 3]
     [1, 2, 3]

* odčítání (``-``)::

     >>> 2 - 1
     1
     >>> _  # last saved result
     1
     >>> _ - 1
     0
     >> _
     0

* násobení (``*``)::

     >>> 2 * 1
     2
     >>> 3 * "a"
     'aaa'

* dělení:

  * klasické (``/``)::

       >>> 2 / 1  # Division always returns a floating point number
       2.0

  * celočíselné (``//``)::

       >>> 2 // 1
       2
       >>> 3 // 2
       1

  * zbytek po dělení (``%``)::

       >>> 3 / 2
       1

* umocnění (``**``)::

     >>> 2 ** 3
     8

.. note::

   Při práci s aritmetickými operátory musí být zpravidla na obou stranách
   stejné typy hodnot, jinak hrozí typový error::

      >>> 1 + "1"
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      TypeError: unsupported operand type(s) for +: 'int' and 'str'

.. tip::

   Je-li třeba aktualizovat hodnotu v proměnné, např. přičíst číslo, lze
   použít zkrácený zápis pomoci ``+=``::

      >>> x = 1
      >>> x = x + 1
      >>> x
      2
      >>> y = 1
      >>> y += 1
      >>> y
      2

   Stejný princip lze aplikovat i u ostatních aritmetických operátorů:

   * ``-=``
   * ``*=``
   * ``/=``
   * ``//=``
   * ``%=``
   * ``**=``

Odbočka k formátování řetězců
"""""""""""""""""""""""""""""

Namísto zřetězení řetězců je vhodné použít formátování řetězců::

   >>> day = 11
   >>> month = 4
   >>> year = 1995
   >>> "Today is " + str(day) + "." + str(month) + "." + str(year)
   'Today is 11.4.1995'
   >>> "Today is {}.{}.{}".format(day, month, year)
   'Today is 11.4.1995'
   >>> "Today is {0}.{1}.{2}".format(day, month, year)
   'Today is 11.4.1995'
   >>> "Today is {0}.{1}.{2} or {1}.{0}.{1995}?".format(day, month, year)
   'Today is 11.4.1995 or 4.11.1995?'
   >>> "Today is {day}.{month}.{year}".format(day=day, month=month, year=year)
   'Today is 11.4.1995'

.. note::

   Od verze 3.6 lze použít zkrácený zápis pro formátování f-řetězců::

      >>> first_name = "Davie"
      >>> last_name = "Badger"
      >>> f"My name is {first_name} {last_name}"
      'My name is Davie Badger'
      >>> print(f"{first_name}\n{last_name}")
      Davie
      Badger
      >>> print(fr"{first_name}\n{last_name}")
      Davie\nBadger
      >>> f"2 * 2 is {2 * 2}"
      '2 * 2 is 4'

.. tip::

   Formátovaný řetězec lze ještě dále naformátovat, případně dědit::

      >>> "{}".format(123)
      '123'
      >>> "{:13}".format(123)
      '          123'
      >>> "{:>13}".format(123)
      '123          '
      >>> "{:^13}".format(123)
      '     123     '
      >>> "{x} {{y}}".format(x=0)
      '0 {y}'
      >>> "{x} {{y}}".format(x=0).format(y=1)
      '0 1'

Pořadí aritmetických operací
""""""""""""""""""""""""""""

1. závorky
2. umocňování
3. násobení a dělení
4. sčítání a odčítání

::

   >>> ((1 + 1) ** 2 - 2 / 1) * 1
   2.0

Relační
^^^^^^^

* větší (``>``)::

     >>> 1 > 0
     True
     >>> 0 > 1
     False

* menší (``<``)::

     >>> 1 < 0
     False
     >>> 0 < 1
     True

* větší nebo rovno (``>=``)::

     >>> 1 >= 0
     True

* menší nebo rovno (``<=``)::

     >>> 1 <= 0
     False

* rovná se (``==``)::

     >>> 1 == 1
     True
     >>> 1 == 1.0
     True
     >>> is_even = 2 % 2 == 0
     >>> is_even
     True

* nerovná se (``!=``)::

     >>> "a" != "b"
     True

Logické
^^^^^^^

* a (``and``)::

     >>> 0 == 0 and 1 == 1
     True
     >>> 0 == 0 and 0 == 1
     False

* nebo (``or``)::

     >>> 0 != 0 or 1 == 1
     True
     >>> 0 != 0 or 1 != 1
     False

* ne (``not``)::

     >>> 0 == 0 and not 1 == 1
     False
     >>> 1 != 1 or not 1 != 1
     True

.. tip::

   Negaci lze taktéž použít na přepínání mezi ``True`` a ``False`` hodnotou::

      >>> is_active = True
      >>> is_active = not is_active
      >>> is_active
      False

Množinové
^^^^^^^^^

* sjednocení (``!``)::

     >>> {1, 2} | {3}
     {1, 2, 3}

* průnik (``&``)::

     >>> {1, 2} & {1}
     {1}

* rozdíl (``-``)::

     >>> {1, 2} - {1}
     {2}

* doplněk (``^``)::

     >>> {1, 2} ^ {1}
     {2}

Podmínky
--------

Spusť patřičný kód, je-li splněna podmínka::

   >>> age = 18
   >>> if age >= 18:
   ...     print("You're adult.")
   You're adult.

Spusť alternativní kód, není-li podmínka splněna::

   >>> number = 3
   >>> if number % 2 == 0:
   ...     print("It's even number.")
   ... else:
   ...     print("It's odd number.")
   It's odd number.

Zkus další podmínky, není-li předchozí podmínka splněna::

   >>> age = 17
   >>> if age < 0:
   ...     print("You don't exist.")
   ... elif age < 18:
   ...     print("You're child.")
   ... else:
   ...     print("You're adult.")
   You're child.

Podmínky včetně logických spojek::

   >>> age = 22
   >>> if age >= 18 and <= 26:
   ...     print("You are still young person")
   ...
   You are still young person
   >>> if 18 <= age <= 26:
   ...     print("You are still young person")
   ...
   You are still young person

.. note::

   Je-li třeba vyhodnotit pravdivost či nepravdivost hodnoty v proměnné, není
   nutné používat relační operátory::

      >>> todos = []
      >>> if todos:
      ...     print("I have to do something.")
      ... else:
      ...     print("I don't have to anything.")
      I don't have to do anything.

   Přehled pravdivostních a nepravdivostních hodnot:

   =====  ================  ==================
   Typ    Pravdivé hodnoty  Nepravdivé hodnoty
   =====  ================  ==================
   int    -1, 1             0
   float  -1.0, 1.0         0.0
   str    "text"            ""
   list   [1, 2, 3]         []
   set    {1, 2, 3}         set()
   dict   {"age": 22}       {}
   =====  ================  ==================

   Ověření pravdivosti::

      >>> bool([])
      False
      >>> bool([1, 2 3])
      True

.. tip::

   Je-li třeba na základě ``if`` a ``else`` podmínky uložit nějakou hodnotu
   do proměnné, lze použít zkrácený zápis::

      >>> number = 2
      >>> is_even = True if number % 2 == 0 else False
      >>> is_even
      True

   Taktéž lze použít logické operátory ``and`` a ``or``::

      >>> is_married = True or False
      >>> is_married
      True

   U operátoru ``and`` je třeba dávat pozor, ze při pravdivosti všech
   objektů se jako výsledek uloží hodnota posledního objektu::

      >>> a = 1
      >>> b = "1"
      >>> c = [1]
      >>> x = a and b and c
      >>> x
      [1]
      >>> True and True and True
      True
      >>> True and True and False
      False

Cykly
-----

for
^^^

Opakuj N-krát kód uvnitř cyklu::

   >>> name = input("Enter your name: ")
   Enter your name: Davie
   >>> for character in name:
   ...     print(character)
   ...
   D
   a
   v
   i
   e

.. note::

   Cykly lze aplikovat na řetězce, seznamy či slovníky::

      >>> person = {"name": "Davie Badger", "age": 22}
      >>> for key in person:
      ...    print(f"{key}: {person[key]}")
      ...
      name: Davie Badger
      age: 22

   Cyklus se bude opakovat tolikrát, kolik existuje položek v dané hodnotě::

      >>> len("Davie")
      5

.. tip::

   Je-li třeba vědět, s kolikátou položkou se aktuálně pracuje::

      >>> name = "Davie"
      >>> for index, character in enumerate(name):
      ...     print(f"Index {index} contains {character} character")
      ...
      Index 0 contains D character
      Index 1 contains a character
      Index 2 contains v character
      Index 3 contains i character
      Index 4 contains e character

   V programování se zpravidla začíná počítat od nuly.

Odbočka k indexům
"""""""""""""""""

Pomocí indexů lze přístupovat k jednotlivým položkám řetězce či seznamu::

   >>> name = "Davie Badger"
   >>> name[0]
   'D'
   >>> cities = ["Prague", "Brno", "Ostrava"]
   >>> cities[0]
   'Prague'

U slovníků je třeba přístupovat pomocí názvů klíčů::

   >>> person = {"name": "Davie Badger"}
   >>> person["name"]
   'Davie Badger'

.. note::

   Indexy zpravidla musí existovat v sekvenci, jinak hrozí indexový error::

      >>> cities = ["Prague", "Brno", "Ostrava"]
      >>> cities[3]
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      IndexError: list index out of range

   U slovníků hrozí klíčový error, pokud daný klíč neexistuje ve slovníku::

      >>> empty_dict = {}
      >>> empty_dict["key"]
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      KeyError: 'key'

.. tip::

   Způsoby indexování u sekvencí:

   ======  =========================  =============================
   Index   Význam                     Výstup
   ======  =========================  =============================
   [0]     První položka              'Prague'
   [-1]    Poslední položka           'Ostrava'
   [:]     Kopie sekvence             ['Prague', 'Brno', 'Ostrava']
   [1:]    Interval <1, konec>        ['Brno', 'Ostrava']
   [:2]    Interval <začátek, 2)      ['Prague', 'Brno']
   [1:2]   Interval <1, 2)            ['Brno']
   [::2]   Ob jednu položku           ['Prague', 'Ostrava']
   [::-1]  Obrácená sekvence          ['Ostrava', 'Brno', 'Prague']
   ======  =========================  =============================

Příkaz continue
"""""""""""""""

Přeskoč exekuci kódu v cyklu, je-li něco nevhodného::

   >>> for number in range(11):  # <0, 11)
   ...     if number % 2 != 0:
   ...         continue
   ...     print(f"Number {number} is even")
   ...
   Number 0 is even
   Number 2 is even
   Number 4 is even
   Number 6 is even
   Number 8 is even
   Number 10 is even
   >>> for number in range(11):
   ...     if number % 2 == 0:
   ...         print(f"Number {number} is even")
   ...
   Number 0 is even
   Number 2 is even
   Number 4 is even
   Number 6 is even
   Number 8 is even
   Number 10 is even

.. note::

   Taktéž lze nastavit jiný interval pro vygenerování posloupnosti celých
   čísel::

      >>> list(range(1, 4))  # <1, 4)
      [1, 2, 3]

.. tip::

   Ignoruj aktuální položku ze sekvence::

      >>> for _ in range(3):
      ...     print("Spam")
      ...
      Spam
      Spam
      Spam

Příkaz break
""""""""""""

Ukončí násilně cyklus::

   >>> allowed_letter = ["d", "g", "o"]
   >>> word = input("Enter a word which contains only letters 'd' or 'g' or 'o': ")
   Enter a word which contains only letters 'd' or 'g' or 'o': test
   >>> for letter in word:
   ...     if letter not in allowed_letters:
   ...         print(f"Word '{word}' is not allowed")
   ...         break
   ...
   Word 'test' is not allowed

.. tip::

   Spusť kód, pokud v cyklu nedošlo k jeho násilnému ukončení nebo jiné chybě::

      >>> allowed_letter = ["d", "g", "o"]
      >>> word = input("Enter a word which contains only letters 'd' or 'g' or 'o': ")
      Enter a word which contains only letters 'd' or 'g' or 'o': dog
      >>> for letter in word:
      ...     if letter not in allowed_letters:
      ...         print(f"Word '{word}' is not allowed")
      ...         break
      ... else:
      ...     print(f"Yes, {word} is a valid word")
      ...
      Yes, dog is a valid word

while
^^^^^

Opakuj N-krát kód uvnitř cyklu, dokud je podmínka platná::

   >>> number = int(input("Guess number: "))
   Guess number: 1
   >>> while number != 5:
   ...     number = int(input("Sorry, try again: "))
   ...
   Sorry, try again: 2
   Sorry, try again: 3
   Sorry, try again: 4
   Sorry, try again: 5
   >>> number
   5

.. note::

   Místo podmínky lze použít pravdivou hodnotu, pomocí které vznikne nekonečný
   cyklus::

      >>> while True:
      ...     print("Spam")
      ...
      Spam
      Spam
      Spam
      Spam
      Spam

   Nekonečný cyklus lze v shellu ukončit pomocí klávesové zkratky
   ``CTRL + c``::

      >>> while True:
      ...     print("Spam")
      ...
      Spam
      Spam
      Spam
      ^CSpam
      Traceback (most recent call last):
        File "<stdin>", line 2, in <module>
      KeyboardInterrupt

   V kódu lze vyskočit z nekonečného cyklu pomocí příkazu ``break``, zpravidla
   při nějaké splněné podmínce.

.. tip::

   Spusť kód, pokud se podmínka u cyklu stala nepravdivá::

      >>> number = int(input("Guess number: "))
      Guess number: 1
      >>> while number != 3:
      ...     number = int(input("Sorry, try again: "))
      ... else:
      ...     print("You've just guessed the right number")
      Sorry, try again: 2
      Sorry, try again: 3
      You've just guessed the right number

Funkce
------

Vlastní funkce
^^^^^^^^^^^^^^

Vytvoř a zavolej vlastní funkci bez argumentů::

   >>> def say_hello():
   ...     print("Hello")
   ...
   >>> say_hello()
   Hello

Vytvoř a zavolej vlastní funkci s povinným pozičním argumentem::

   >>> def say_hello(name):
   ...     print(f"Hello {name}")
   ...
   >>> say_hello()
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: say_hello() missing 1 required positional argument: 'name'
   >>> say_hello("Davie")
   Hello Davie
   >>> say_hello(name="Davie")
   Hello Davie

Vytvoř a zavolej vlastní funkcí s volitelným argumentem::

   >>> def say_hello(name="No One"):
   ...     print(f"Hello {name}")
   ...
   >>> say_hello()
   Hello No One

Vytvoř a zavolej vlastní funkcí s povinným pozičním a volitelným argumentem::

   >>> def power(x, y=2)
   ...     print(x * y)
   ...
   >>> power(2)
   4
   >>> power(2, 3)
   6

Vytvoř a zavolej vlastní funkci s neomezeným počtem pozičních argumentů::

   >>> numbers = [1, 2, 3]
   >>> def sum_numbers(*numbers):
   ...     result = 0
   ...     for number in numbers:
   ...         result += number
   ...     print(result)
   ...
   >>> def sum_numbers(*numbers)
   6
   >>> def sum_numbers(1, 2, 3)
   6

Vytvoř a zavolej vlastní funkci s neomezeným počtem klíčových argumentů::

   >>> person = {
   ...     "name": "Davie Badger",
   ...     "age": 22,
   ... }
   >>> def person_details(**details):
   ...     for detail in details:
   ...         print(f"{detail} - {details[detail]}")
   ...
   >>> person_details(**person)
   name - Davie Badger
   age - 22
   >>> person_details(name="Davie Badger", age=22)
   name - Davie Badger
   age - 22
   >>> person_details("Davie Badger", 22)
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: person_details() takes 0 positional arguments but 2 were given

Vytvoř a zavolej vlastní funkci s povinným pozičním a klíčovým argumentem::

   >>> def say_hello(name, *, repeat):
   ...     for _ in range(repeat)
   ...         print(f"Hello {name}")
   ...
   >>> say_hello("Davie")
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: say_hello() missing 1 required keyword-only argument: 'repeat'
   >>> say_hello("Davie", 3)
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: say_hello() takes 1 positional argument but 2 were given
   >>> say_hello("Davie", repeat=3)
   Hello Davie
   Hello Davie
   Hello Davie

Vytvoř a zavolej vlastní funkci s povinnými klíčovými argumenty::

   >>> def person_details(*, name, age):
   ...     print(f"{name}, {age}")
   ...
   >>> person_details("Davie Badger", 22)
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: person_details() takes 0 positional arguments but 2 were given
   >>> person_details(name="Davie Badger", age=22)
   Davie Badger, 22

.. note::

   K proměnným, které jsou vytvořené uvnitř funkcí, nelze z vnějšku
   přístupovat::

      >>> def create_variable_age():
      ...     age = 22
      ...
      >>> age
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      NameError: name 'age' is not defined
      >>> create_variable_age()
      >>> age
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      NameError: name 'age' is not defined

   Naopak zevnitř funkce lze přístupovat k vnějším (globálním) proměnnám bez
   možností měnit její hodnotu::

      >>> age = 22
      >>> def print_age():
      ...     print(age)
      ...
      >>> print_age()
      22

.. tip::

   Funkce lze taktéž použít namísto dlouhých a mnohdy nečitelných podmínek::

      >>> def is_leap_year(year):
      ...     return (year % 4 == 0 and year % 100 != 0) or year % 400 == 0
      ...
      >>> year = int(input("Enter an year: "))
      Enter an year: 1995
      >>> if is_leap_year(year):
      ...     print(f"{year} is a leap year")
      ... else:
      ...     print(f"{year} is not a leap year")
      ...
      1995 is not a leap year

Odbočka k parametrům a argumentům funkce
""""""""""""""""""""""""""""""""""""""""

Pořadí jednotlivých parametrů funkce, pro které lze zadávat argumenty::

   >>> def example(x, y=1, *args, **kwargs):
   ...     print(x)
   ...     print(y)
   ...     print(args)
   ...     print(kwargs)
   ...
   >>> example(0)
   0
   1
   ()
   {}
   >>> example(1, 2)
   1
   2
   ()
   {}
   >>> example(1, 2, 3, 4, 5)
   1
   2
   (3, 4, 5)
   {}
   >>> example(1, 2, 3, 4, 5, name="Davie Badger", age=22)
   1
   2
   (3, 4, 5)
   {'name': 'Davie Badger', 'age': 22}

.. note::

   Jako defaultní hodnoty lze použít všechny datové typy kromě seznamů,
   slovníků, množin a později instancí vlastních třid, kde může dojít k
   nechtěné mutaci hodnot::

      >>> def add_number(number, numbers=[]):
      ...     numbers.append(number)
      ...     return numbers
      ...
      >>> add_number(0)
      [0]
      >>> add_number(1)
      [0, 1]
      >>> add_number(2)
      [0, 1, 2]

   Pokud i přesto je nutné mít výchozí hodnotu jako prázdný list, je nezbytné
   pro zamezení mutace použít jako defaultní argument jiný datový typ::

      >>> def add_number(number, numbers=None):
      ...     if numbers is None:
      ...         numbers = []
      ...     numbers.append(number)
      ...     return numbers
      ...
      >>> add_number(0)
      [0]
      >>> add_number(1)
      [1]
      >>> add_number(2)
      [2]

   Hodnota ``None`` je fakticky prázdná hodnota, která nic neobsahuje::

      >>> empty = None
      >>> empty
      >>> print(empty)
      None
      >>> type(empty)
      <class 'NoneType'>
      >>> bool(empty)
      False

.. tip::

   Funkce může omezeně či neomezeně volat samu sebe, pokud se správně předávájí
   argumenty::

      >>> def countdown(number):
      ...     if number != 0:
      ...         print(number)
      ...         countdown(number - 1)
      ...     else:
      ...         print("GO!")
      ...
      >>> countdown(3)
      3
      2
      1
      GO!

Příkaz return
"""""""""""""

Vrať po zavolání funkci nějakou hodnotu::

   >>> def multiply(x, y):
   ...     return x * y
   ...
   >>> multiply(1, 2)
   2
   >>> result = multiply(1, 2)
   >>> result
   2
   >>> def multiply(x, y):
   ...     print(x * y)
   ...
   >>> result = multiply(1, 2)
   2
   >>> result
   >>>

Ukonči funkci a vrať hodnotu::

   >>> def is_even(number):
   ...     if number % 2 == 0:
   ...         return True
   ...     return False
   >>> is_even(2)
   True
   >>> is_even(3)
   False
   >>> def is_even(number):
   ...     return number % 2 == 0
   ...
   >>> is_even(2)
   True
   >>> is_even(3)
   False

.. note::

   Pokud funkce nic explicitně nevrací, tak vrácena hodnota z funkce je
   ``None``::

      >>> def test_nothing():
      ...     pass
      ...
      >>> nothing = test_nothing()
      >>> type(nothing)
      <class 'NoneType'
      >>> def test_another_nothing():
      ...     return None
      ...
      >>> test_another_nothing() is None
      True

   Naopak lze vracet í více než jednu hodnotu a to ve formě n-tice::

      >>> def get_numbers():
      ...     return 1, 2, 3, 4, 5
      ...
      >>> numbers = get_numbers()
      >>> numbers
      (1, 2, 3, 4, 5)
      >>> type(numbers)
      <class 'tuple'>
      >>> numbers[0]
      1

.. tip::

   K funcím lze psát dokumentaci, zpravidla podle Google_ stylu
   (alternativě lze použít Numpy_ styl)::

      def multiply(x, y):
          """
          Multiply two numbers.

          Args:
              x (int): First number for multiplication.
              y (int): Second number for multiplication.

          Returns:
              int: Result of multiplication of two numbers.

          Example:
              >>> multiply(2, 3)
              6
          """
          return x * y

   Ovšem ne vždy se daří dokumentaci aktualizovat, proto je vhodné použít i
   typové anotace a kontrolovat argumenty funkcí pomocí Mypy_ kontrolovače::

      def multiply(x: int, y: int) -> int:
          """
          Multiply two numbers.

          Args:
              x (int): First number for multiplication.
              y (int): Second number for multiplication.

          Returns:
              int: Result of multiplication of two numbers.

          Example:
              >>> multiply(2, 3)
              6
          """
          return x * y

Příkaz pass
"""""""""""

Nevykonej žádný kód po zavolání funkce::

   >>> def nothing():
   ...     pass
   ...
   >>> nothing()
   >>>

.. note::

   Příkaz ``pass`` se zpravidla používá k označení kódu, který ještě není
   dokončen::

      >>> def is_even():
      ...     pass
      ...
      >>>

   Po dokončení kódu příkaz ``pass`` zmizí::

      >>> def is_even(number):
      ...     return number % 2 == 0
      ...
      >>>

   Bez příkazu ``pass`` vznikne odsazující error::

      >>> def empty():
      ...
        File "<stdin>", line 2

          ^
      IndentationError: expected an indented block

.. tip::

   Příkaz ``pass`` lze použít i u podmínek nebo cyklů::

      >>> if True:
      ...     pass
      ...
      >>>

Zabudované funkce
^^^^^^^^^^^^^^^^^

Seznam již existujících funkcí::

   abs()           dict()        help()          min()        setattr()
   all()           dir()         hex()           next()       slice()
   any()           divmod()      id()            object()     sorted()
   ascii()         enumerate()   input()         oct()        staticmethod()
   bin()           eval()        int()           open()       str()
   bool()          exec()        isinstance()    ord()        sum()
   bytearray()     filter()      issubclass()    pow()        super()
   bytes()         float()       iter()          print()      tuple()
   callable()      format()      len()           property()   type()
   chr()           frozenset()   list()          range()      vars()
   classmethod()   getattr()     locals()        repr()       zip()
   compile()       globals()     map()           reversed()   __import__()
   complex()       hasattr()     max()           round()
   delattr()       hash()        memoryview()    set()

* ``abs(number)``

  * vrať absolutní hodnotu čísla::

       >>> abs(-1)
       1
       >>> abs(0)
       0
       >>> abs(1.0)
       1.0

* ``all(iterable)``

  * vrať ``True``, pokud všechny položky v ``iterable`` (datové typy, na které
    lze použít cykly) jsou pravdivé::

       >>> all([])
       True
       >>> all([1, 2, 3])
       True
       >>> all([0, 1, 2, 3])
       False

* ``any(iterable)``

  * vrať ``True``, pokud alespoň jedna položka v ``iterable`` je pravdivá::

       >>> any([])
       False
       >>> any([0])
       False
       >>> any([0, 1])
       True

* ``bool(value=False)``

  * vrať ``True`` nebo ``False``, je-li hodnota pravdivá či nepravdivá::

       >>> bool()
       False
       >>> bool(0)
       False
       >>> bool(1)
       True

* ``callable(object)``

  * vrať ``True``, je-li daný objekt volatelný::

       >>> callable("test")
       False
       >>> def test():
       ...     pass
       ...
       >>> callable(test)
       True

* ``dict(value={})``

  * převeď hodnotu na slovník, je-li to možné::

       >>> dict()
       {}
       >>> dict([("name", "Davie"), ("age", 22)])
       {'name': 'Davie', 'age': 22}

* ``divmod(x, y)``

  * vrať n-tici s výsledkem celočíselného dělení a zbytkem::

       >>> divmod(2, 1)
       (2, 0)
       >>> divmod(10, 3)
       (3, 1)

* ``enumerate(iterable, start=0)``

  * vrať ``enumerate`` objekt, který interně přiřadí index k jednotlivým
    položkam v ``iterable``::

       >>> enumerate(["a", "b", "c"])
       <enumerate object at 0x7fdb4258bb40>
       >>> list(enumerate(["a", "b", "c"]))
       [(0, 'a'), (1, 'b'), (2, 'c')]
       >>> list(enumerate(["a", "b", "c"], start=1))
       [(1, 'a'), (2, 'b'), (3, 'c')]

* ``filter(function, iterable)``

  * vrať ``filter`` objekt, ve kterém jsou položky z ``iterable``, pro které
    funkce v ``function`` vrátila ``True`` hodnotu::

       >>> filter(lambda number: number % 2 == 0, range(11))
       <filter object at 0x7fdb42584e48>
       >>> list(filter(lambda number: number % 2 == 0, range(11)))
       [0, 2, 4, 6, 8, 10]
       >>> list(filter(None, [0, 1, "", "2", {}, {3}]))
       [1, '2', {3}]

* ``float(value=0.0)``

  * převeď hodnotu na desetinné číslo, je-li to možné::

       >>> float()
       0.0
       >>> float("1")
       1.0
       >>> float("inf")  # infinity
       inf
       >>> float("-inf")
       -inf

* ``frozenset(iterable=None)``

  * vrať ``iterable`` zkonvertovaný na neměnitelnou množinu::

       >>> frozenset()
       frozenset()
       >>> frozenset([0, 1, 0, 1, 0])
       frozenset({0, 1})

* ``input(prompt="")``

  * vrať uživatelský vstup::

       >>> input()

       ''
       >>> input("Your name: ")
       Your name: Davie
       'Davie'

* ``int(value=0, base=10)``

  * převeď hodnotu na číslo v desítkové soustavě, jeli-to možné::

       >>> int()
       0
       >>> int("1")
       1

* ``len(sequence)``

  * vrať počet položek v sekvenci::

       >>> len("test")
       4

* ``list(iterable=None)``

  * převeď ``iterable`` na na seznam::

       >>> list()
       []
       >>> list(range(3))
       [0, 1, 2]

* ``map(function, iterable)``

  * vrať ``map`` objekt, ve kterém jsou položky z ``iterable`` po aplikakování
    funkce ``function``::

       >>> map(lambda number: number * 2, [1, 2, 3])
       <map object at 0x7fdb42584e48>
       >>> list(map(lambda number: number * 2, [1, 2, 3]))
       [2, 4, 6]

* ``max(iterable, *args)``

  * vrať položku s nejvyšší hodnotou z ``iterable`` či poskytnutých argumentů::

       >>> max([1, 2, 3])
       3
       >>> max(1, 2, 3)
       3

* ``min(iterable, *args)``

  * vrať položku s nejnižší hodnotou z ``iterable`` či poskytnutých argumentů::

       >>> min([1, 2, 3])
       1
       >>> min(1, 2, 3)
       1

* ``open(file, mode="r", encoding=None)``

  * otevři a vrať ``file`` objekt v daném módu ``mode`` a kódování
    ``encoding``, pokud soubor ``file`` existuje::

       >>> open("/etc/passwd", encoding="UTF-8")
       <_io.TextIOWrapper name='/etc/passwd' mode='r' encoding='UTF-8'>

  * základní módy:

    * ``r``

      * pro čtení

    * ``r+``

      * pro čtení a zapisování

    * ``w``

      * pro zapisování (přepísování) od začátku souboru

    * ``w+``

      * pro čtení a zapisování, pričemž se obsah existujícího souboru nejdříve
        smaže

    * ``a``

      * pro zapisování na konec souboru

    * ``a+``

      * pro čtení a zapisování na konec souboru

    * ``x``

      * pro vytvoření souboru, pokud ještě neexistuje

* ``print(*objects, sep=" ", end="\n")``

  * vytiskni objekty ``objects`` v textové podobě na standardní výstup podle
    daného oddělovače ``sep`` a zakončovače ``end``::

       >>> print(1, 2, 3)
       1 2 3
       >>> print(1, 2, 3, sep="")
       123
       >>> print(1, 2, 3, end="")
       123>>>

* ``range(stop)``

  * vrať ``range`` objekt, ve kterém jsou celá čísla od nuly po ``stop``
    číslo::

       >>> range(10)
       range(0, 10)
       >>> list(range(10))
       [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

* ``range(start, stop, step=0)``

  * vrať ``range`` objekt, ve kterém jsou celá čísla v intervalu ``start`` až
    ``stop`` s případným krokem ``step``::

       >>> range(1, 6)
       range(1, 6)
       >>> list(range(1, 6))
       [1, 2, 3, 4, 5]
       >>> list(range(1, 6, 2))
       [1, 3, 5]

* ``reversed(sequence)``

  * vrať ``list_reverseiterator`` objekt, kde jsou položky v ``sequence`` v
    obráceném pořadí::

       >>> reversed("Davie")
       <reversed object at 0x7fdb42584eb8>
       >>> list(reversed("Davie"))
       ['e', 'i', 'v', 'a', 'D']

* ``round(number, ndigits=None)``

  * zaokrouhlí číslo na daný počet desetinných míst (není zcela přesné)::

       >>> round(1.4)
       1
       >>> round(1.4, 0)
       1.0
       >>> round(1.45, 1)  # Correct is 1.5
       1.4

* ``set(iterable=None)``

  * převeď ``iterable`` na množinu, je-li to množné::

       >>> set()
       set()
       >>> set([0, 1, 0])
       {0, 1}

* ``slice(stop)``

  * vrať ``slice`` objekt s intervalem jako u indexování nebo funkce
    ``range``::

       >>> numbers = list(range(10))
       >>> first_three = slice(3)
       >>> numbers[first_three]
       [0, 1, 2]

* ``slice(start, stop, step=None)``

  * vrať ``slice`` objekt s intervalem jako u indexování nebo funkce
    ``range``::

       >>> numbers = list(range(10))
       >>> every_second = slice(0, 10, 2)
       >>> numbers[every_second]
       [0, 2, 4, 6, 8]

* ``sorted(iterable, key=None, reverse=False)``

  * vrať seřazený seznam z položek v ``iterable``::

       >>> sorted([3, 2, 1])
       [1, 2, 3]
       >>> sorted([1, 2, 3], reverse=True)
       [3, 2, 1]
       >>> students = [("John", "M", 18), ("Jane", "F", 17)]
       >>> sorted(students, key=lambda student: student[2])
       [('Jane', 'F', 17), ('John', 'M', 18)]

* ``str(object="")``

  * převeď ``object`` na řetězec::

       >>> str()
       ''
       >>> str(1)
       '1'
       >>> str(None)
       'None'

* ``sum(iterable, start=0)``

  * sečti položky v ``iterable`` od začátku ``start``::

       >>> sum([1, 1, 1])
       3

* ``tuple(iterable=())``

  * převeď ``iterable`` na n-tici, je-li to možné::

       >>> tuple()
       ()
       >>> tuple([1])
       (1,)
       >>> tuple([1, 2, 3])
       (1, 2, 3)

* ``type(object)``

  * vrať typ objektu ``object``::

       >>> type(1)
       <class 'int'>

* ``zip(*iterables)``

  * vrať ``zip`` objekt, který propojí jednotlivé položky v ``iterables`` do
    n-tic, dokud se některý ``iterable`` nevyčerpá nebo naopak rozbalí
    ``zip`` objekt::

       >>> a = [1, 2, 3]
       >>> b = ["a", "b", "c"]
       >>> zip(a, b)
       <zip object at 0x7fdb4258dc88>
       >>> list(zip(a, b))
       [(1, 'a'), (2, 'b'), (3, 'c')]
       >>> list(zip(*zip(a, b)))
       [(1, 2, 3), ('a', 'b', 'c')]

.. note::

   U funkcí příjímací jako argument jinou funkci je vhodnější místo bezejmenné
   lambda funkce použít standardní pojmenovanou funkci kvůli čitelnosti::

      >>> def is_odd(number):
      ...     return number % 2 != 0
      ...
      >>> list(filter(is_odd, range(11)))
      [1, 3, 5, 7, 9]

.. tip::

   Při IO operacích se soubory je vhodnější použít konstrukci ``with`` s funkcí
   ``open``, kde dojde k automatickému zavření souboru po ukončení práce s
   daným souborem::

      with open("/path/to/file") as file:
          for line in file:
              print(line)

      with open("/etc/passwd") as file:
          file_content = file.read()

      with open("new_file.txt", mode="w") as file:
          file.write("Hello World!")

Odbočka k reduce funkci
"""""""""""""""""""""""

Vedle zabudovaných funcí ``map`` a ``filter`` existuje ještě funkce ``reduce``
ze standardní knihovny ``functools``, která postupně provádí operace nad
každou další položkou z ``iterable`` s výsledkem předchozích dvou položek::

   >>> from functools import reduce
   >>> numbers = range(1, 6)
   >>> # reduce(function, iterable, initializer=None)
   ...
   >>> # reduce like sum
   ... reduce(lambda x, y: x + y, numbers)
   15
   >>> # reduce like max
   ... reduce(lambda x, y: x if x > y else y, numbers)
   5
   >>> # reduce like min
   ... reduce(lambda x, y: x if x < y else y, numbers)
   1
   >>> reduce(lambda x, y: x * y, numbers)
   120

.. note::

   Pokud je ``iterable`` prázdný, tak se vyvolá typový error::

      >>> from functools import reduce
      >>> reduce(lambda x, y: x + y, [])
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      TypeError: reduce() of empty sequence with no initial value

   Pro zamezení typové chyby je třeba použít výchozí hodnotu::

      >>> from functools import reduce
      >>> reduce(lambda x, y: x + y, [], 0)
      0

   Avšak pokud není ``iterable`` prázdný a výchozí hodnota je nastavena,
   tak výchozí hodnota se bere jako první položka v ``iterable``::

      >>> from functools import reduce
      >>> reduce(lambda x, y: x + y, [1], 1)
      2
      >>> reduce(lambda x, y: x + y, [1])
      1

.. tip::

   Místo nečitelných lambda funkcí lze použít čitelné funkce ze zabudované
   knihovny ``operator``, které jsou ekvivalentem operací s operátory::

      >>> from functools import reduce
      >>> from operator import add, sub, mul, truediv
      >>> reduce(add, [1, 2, 3])
      6
      >>> reduce(sub, [3, 2, 1])
      0
      >>> reduce(mul, [1, 1, 1])
      1
      >>> reduce(truediv, [6, 3, 2, 1])
      1.0

Importování
-----------

Moduly
^^^^^^

Modulem je každý Python soubor, ze kterého lze importovat objekty::

   # fibonacci.py:

   def fibonacci(number):
       """
       Fibonacci series up to number.
       """
       a, b = 0, 1

       while b < number:
           print(b, end=" ")
           a, b = b, a + b
       else:
           print()

Funkci ``fibonacci`` lze naimportovat do interaktivního shellu, pokud se
soubor ``fibonacci.py`` nachází v místě, odkud je shell spuštěn::

   >>> from fibonacci import fibonacci
   >>> fibonacci(100)
   1 1 2 3 5 8 13 21 34 55 89

.. note::

   Pokud se obsah souboru změní, je nutné znovuotevřít interaktivní shell,
   jinak se změna v kódu neprojeví.

   Alternativní postup je nechat znovunačíst modul::

      >>> from fibonacci import fibonacci
      >>> fibonacci(100)
      1 1 2 3 5 8 13 21 34 55 89
      >>> import importlib
      >>> import fibonacci
      >>> importlib.reload(fibonacci)
      >>> from fibonacci import fibonacci
      >>> fibonacci(100)
      1-1-2-3-5-8-13-21-34-55-89-

.. tip::

   Pokud je modul spušteň jako skript, používá se na konci souboru následující
   patička::

      if __name__ == "__main__":
          main()

   Uvnitř podmínky bývá zpravidla kód pro exekuci programu, což je obvykle
   zavolání nějaké funkce. Tato hlavní funkce by měla vracet explicitně nulu,
   než ``None``, což indikuje, že program úspěšně skončil.

   Pro propojení exit statusu skriptu s shellem je vhodné ještě použít
   systémovou knihovnu::

      import sys


      def main():
          return 0


      if __name__ == "__main__":
         sys.exit(main())

Balíčky
^^^^^^^

Balíčkem je každý adresář, ve kterém jsou moduly a zpravidla i speciální soubor
``__init__.py`` pro označení adresáře jako balíčku::

   package/
     subpackage/
       __init__.py
       a.py
       b.py
       c.py
     __init__.py
     a.py
     b.py
     c.py

Pokud je interaktivní shell spuštěn z místa, ve kterém se nachází adresář
``package``, tak lze ostatní moduly z balíčku importovat::

   >>> from package.a import X
   >>> from package.b import Y
   >>> from package.c import Z
   >>> from package.subpackage.a import X
   >>> from package.subpackage.b import Y
   >>> from package.subpackage.c import Z

.. note::

   U importování může dojít zacyklení, pokud např. soubor A importuje objekt
   ze souboru B a ten naopak importuje ze souboru A pomocí syntaxe ``from``::

      >>> from a import X
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "/home/davie/a.py", line 1, in <module>
          from b import Y
        File "/home/davie/b.py", line 1, in <module>
          from a import X
      ImportError: cannot import name 'X'

   Řešením je zpravidla neimportovat navzájem mezi sebou, nýbrž vytvořit
   další nezávisly soubor C pro export, ze kterého budou soubory A a B
   importovat.

   Alternativně lze importovat tak, aby nic nebylo spuštěno během startu
   programu. Dále je pak třeba kód zaobalit do funkcí či jiných objektů, které
   se volají, až když je to nutné a to z nezávislého třetího souboru::

      $ cat a.py
      import b

      X = 0


      def foo():
          # or use from import here like:
          #
          # from b import Y
          #
          # print(Y)

          print(b.Y)
      $ cat b.py
      import a

      Y = 1


      def bar():
          # or
          #
          # from a import X
          #
          # print(X)

          print(a.X)
      $ cat c.py
      from a import foo
      from b import bar

      foo()
      bar()
      $ python3 c.py
      1
      0

.. tip::

   Soubor ``__init__.py`` je zpravidla prázdný, ale lze jej použít i na
   zkrácení importovací cesty pro objekty z modulů v daném balíčku::

      # __init__.py

      from a import X

   Zkrácený import lze pak provést s vynecháním názvu modulu::

      >>> from package.a import X
      >>> from package import X

   Dále lze i přehledně vyjmenovat, jaké objekty lze zkráceně importovat::

      # __init__.py

      from a import X

      __all__ = ["X"]

Odbočka k externím balíčkům
"""""""""""""""""""""""""""

Pomocí instalátoru `pip`_ lze nainstalovat i externí balíčky, které se
zpravidla nacházejí v repozitáři `PyPI`_.

Přehled těch nejznámějších balíčků lze najít na `Awesome Python`_.

Odbočka ke způsobu importování
""""""""""""""""""""""""""""""

1. celý modul / balíček::

      >>> import os
      >>> import sys

2. konkrétní objekt z modulu / balíčku::

      >>> from package import X

3. konkrétní objekt s alisem z modulu / balíčku::

      >>> from package import X as x

4. všechny objekty z modulu / balíčku (nebezpečná varianta)::

      >>> from package import *

.. note::

   Importovat lze i relativní cestou, ale preferovanější způsob je absolutní
   cestou::

      # Relative

      from .. import X  # from higher __init__.py
      from ..a import X
      from . import X  # from actual __init__.py
      from .a import X

      # Absolute

      from package.subpackage import X
      from package.subpackage.a import X
      from package import X
      from package.a import X

   U absolutní cesty je akorát nutné dávat pozor, aby se balíček nebo modul
   nejmenoval stejně jako již existující modul ve standardní knihovně, např.
   ``random``, neboť by došlo k jeho nahrazení lokálním modulem:

   .. code:: none

      $ ls
      random.py
      $ cat random.py
      $ python3 -q
      >>> from random import choice
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      ImportError: cannot import name 'choice'
      Error in sys.excepthook:
      Traceback (most recent call last):
        File "/usr/lib/python3/dist-packages/apport_python_hook.py", line 63, in apport_excepthook
          from apport.fileutils import likely_packaged, get_recent_crashes
        File "/usr/lib/python3/dist-packages/apport/__init__.py", line 5, in <module>
          from apport.report import Report
        File "/usr/lib/python3/dist-packages/apport/report.py", line 12, in <module>
          import subprocess, tempfile, os.path, re, pwd, grp, os, time
        File "/usr/lib/python3.6/tempfile.py", line 184, in <module>
          from random import Random as _Random
      ImportError: cannot import name 'Random'

      Original exception was:
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      ImportError: cannot import name 'choice'
      >>> # CTRL + d
      $ rm random.py
      $ python3 -q
      >>> from random import choice
      >>>

.. tip::

   Z modulu / balíčku lze naimportovat i více objektu najednou::

      >>> from package import X, Y, Z

   Nicméně může docházet k úpravám importů a upravovat řádek s několika
   objekty může být zdlouhavé, proto je vhodnější importovat objekty po
   jednom::

      >>> from package import X
      >>> from package import Y
      >>> from package import Z

   Pomocí chytrého editoru lze pak rychle zakomentovat / odkomentovat / přidat
   / upravit či odebrat import.

Errory a výjimky
----------------

Error je chyba ještě před spuštením programu, zpravidla syntaktická chyba::

   >>> print "Hello World!"
     File "<stdin>", line 1
       print "Hello World!"
                          ^
   SyntaxError: Missing parentheses in call to 'print'. Did you mean print("Hello World!")?

Výjimka je chyba až při běhu programu, kdy je vše syntakticky správně, ale něco
je nefunkční::

   >>> 1 / 0
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   ZeroDivisionError: division by zero

Zachytávání výjimek
^^^^^^^^^^^^^^^^^^^

Zachyť výjimku::

   >>> try:
   ...     number = int(input("Enter a number: "))
   ... except ValueError:
   ...     print("That was not a number")
   ...
   Enter a number: a
   That was not a number

Zachyť více výjimek::

   >>> try:
   ...     number = int(input("Enter a number: "))
   ... except ValueError:
   ...     print("That was not a number")
   ... except KeyboardInterrupt:
   ...     print("\nYou are a chicken")
   ...
   Enter a number: ^c (CTRL + c)
   You are a chicken

Zachyť více výjimek najednou::

   >>> try:
   ...     number = int(input("Enter a number: "))
   ... except (ValueError, KeyboardInterrupt):
   ...     print("No number entered")
   ...
   Enter a number: a
   No number entered

.. note::

   Výjimky se nemusí vždy vyskytnout, proto lze spustit alternativní kód
   pro tuto situaci::

      >>> def divide(x, y):
      ...     try:
      ...         result = x / y
      ...     except ZeroDivisionError:
      ...         print("You cannot divide by zero")
      ...     else:
      ...         print(result)
      ...
      >>> divide(1, 0)
      You cannot divide by zero
      >>> divide(1, 1)
      1.0

.. tip::

   Taktéž lze spustit kód, ať už se výjimka stala nebo ne::

      >>> def number():
      ...     try:
      ...         number = int(input("Enter a number: "))
      ...     except ValueError:
      ...         print("That was not a number")
      ...     else:
      ...         print(number)
      ...     finally:
      ...         print("Thanks for your activity")
      ...
      >>> number()
      Enter a number: 1
      1
      Thanks for your activity
      >>> number()
      Enter a number: a
      That was not a number
      Thnkas for your activity

   Konstrukci ``else`` lze vynechat a ponechat jen ``finally``.

Potlačení výjimek
^^^^^^^^^^^^^^^^^

Potlač výjimku při smazání neexistujícího souboru::

   >>> import os
   >>> os.remove("dummy_file.txt")
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   FileNotFoundError: [Errno 2] No such file or directory: 'dummy_file.txt'
   >>> def delete_file(filename):
   ...     try:
   ...         os.remove(filename)
   ...     except FileNotFoundError:
   ...         pass
   ...
   >>> delete_file("dummy_file.txt")
   >>>

.. tip::

   Potlač zkráceně výjimku::

      >>> from contextlib import suppress
      >>> delete_file(filename):
      ...     with suppress(FileNotFoundError):
      ...         os.remove(filename)
      ...
      >>> delete_file("dummy_file.txt")
      >>>

   Importováný kontextový manažer ``suppress`` umí potlačit i více výjimek
   najednou::

      >>> with suppress(IndexError, TypeError, ValueError):
      ...     pass
      ...
      >>>

Vyvolání výjimek
^^^^^^^^^^^^^^^^

Vyvolej násilně výjimku::

   >>> def countdown(number):
   ...     if not isinstance(number, int):
   ...         raise ValueError(f"{number} is not a whole number")
   ...
   >>> countdown("abc")
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "<stdin>", line 3, in countdown
   ValueError: abc is not a whole number

.. note::

   Vyvolat výjimku lze i pomocí příkazu ``assert`` spolu s podmínkou, pokud je
   neplatná::

      >>> assert 1 == 2
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      AssertionError
      >>> assert 1 == 2, "1 is not 2"
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      AssertionError: 1 is not 2

   Avšak ``assert`` oveřování se používá jen pro interní potřebu, zejména u
   testování kódu.

.. tip::

   Výjimku lze i znovu vyvolat, pokud je předtím zachycena, což může být vhodné
   pro zaslání notifikace, ve které bude celý chybový výpis (traceback)::

      >>> import traceback
      >>> def send_email(tb):
      ...     pass
      ...
      >>> try:
      ...     number = int(input("Enter a number: "))
      ... except Exception:
      ...     tb = traceback.format_exc()
      ...     send_email(tb)
      ...     raise
      ...
      Enter a number: a
      Traceback (most recent call last):
        File "<stdin>", line 2, in <module>
      ValueError: invalid literal for int() with base 10: 'a'
      >>> print(tb)
      Traceback (most recent call last):
        File "<stdin>", line 2, in <module>
      ValueError: invalid literal for int() with base 10: 'a'

   Do výjimky ``Exception`` spádá jakákoliv výjimka.

Zabudované výjimky
^^^^^^^^^^^^^^^^^^

Nejběžnější výjimky:

* ``IndexError``

  * neexistující index v sekvenci::

       >>> x = [1, 2, 3]
       >>> x[3]
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       IndexError: list index out of range

* ``KeyError``

  * neexistující klíč ve slovníku::

       >>> x = {"age": 22}
       >>> x["name"]
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       KeyError: 'name'

* ``ModuleNotFoundError``

  * modul či balíček nenalezen::

       >>> import blablabla
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       ModuleNotFoundError: No module named 'blablabla'

* ``NameError``

  * neexistující objekt v programu, zpravidla proměnná::

       >>> blablabla
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       NameError: name 'blablabla' is not defined

* ``SyntaxError``

  * syntaktická chyba v kódu::

       >>> print "Hello World!"
         File "<stdin>", line 1
           print "Hello World!"
                              ^
       SyntaxError: Missing parentheses in call to 'print'. Did you mean print("Hello World!")?

* ``TypeError``

  * neplatná operace s různými datovými typy::

       >>> 1 + "a"
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       TypeError: unsupported operand type(s) for +: 'int' and 'str'

  * chybějící argument při volání funkce::

       >>> def countdown(number):
       ...     pass
       ...
       >>> countdown()
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       TypeError: countdown() missing 1 required positional argument: 'number'

  * nevhodný typ argumentu pro funkci::

       >>> int("a")
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       ValueError: invalid literal for int() with base 10: 'a'

* ``ValueError``

  * správný typ argumentu pro funkci, ale špatná hodnota::

       >>> float("1,1")
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       ValueError: could not convert string to float: '1,1'

`Ostatní výjimky`_ lze nalézt v dokumentaci.

Vlastní výjimky
^^^^^^^^^^^^^^^

Vytvoř a vyvolej vlastní výjimku::

   >>> class MyError(Exception):
   ...     pass
   ...
   >>> raise MyError("Error")
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   __main__.MyError: Error

.. note::

   Vlastní výjimky lze i formátovat::

      >>> class MyError(Exception):
      ...     def __init__(self, code, description):
      ...         super().__init__(f"{code}: {description}")
      ...
      >>> raise MyError("ABC123", "bla bla bla")
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      __main__.MyError: ABC123: bla bla bla

.. tip::

   Pomocí aliasu zachycené výjimky se lze dostat k chybové zprávě::

      >>> class MyError(Exception):
      ...     pass
      ...
      >>> try:
      ...     raise MyError("Error")
      ... except MyError as error:
      ...     print(f"Error message: {error}")
      ...
      Error message: Error

Pokročila syntaxe
=================

Třídy
-----

Vytvoř vlastní třídu (datový typ)::

   >>> class Person:
   ...     pass
   ...
   >>> type(Person)
   <class 'type'>

Vytvoř instanci třídy::

   >>> class Person:
   ...     pass
   ...
   >>> person = Person()
   >>> type(person)
   <class '__main__.Person'>

.. note::

   Každá nová třída implicitně dědí z objektu ``object``. Tento objekt lze i
   explicitně zdědit::

      >>> class Pet(object):
      ...     pass
      ...
      >>>

.. tip::

   Pomocí zabudované funkce ``dir`` lze zobrazit všechny atributy objektu nebo
   také objekty v daném jmenném prostoru::

      >>> dir()
      ['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__', '__package__', '__spec__']
      >>> class Point(object):
      ...     x = 0
      ...     y = 1
      ...
      >>> dir(Point)
      ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'x', 'y']

   Pokud je funkce ``dir`` použíta v globálním jmenném prostoru ve skriptu,
   tak vrací více objektů oprotí shellu, hlavně magickou proměnnou
   ``__file__``, která vrací název skriptu::

      # print(dir())

      ['__annotations__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__']

      # print(__file__)

      "test.py"

      # import os
      # print(os.path.abspath(__file__))

      "/home/davie/test.py"

   Pro zjištení objektů ve jmenném prostoru a jejich hodnot lze použít
   zabudované funkce ``globals`` a ``locals``::

      >>> globals()
      {'__builtins__': <module '__builtin__' (built-in)>, '__name__': '__main__', '__doc__': None, '__package__': None}cc
      >>> def function():
      ...     x, y = 0, 1
      ...     print(locals())
      ...
      >>> function()
      {'y': 1, 'x': 0}

   Pokud je funkce ``locals`` spuštěna v globálním jmenném prostoru, budu se
   chovat stejně jako funkce ``globals``.

Atributy
^^^^^^^^

Vytvoř atributy na instanci::

   >>> class Point(object):
   ...     pass
   ...
   >>> point = Point()
   >>> point.x
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   AttributeError: 'Point' object has no attribute 'x'
   >>> point.x = 0
   >>> point.x
   0
   >>> setattr(point, "y", 1)
   >>> point.y
   1
   >>> getattr(point, "y")
   1
   >>> hasattr(point, "y")
   True
   >>> del point.x
   >>> hasattr(point, "x")
   False
   >>> delattr(point, "y")
   >>>

Vytvoř defaultní atributy (proměnné na třídě), které budou stejné u každé
vzniklé instance::

   >>> class Point(object):
   ...     x = 0
   ...     y = 1
   ...
   >>> point_a = Point()
   >>> point_b = Point()
   >>> point_a.x == point_b.x and point_a.y == point_b.y
   True

.. note::

   Vlastní objekty jsou měnitelné při alisování::

      >>> class Point(object):
      ...     x = 0
      ...
      >>> point_a = Point()
      >>> point_b = point_a
      >>> point_b.x = 1
      >>> point_a.x = 1

   Pro zamezení měnitelnosti atributů na aliasovaných objektech je třeba
   vytvořit mělkou kopii objektu::

      >>> import copy
      >>> class Point(object):
      ...     x = 0
      ...
      >>> point_a = Point()
      >>> point_b = copy.copy(point_a)
      >>> point_b.x = 1
      >>> point_a.x
      0

   Pokud atributy neobsahují jen primitivní datové typy, ale i jiné objekty,
   tak je třeba použít hlubokou kopii objektu pomocí ``copy.deepcopy(object)``.

.. tip::

   Atributy, metody ale i funkce mohou začínat na podtržítko::

      >>> def _protected_function():
      ...     pass

   Objekty, které začínájí na podtržítko slouží pro interní potřebu programu a
   tudíž nejsou součásti veřejné API (dokumentace aj.).

Odbočka omezenému počtu atributů
""""""""""""""""""""""""""""""""

Pomocí proměnné ``__slots__`` na třídě lze striktně definovat, jaké atributy
mohou existovat, čímž lze ušetřit na paměti, je-li v programu velké množství
instancí::

   >>> class Point(object):
   ...     __slots__ = ["x", "y"]
   ...     def __init__(self, x, y):
   ...        self.x = x
   ...        self.y = y
   ...
   >>> point = Point(0, 1)
   >>> point.x
   0
   >>> point.y
   1
   >>> point.z = 2
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   AttributeError: 'Point' object has no attribute 'z'
   >>> point.x = 1
   >>> point.x
   1

.. note::

   Pří použítí proměnné ``__slots__`` pak nelze použít uvedené atributy jako
   další proměnné na třídě pro definovaní defaultních hodnot::

      >>> class Point(object):
      ...     __slots__ = ["x", "y"]
      ...     x = 0
      ...     y = 1
      ...
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      ValueError: 'x' in __slots__ conflicts with class variable

.. tip::

   Pro správnou funkčnost proměnné ``__slots__`` je třeba ji mít definovanou
   na třídě a každě další zdědené třídě, kde je třeba uvést jen nové atributy,
   aby došlo ke kýženému výsledku.

   Pokud není tato situace řádně ošetřena, k žádnému šetření paměti nedojde
   a na instanci půjde přidávat další nové atributy, neboť bude přítomný
   speciální atribut ``__dict__``, což je slovník atributů a jejich hodnot::

      >>> class Person(object):
      ...     def __init__(self, name, age):
      ...         self.name = name
      ...         self.age = age
      ...
      >>> p = Person("Davie", 22)
      >>> p.__dict__
      {'name': 'Davie', 'age': 22}
      >>> vars(p)
      {'name': 'Davie', 'age': 22}
      >>> vars() == locals()
      True

Metody
^^^^^^

Vytvoř speciální inicializační metodu, která příjímá argumenty při inicializaci
objektu::

   >>> class Point(object):
   ...     pass
   ...
   >>> point = Point(0, 1)
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: object() takes no parameters
   >>> class Point(object):
   ...     def __init__(self, x, y):
   ...         self.x = x
   ...         self.y = y
   ...
   >>> point = Point(0, 1)
   >>> point.x
   0
   >>> point.y
   1

Vytvoř speciální destrukční metodu, která se zavolá před smazáním objektu::

   >>> class Point(object):
   ...     def __del__(self):
   ...         print("Good bye")
   ...
   >>> point = Point()
   >>> del point
   Good bye

Vytvoř normální metodu pro výpočet vzdálenosti dvou bodů::

   >>> class Point(object):
   ...     def __init__(self, x, y):
   ...         self.x = x
   ...         self.y = y
   ...     def distance_from_point(self, point):
   ...         if not isinstance(point, Point):
   ...             raise TypeError(f"point must be a Point, not {point.__class__.__name__}")
   ...         return ((point.x - self.x) ** 2 + (point.y - self.y) ** 2) ** 0.5
   ...
   >>> a = Point(0, 0)
   >>> b = Point(3, 3)
   >>> a.distance_from_point(0)
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "<stdin>", line 7, in distance_from_point
   TypeError: point must be a Point, not int
   >>> a.distance_from_point(b)
   4.242640687119285

Vytvoř normální metody, které lze řetězit za sebou::

   >>> class Account(object):
   ...     def __init__(self, balance=0):
   ...         self.balance = balance
   ...     def deposit(self, amount):
   ...         self.balance += amount
   ...         return self
   ...     def withdraw(self, amount):
   ...         self.balance -= amount
   ...         return self
   ...
   >>> account = Account(100)
   >>> account.withdraw(50).deposit(25).withdraw(75)
   >>> account.balance
   0

.. note::

   U každé metody je nutné zpravidla definovat počateční parametr ``self``, do
   kterého Python vloží instanci objektu. Pomocí ``self`` objektu pak lze
   přistupovat k atributům uvnitř metod nebo volat jiné metody.

.. tip::

   Defaultní atributy, respektive proměnné na instanci by neměly obsahovat
   měnitelné datové typy jako jsou seznamy, množiny či slovníky, pokud s těmito
   hodnotami pracují metody::

      >>> class Dog(object):
      ...     tricks = []
      ...     def __init__(self, name):
      ...         self.name = name
      ...     def add_trick(self, trick):
      ...         self.tricks.append(trick)
      ...
      >>> a = Dog("Charlie")
      >>> b = Dog("Maggie")
      >>> a.add_trick("sit")
      >>> b.add_trick("down")
      >>> a.tricks
      ['sit', 'down']
      >>> b.tricks
      ['sit', 'down']

   Měnitelné typy je třeba přesunout konstruktor, respektive inicializační
   metodu::

      >>> class Dog(object):
      ...     def __init__(self, name):
      ...         self.name = name
      ...         self.tricks = []
      ...     def add_trick(self, trick):
      ...         self.tricks.append(trick)
      ...
      >>> a = Dog("Charlie")
      >>> b = Dog("Maggie")
      >>> a.add_trick("sit")
      >>> b.add_trick("down")
      >>> a.tricks
      ['sit']
      >>> b.tricks
      ['down']

Odbočka k reprezentaci objektu
""""""""""""""""""""""""""""""

Každá vlastní třída má zpravidla definovanou i speciální metodu ``__repr__``,
která zobrazí popisek objektu::

   >>> class Point(object):
   ...     def __init__(self, x, y):
   ...         self.x = x
   ...         self.y = y
   ...
   >>> a = Point(0, 0)
   >>> a
   <__main__.Point object at 0x7fd9140ecb70>
   >>> class Point(object):
   ...     def __init__(self, x, y):
   ...         self.x = x
   ...         self.y = y
   ...     def __repr__(self):
   ...         return f"<Point [{self.x}, {self.y}]"
   ...
   >>> a = Point(0, 0)
   >>> a
   <Point [0, 0]>

Pro textovou reprezentaci objektu se pak definuje speciální metoda ``__str__``,
kterou si uživatel definuje sám, nejčastěji při dědičnosti::

   >>> class Dog(object):
   ...     def __init__(self, name):
   ...         self.name = name
   ...     def __repr__(self):
   ...         return f"<Dog '{self.name}'>"
   ...     def __str__(self):
   ...         return self.name
   ...
   >>> dog = Dog("Buddy")
   >>> dog
   <Dog 'Buddy'>
   >>> print(dog)
   Buddy
   >>> repr(dog)
   "<Dog 'Buddy'>"
   >>> str(dog)
   'Buddy'

Odbočka k varování
""""""""""""""""""

Uživatele lze varovat, že používá starou funkci či metodu, která se v
budoucnosti smaže a že má používat alternativu::

   >>> from warnings import warn
   >>> def old_function():
   ...     warn("'old_function' is deprecated, use 'new_function' instead")
   ...
   >>> old_function()
   __main__:2: UserWarning: 'old_function' is deprecated, use 'new_function' instead
   >>> def old_function():
   ...     warn("'old_function' is deprecated, use 'new_function' instead", DeprecationWarning)
   ...
   >>> old_function()
   >>> def old_function():
   ...     warn("'old_function' will be deprecated, use 'new_function' instead", PendingDeprecationWarning)
   ...
   >>> old_function()
   >>>

.. note::

   Várování ``DeprecationWarning`` a ``PendingDeprecationWarning`` jsou
   defaultně potlačeny, aby nemátly uživatele. Zobrazit je lze pomocí varovného
   filtru::

      >>> import warnings
      >>> warnings.simplefilter("always")  # show all warnings
      >>> warnings.warn("test", DeprecationError)
      __main__:1: DeprecationWarning: test
      >>> warnings.simplefilter("default")  # show suppressed default warnings
      >>> warnings.warn("test", DeprecationError)
      __main__:1: DeprecationWarning: test

   Varovné hlášky lze taktéž zapnout pomocí volby ``-W`` a patřičného filtr
   argumentu:

   .. code:: none

      $ cat test.py
      import warnings


      def old_function():
          warnings.warn("'old_function' is deprecated, use 'new_function' instead", DeprecationWarning)


      old_function()
      $ python3 -W default test.py
      test.py:5: DeprecationWarning: 'old_function' is deprecated, use 'new_function' instead
        warnings.warn("'old_function' is deprecated, use 'new_function' instead", DeprecationWarning)
      $ python3 -Wd test.py
      test.py:5: DeprecationWarning: 'old_function' is deprecated, use 'new_function' instead
        warnings.warn("'old_function' is deprecated, use 'new_function' instead", DeprecationWarning)

   Hlášky lze kompletně ignorovat nebo je proměnit ve výjimky:

   .. code:: none

      $ python3 -W ignore test.py
      $ python3 -Wi test.py
      $ python3 -q
      >>> import warnings
      >>> warnings.simplefilter("ignore")  # for all warnings
      >>> warnings.warn("test")
      >>> warnings.simplefilter("error", UserWarning)  # for this warning
      >>> warnings.warn("test")
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      UserWarning: test
      >>> warnings.warn("test", DeprecationWarning)
      >>>

.. tip::

   Stejně jako výjimky, i varování lze zachytit::

      >>> from warnings import catch_warnings, warn
      >>> with catch_warnings():
      ...     warn("test")
      ...
      >>> with catch_warnings(record=True) as warns:
      ...     warn("test")
      ...     print(warns)
      ...
      [<warnings.WarningMessage object at 0x7f05bdaf7ef0>]
      >>> with catch_warnings(record=True) as warns:
      ...     warn("test")
      ...     print(str(warns[0].message) == "test")
      ...
      True

   Seznam všech varování lze najít `ZDE <https://docs.python.org/3/library/exceptions.html#warnings>`_.

Dědičnost
^^^^^^^^^

Zděd třídu a přidej navíc metodu::

   >>> class Pet(object):
   ...     def __init__(self, name):
   ...         self.name = name
   ...
   >>> class Dog(Pet):
   ...     def bark(self):
   ...         return "Woof! Woof!"
   ...
   >>> dog = Dog()
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: __init__() missing 1 required positional argument: 'name'
   >>> dog = Dog("Buddy")
   >>> dog.bark()
   'Woof Woof!'
   >>> isinstance(dog, Dog)
   True
   >>> isinstance(dog, Pet)
   True
   >>> isinstance(dog, (Dog, Pet))
   True
   >>> issubclass(Dog, Pet)
   True

Zděd třídu a uprav inicializační metodu pro příjem dalších argumentů::

   >>> class Pet(object):
   ...     def __init__(self, name):
   ...         self.name = name
   ...
   >>> class Dog(Pet):
   ...     def __init__(self, name, breed):
   ...         super().__init__(name)
   ...         self.breed = breed
   ...
   >>> dog = Dog("Buddy")
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: __init__() missing 1 required positional argument: 'breed'
   >>> dog = Dog("Buddy", "Siberian Husky")
   >>> dog.name
   'Buddy'
   >>> dog.breed
   'Siberian Husky'

Zděd třídu a přepiš původní chování metody::

   >>> class Pet(object):
   ...     def __init__(self, name):
   ...         self.name = name
   ...     def talk(self):
   ...         raise NotImplementedError
   ...
   >>> pet = Pet("Buddy")
   >>> pet.talk()
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "<stdin>", line 5, in talk
   NotImplementedError
   >>> class Dog(Pet):
   ...     def talk(self):
   ...         return "Woof! Woof!"
   ...
   >>> dog = Dog("Buddy")
   >>> dog.talk()
   'Woof! Woof!'

.. note::

   Zabudovaná funkce ``super`` umí volat atributy a metody na předkovi, tj. na
   třídě, která byla zděděna.

.. tip::

   Dědit lze i z několika tříd najednou::

      >>> class Base3(object): pass
      ...
      >>> class Base2(object): pass
      ...
      >>> class Base1(object): pass
      ...
      >>> class Base(Base1, Base2, Base3): pass
      ...
      >>>

   Nicméně při několika násobné dědičnosti může vzniknout chaos, kdy se ztratí
   přehled o tom, jaké atributy a metody a na jaké třídě se budou vlastně
   volat.

   Místo několika násobně dedičnosti lze použit kompozici, kdy atributy objektu
   mohou obsahovat jiné objekty::

      >>> class Salary(object):
      ...     def __init__(self, amount):
      ...         self.amount = amount
      ...     def net_salary(self):
      ...         return self.amount * 0.80
      ...
      >>> class Employee(object):
      ...     def __init__(self, name, salary):
      ...         self.name = name
      ...         self.salary = Salary(salary)
      ...
      >>> employee = Employee("Davie", 1000)
      >>> employee.name
      'Davie'
      >>> employee.salary
      <__main__.Salary object at 0x7f91f25ddd68>
      >>> employee.salary.amount
      1000
      >>> employee.salary.net_salary()
      800

Modifikace tříd
---------------

Deskriptory
^^^^^^^^^^^

Vytvoř deskriptor pro validaci vstupních hodnot při inicializaci objektu::

   >>> class NonNegativeInteger(object):
   ...     def __init__(self, name):
   ...         self.name = name
   ...     def __set__(self, instance, value):
   ...         if value < 1:
   ...             raise ValueError(f"{self.name} must be greater than zero")
   ...         instance.__dict__[self.name] = value
   ...     def __delete__(self, instance):
   ...         del instance.__dict__[self.name]
   >>> class Person(object):
   ...     age = NonNegativeInteger("age")
   ...     def __init__(self, name, age):
   ...         self.name = name
   ...         self.age = age
   >>> p = Person("Davie", 0)
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "<stdin>", line 5, in __init__
     File "<stdin>", line 8, in __set__
   ValueError: age must be greater than zero
   >>> p = Person("Davie", 22)
   >>> p.age
   22
   >>> del p.age
   >>> p.age
   <__main__.NonNegativeInteger object at 0x7f322588a160>

.. note::

   Pokud je vynechána metoda ``__delete__`` na deskriptoru, tak daný atribut
   na instanci nepůjde smazat::

      >>> class NonNegativeInteger(object):
      ...     def __init__(self, name):
      ...         self.name = name
      ...     def __set__(self, instance, value):
      ...         if value < 1:
      ...             raise ValueError(f"{self.name} must be greater than zero")
      ...         instance.__dict__[self.name] = value
      >>> class Person(object):
      ...     age = NonNegativeInteger("age")
      ...     def __init__(self, name, age):
      ...         self.name = name
      ...         self.age = age
      >>> p = Person("Davie", 22)
      >>> p.age
      22
      >>> del p.age
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "<stdin>", line 5, in __init__
      AttributeError: __delete__

   Stejný princip nastane v případě, bude-li chybět metoda ``__set__``.

   Deskriptory zpravidla obsahují jen ``__get__`` metodu (nedatový deskriptor)
   nebo ``__get__`` a ``__set__``, respektive i ``__delete__`` (datový
   deskriptor)::

      >>> class FullName(object):
      ...     def __get__(self, instance, owner):
      ...         if instance is not None:
      ...             return f"{instance.first_name} {instance.last_name}"
      ...         else:
      ...             return self
      ...     def __set__(self, instance, value):
      ...         raise AttributeError("can't set attribute")
      >>> class Person(object):
      ...     full_name = FullName()
      ...     def __init__(self, first_name, last_name):
      ...         self.first_name = first_name
      ...         self.last_name = last_name
      >>> p = Person
      >>> p.full_name
      <__main__.FullName object at 0x7f322589ac50>
      >>> p = Person("Davie", "Badger")
      >>> p.full_name
      'Davie Badger'
      >>> p.full_name = "Jacob Badger"
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "<stdin>", line 8, in __set__
      AttributeError: can't set attribute

.. tip::

   Od verze Python verze 3.6 již není třeba posílat název atributu do
   deskriptoru::

      >>> class Gender(object):
      ...     def __init__(self, options):
      ...         self.options = options
      ...     def __get__(self, instance, owner):
      ...         if instance is not None:
      ...             return instance.__dict__[self.name]
      ...         else:
      ...             return self
      ...     def __set__(self, instance, value):
      ...         if value not in self.options:
      ...             raise ValueError(f"{self.name} must be one of {self.options}")
      ...         instance.__dict__[self.name] = value
      ...     def __set_name__(self, owner, name):
      ...         self.name = name
      >>> class Person(object):
      ...     gender = Gender(["M", "F"])
      ...     def __init__(self, name, gender):
      ...         self.name = name
      ...         self.gender = gender
      >>> p = Person("Davie", "male")
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "<stdin>", line 5, in __init__
        File "<stdin>", line 8, in __set__
      ValueError: gender must be one of ['M', 'F']

Meta třídy
^^^^^^^^^^

Vytvoř meta třídu, která si pamatuje počet volání dané metody::

   >>> from functools import wraps
   >>> class CounterMeta(type):
   ...     def __new__(cls, name, bases, namespace, debug=False):
   ...         if debug:
   ...             print(cls)
   ...             print(name)
   ...             print(bases)
   ...             print(namespace)
   ...         for attr in namespace:
   ...             if not attr.startswith("__") and callable(namespace[attr]):
   ...                 namespace[attr] = cls.count(namespace[attr])
   ...         return type.__new__(cls, name, bases, namespace)
   ...     @staticmethod
   ...     def count(func):  # Decorator
   ...         @wraps(func)
   ...         def wrapper(*args, **kwargs):
   ...             wrapper.count += 1
   ...             return func(*args, **kwargs)
   ...         wrapper.count = 0
   ...         return wrapper
   ...
   >>> class Point(metaclass=CounterMeta):
   ...     def __init__(self, x, y):
   ...         self.x = x
   ...         self.y = y
   ...     def distance_from_zero(self):
   ...         return (self.x ** 2 + self.y ** 2) ** 0.5
   ...
   >>> p = Point(0, 1)
   >>> p.x
   0
   >>> p.y
   1
   >>> p.distance_from_zero()
   1.0
   >>> p.distance_from_zero()
   1.0
   >>> p.distance_from_zero()
   1.0
   >>> p.distance_from_zero.count
   3
   >>> class Point(metaclass=CounterMeta, debug=True):
   ...     def __init__(self, x, y):
   ...         self.x = x
   ...         self.y = y
   ...     def distance_from_zero(self):
   ...         return (self.x ** 2 + self.y ** 2) ** 0.5
   ...
   <class '__main__.CounterMeta'>
   Point
   ()
   {'__module__': '__main__', '__qualname__': 'Point', '__init__': <function Point.__init__ at 0x7fdd5a7f0620>, 'distance_from_zero': <function Point.distance_from_zero at 0x7fdd5a7f06a8>}
   >>> p = Point(0, 1)

Vytvoř meta třídu, která si pamatuje pořadí definovaných atributů na třídě::

   >>> from collections import OrderedDict
   >>> class OrderedMeta(type):
   ...     @classmethod
   ...     def __prepare__(cls, name, bases):  # Structure for namespace
   ...         return OrderedDict()
   ...     def __new__(cls, name, bases, namespace):
   ...         result = type.__new__(cls, name, bases, dict(namespace))
   ...         result._order = [key for key in namespace if not key.startswith("_")]
   ...         return result
   ...
   >>> class Point(metaclass=OrderedMeta):
   ...     z = 0
   ...     y = 1
   ...     x = 0
   ...
   >>> Point._order
   ['z', 'y', 'x']
   >>> Point.a = "a"
   >>> Point._order
   ['z', 'y', 'x']

.. note::

   Pomocí ``type`` objektu lze taktéž dynamicky vytvářet třídy::

      >>> class Point(object):
      ...     x = 0
      ...     y = 1
      ...
      >>> def distance_from_zero(self):
      ...     return (self.x ** 2 + self.y ** 2) ** 0.5
      ...
      >>> Point = type("Point", (object,), {"x": 0, "y": 1, "distance_from_zero": distance_from_zero})
      >>> point = Point()
      >>> point.x
      0
      >>> point.y
      1
      >>> point.distance_from_zero()
      1.0

   Metoda ``__call__`` v ``type`` objektu interně volá metodu ``__new__``,
   která vytvoří instanci dané třídy a posléze metodu ``__init__``, pomocí
   které se upraví atributy této instance.

   Pokud se volá objekt ``type`` jen s jedním argumentem, tak se vrátí daný
   typ objektu::

      >>> type(0)
      <class 'int'>
      >>> type(int)
      <class 'type'>
      >>> type(type)
      <class 'type'>

   Je-li argumentem instance nějakého objektu, vrátí se název třídy, ze které
   tato instance vznikla. Je-li argumentem třída, vrátí se vždy ``type`` třída,
   neboť všechny třídy jsou interně vytvořeny z této meta třidy::

      >>> class Point(object):
      ...     x = 0
      ...     y = 1
      ...
      >>> point = Point()
      >>> type(point)
      <class '__main__.Point'>
      >>> type(Point)
      <class 'type'>

.. tip::

   Povol jen jednu instanci z dané třídy::

      >>> class SingletonMeta(type):
      ...     _instances = None
      ...     def __call__(cls, *args, **kwargs):
      ...         if cls._instances is None:
      ...             cls._instances = type.__call__(cls, *args, **kwargs)
      ...         return cls._instances
      ...
      >>> class Test(metaclass=SingletonMeta):
      ...     pass
      ...
      >>> a = Test()
      >>> b = Test()
      >>> a is b
      True
      >>> id(a) == id(b)
      True
      >>> class Dog(metaclass=Singleton):
      ...     def __init__(self, name):
      ...         self.name = name
      ...
      >>> buddy = Dog("Buddy")
      >>> charlie = Dog("Charlie")
      >>> buddy.name
      'Buddy'
      >>> charlie.name
      'Buddy'

   Singleton lze taktéž vytvořit bez metatřídy pomocí upravení ``__new__``
   metody, avšak na rozdíl od metatřídy se vždy bude volat metoda ``__init__``,
   která může upravit atributy na instanci::

      >>> class Singleton(object):
      ...     _instance = None
      ...     def __new__(cls, *args, **kwargs):
      ...         if cls._instance is None:
      ...             print("Singleton._instance is None")
      ...             cls._instance = object.__new__(cls)
      ...         else:
      ...             print("Singleton._instance is not None")
      ...         return cls._instance
      ...
      >>> class Dog(Singleton):
      ...     def __init__(self, name):
      ...         self.name = name
      ...
      >>> buddy = Dog("Buddy")
      Singleton._instance is None
      >>> charlie = Dog("Charlie")
      Singleton._instance is not None
      >>> buddy.name
      'Charlie'
      >>> charlie.name
      'Charlie'
      >>> buddy is charlie
      True
      >>> id(buddy) == id(charlie)
      True

Abstraktní třídy
^^^^^^^^^^^^^^^^

Vytvoř abstraktní třídu, která poslouží jako rozhraní pro ostatní třídy::

   >>> from abc import ABCMeta, abstractmethod
   >>> class Animal(metaclass=ABCMeta):
   ...     @abstractmethod
   ...     def sound(self):
   ...         pass
   ...
   >>> class Dog(Animal):
   ...     pass
   ...
   >>> d = Dog()
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: Can't instantiate abstract class Dog with abstract methods sound
   >>> Animal.sound.__isabstractmethod__
   True
   >>> Dog.sound.__isabstractmethod__
   True
   >>> class Dog(Animal):
   ...     def sound(self):
   ...         return "Woof! Woof!"
   ...
   >>> d = Dog()
   >>> d.sound()
   'Woof! Woof!'
   >>> Animal.sound.__isabstractmethod__
   True
   >>> Dog.sound.__isabstractmethod__
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   AttributeError: 'function' object has no attribute '__isabstractmethod__'

.. note::

   Abstraktní metody lze použít spolu se zabudovanými dekorátory pro třidu,
   viz `Zabudované dekorátory`_::

      >>> from abc import ABCMeta, abstractmethod
      >>> class Abstract(metaclass=ABCMeta):
      ...     @property
      ...     @abstractmethod
      ...     def abstract_property(self):
      ...         pass
      ...     @staticmethod
      ...     @abstractmethod
      ...     def abstract_static_method(self):
      ...         pass
      ...     @classmethod
      ...     @abstractmethod
      ...     def abstract_class_method(self):
      ...         pass
      ...
      >>>

.. tip::

   Abstraktní třídu lze vytvořít zkráceně pomocí dědičnost z ``ABC`` třídy,
   která už obsahuje v sobě metařídu ``ABCMeta``::

      >>> from abc import ABC, abstractmethod
      >>> class Animal(ABC):
      ...     @abstractmethod
      ...     def sound(self):
      ...         pass
      ...
      >>> class Dog(Animal):
      ...     pass
      ...
      >>> d = Dog()
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      TypeError: Can't instantiate abstract class Dog with abstract methods sound

Datové modely
-------------

Iterátory
^^^^^^^^^

Vytvoř vlastní iterátor, respektive kolekci, nad kterou půjde použít ``for``
smyčka::

   >>> class ToDo(object):
   ...     def __init__(self):
   ...         self._todos = []
   ...         self._index = 0
   ...     def add(self, todo):
   ...         self._todos.append(todo)
   ...     def __iter__(self):
   ...         return self
   ...     def __next__(self):
   ...         if self._index == len(self._todos):
   ...             self._index = 0
   ...             raise StopIteration
   ...         self._index += 1
   ...         return self._todos[self._index - 1]
   ...
   >>> todos = ToDo()
   >>> todos.add("a")
   >>> todos.add("b")
   >>> todos.add("c")
   >>> for todo in todos:
   ...     print(todo)
   a
   b
   c
   >>> list(todos)
   ['a', 'b', 'c']

Vytvoř vlastní iterátor s podporou pro iteraci nad obráceným iterátorem::

   >>> class ToDo(object):
   ...     def __init__(self):
   ...         self._todos = []
   ...         self._index = 0
   ...     def add(self, todo):
   ...         self._todos.append(todo)
   ...     def __iter__(self):
   ...         return self
   ...     def __next__(self):
   ...         if self._index == len(self._todos):
   ...             self._index = 0
   ...             raise StopIteration
   ...         self._index += 1
   ...         return self._todos[self._index - 1]
   ...     def __reversed__(self):
   ...         return reversed(self._todos)
   ...
   >>> todos = ToDo()
   >>> todos.add("a")
   >>> todos.add("b")
   >>> todos.add("c")
   >>> for todo in reversed(todos):
   ...     print(todo)
   c
   b
   a

.. note::

   Iterátory umí automaticky vyhodnocovat, jestli se položka nachází v
   iterátoru nebo ne::

      >>> class Series(object):
      ...     def __init__(self, stop):
      ...         self._stop = stop
      ...     def __iter__(self):
      ...         n = 0
      ...         while n < self._stop:
      ...             yield n
      ...             n += 1
      ...     def __reversed__(self):
      ...         n = self._stop - 1
      ...         while n >= 0:
      ...             yield n
      ...             n -= 1
      ...
      >>> series = Series(3)
      >>> 0 in series
      True
      >>> 3 in series
      False
      >>> 3 not in series
      True
      >>> for number in series:
      ...     print(number)
      ...
      0
      1
      2

.. tip::

   Obsahuje-li objekt interně kolekci hodnot, tak lze přeskočit pamatování
   položek v kolekci pomocí indexů a metodu ``__next__``, avšak metoda
   ``__iter__`` musí vracet iterátor::

      >>> class ToDo(object):
      ...     def __init__(self):
      ...         self._todos = []
      ...     def add(self, todo):
      ...         self._todos.append(todo)
      ...     def __iter__(self):
      ...         return iter(self._todos)
      ...     def __reversed__(self):
      ...         return reversed(self._todos)
      ...
      >>> todos = ToDo()
      >>> todos.add("a")
      >>> todos.add("b")
      >>> todos.add("c")
      >>> for todo in todos:
      ...     print(todo)
      ...
      a
      b
      c
      >>> for todo in todos:
      ...     print(todo)
      ...
      a
      b
      c
      >>> for todo in reversed(todos):
      ...     print(todo)
      ...
      c
      b
      a
      >>> for todo in reversed(todos):
      ...     print(todo)
      ...
      c
      b
      a

Nekonečné iterátory
"""""""""""""""""""

* ``count(start=0, step=1)``

  * vrať iterátor, který generuje do nekonečna čísla od ``start`` s krokem
    ``step``::

       >>> from itertools import count
       >>> i = count(step=-1)
       >>> for _ in range(10):
       ...     next(i)
       ...
       0
       -1
       -2
       -3
       -4
       -5
       -6
       -7
       -8
       -9

* ``cycle(iterable)``

  * vrať iterátor, který nekonečně vrací prvky z ``iterable``::

       >>> from itertools import cycle
       >>> i = cycle("ABC")
       >>> for _ in range(9):
       ...     next(i)
       ...
       'A'
       'B'
       'C'
       'A'
       'B'
       'C'
       'A'
       'B'
       'C'

* ``repeat(object, times=None)``

  * vrať iterátor, kde se ``object`` opakuje ``times`` krát, defaultně
    nekonečně krát::

       >>> from itertools import repeat
       >>> repeat(3)
       repeat(3)
       >>> next(repeat(3))
       3
       >>> list(repeat(3, 3))
       [3, 3, 3]

.. tip::

   Zabudované funkce ``map`` umí pro zadanou funkci rozbalit argumenty z
   vícero iterátorů, dokud nějaký nedojde::

      >>> from operator import mul
      >>> for number in range(1, 11):
      ...     list(map(mul, range(1, 11)))
      ...
      Traceback (most recent call last):
        File "<stdin>", line 2, in <module>
      TypeError: op_mul expected 2 arguments, got 1
      >>> from itertools import repeat
      >>> for number in range(1, 11):
      ...     list(map(mul, range(1, 11), repeat(number)))
      ...
      [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
      [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
      [3, 6, 9, 12, 15, 18, 21, 24, 27, 30]
      [4, 8, 12, 16, 20, 24, 28, 32, 36, 40]
      [5, 10, 15, 20, 25, 30, 35, 40, 45, 50]
      [6, 12, 18, 24, 30, 36, 42, 48, 54, 60]
      [7, 14, 21, 28, 35, 42, 49, 56, 63, 70]
      [8, 16, 24, 32, 40, 48, 56, 64, 72, 80]
      [9, 18, 27, 36, 45, 54, 63, 72, 81, 90]
      [10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

Konečné iterátory
"""""""""""""""""

* ``chain(*iterables)``

  * vrať iterátor, který spojí dohromady ``iterables``::

       >>> from itertools import chain
       >>> chain("ABC", [1, 2, 3])
       <itertools.chain object at 0x7f47fc053e48>
       >>> list(chain("ABC", [1, 2, 3]))
       ['A', 'B', 'C', 1, 2, 3]

* ``chain.from_iterable(iterable)``

  * vrať iterátor, který spojí dohromady vnořené ``iterable`` položky v
    ``iterable``::

       >>> from itertools import chain
       >>> chain.from_iterable(["ABC", [1, 2, 3]])
       <itertools.chain object at 0x7f47fb9954e0>
       >>> list(chain.from_iterable(["ABC", [1, 2, 3]]))
       ['A', 'B', 'C', 1, 2, 3]

* ``filterfalse(predicate, iterable)``

  * vrať iterátor, který pomocí funkce ``predicate`` profiltruje položky z
    ``iterable`` tak, aby položka byla nepravdivá (opak funkce ``filter``)::

       >>> from itertools import filterfalse
       >>> filterfalse(None, [0, 1, "", "2", {}, {3}])
       <itertools.filterfalse object at 0x7fdea34bde80>
       >>> list(filterfalse(None, [0, 1, "", "2", {}, {3}]))
       [0, '', {}]
       >>> list(filterfalse(lambda x: x % 2 == 0, range(10)))
       [1, 3, 5, 7, 9]

* ``islice(iterable, stop)``
* ``islice(iterable, start, stop, step=1)``

  * vrať iterátor, který vrátí jen položky v rozsahu ``start`` a ``stop`` s
    volitelným krokem ``step``, obdobně jako funkce ``range``::

       >>> from itertools import islice
       >>> i<itertools.islice object at 0x7f03c0395e08>
       <itertools.islice object at 0x7f03c0395e08>
       >>> list(islice(range(10), 3))
       [0, 1, 2]
       >>> i = iter(range(10))
       >>> list(islice(i, 3))
       [0, 1, 2]
       >>> list(islice(i, 3))
       [3, 4, 5]
       >>> list(islice(i, 3))
       [6, 7, 8]
       >>> list(islice(i, 3))
       [9]
       >>> list(islice(i, 3))
       []

* ``starmap(function, iterable)``

  * vrať iterátor, který vrací položky z ``iterable`` po aplikaci funkce
    ``function``, avšak na rozdíl od ``map`` funkce, ``iterable`` musí
    obsahovat vnořené ``iterable``::

       >>> from operator import mul
       >>> from itertools import starmap
       >>> z = zip(range(1, 11), range(1, 11))
       >>> starmap(mul, z)
       <itertools.starmap object at 0x7f03c198f860>
       >>> list(starmap(mul, z))
       [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

* ``tee(iterable, n=2)``

  * vrať iterátory v n-tici, které se ``n`` krát vytvoří z ``iterable``::

       >>> from itertools import tee
       >>> i = range(10)
       >>> tee(i)
       (<itertools._tee object at 0x7f03bd179c88>, <itertools._tee object at 0x7f03bd179cc8>)
       >>> t = tee(i)
       >>> next(t[0])
       0
       >>> list(t[0])
       [1, 2, 3, 4, 5, 6, 7, 8, 9]
       >>> list(t[1])
       [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
       >>> list(i)  # origin iterable
       [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
       >>> list(t[0])
       []
       >>> list(t[1])
       []

* ``zip_longest(*iterables, fillvalue=None)``

  * vrať iterátor, který propojí jednotlivé položky v ``iterables`` do n-tic,
    avšak na rozdíl od ``zip`` funkce se zipování neukonči, pokud se nějaký
    ``iterable`` vyčerpá, neboť se doplní do n-tice hodnotou ``fillvalue``::

       >>> from itertools import zip_longest
       >>> a = "ABC"
       >>> b = [0, 1]
       >>> zip_longest(a, b)
       <itertools.zip_longest object at 0x7f47fc0639f8>
       >>> list(zip_longest(a, b))
       [('A', 0), ('B', 1), ('C', None)]

.. note::

   Další funkce pro práci s ``iterable`` objekty lze najíst v knihovně
   ```itertools`` včetně návodu na vytváření vlastních
   `iter funkcí <https://docs.python.org/3/library/itertools.html#itertools-recipes>`_
   nebo v externích balíčcích zaměřené na funkcionální programování.

.. tip::

   Vrať iterátor, který rozseká ``iterable`` na úplné celky o délce ``size`` a
   neúplné zahodí::

      >>> def chunks(iterable, size):
      ...     return zip(*[iter(iterable)] * size)
      ...
      >>> chunks(range(10), 3)
      <zip object at 0x7f3e12c83d48>
      >>> list(chunks(range(10), 3))
      [(0, 1, 2), (3, 4, 5), (6, 7, 8)]

   Vrať iterátor, který rozseká ``iterable`` na úplné celky o délce ``size`` a
   neúplné ponechá na konci::

      >>> from itertools import islice
      >>> def chunks(iterable, size):
      ...     iterator = iter(iterable)
      ...     return iter(lambda: tuple(islice(iterator, size)), ())
      ...
      >>> list(chunks(range(10), 3))
      [(0, 1, 2), (3, 4, 5), (6, 7, 8), (9,)]

   Vrať iterátor, který rozseká ``iterable`` na úplné celky o délce ``size`` a
   neúplné vyplní hodnotou ``fill``::

      >>> from itertools import zip_longest
      >>> def chunks(iterable, size, fillvalue=None):
      ...     return zip_longest(*[iter(iterable)] * size, fillvalue=fillvalue)
      ...
      >>> chunks(range(10), 3)
      <itertools.zip_longest object at 0x7f3e15e9fe58>
      >>> list(chunks(range(10), 3))
      [(0, 1, 2), (3, 4, 5), (6, 7, 8), (9, None, None)]
      >>> list(chunks(range(10), 3, "X"))
      [(0, 1, 2), (3, 4, 5), (6, 7, 8), (9, 'X', 'X')]

   Pokud funkce ``iter`` dostane i druhý argument, tzv. sentinel, tak první
   argument musí být volatelný objekt, který se bude volat tak dlouho, dokud
   se nevrátí hodnota rovna sentinelu::

      >>> with open("test.py") as file:
      ...     for line in iter(file.readline, "\n"):  # Until line == blank line
      ...          print(repr(line))
      ...
      'import itertools\n'

Kombinační iterátory
""""""""""""""""""""

* ``product(*iterables, repeat=1)``

  * vrať iterátor s kartézským součinem mezi ``iterables``::

       >>> from itertools import product
       >>> i = "ABC"
       >>> product(i)
       <itertools.product object at 0x7f745ac8dcf0>
       >>> list(product(i))
       [('A',), ('B',), ('C',)]
       >>> list(product(i, repeat=2))
       [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'B'), ('B', 'C'), ('C', 'A'), ('C', 'B'), ('C', 'C')]
       >>> list(product(i, repeat=3))
       [('A', 'A', 'A'), ('A', 'A', 'B'), ('A', 'A', 'C'), ('A', 'B', 'A'), ('A', 'B', 'B'), ('A', 'B', 'C'), ('A', 'C', 'A'), ('A', 'C', 'B'), ('A', 'C', 'C'), ('B', 'A', 'A'), ('B', 'A', 'B'), ('B', 'A', 'C'), ('B', 'B', 'A'), ('B', 'B', 'B'), ('B', 'B', 'C'), ('B', 'C', 'A'), ('B', 'C', 'B'), ('B', 'C', 'C'), ('C', 'A', 'A'), ('C', 'A', 'B'), ('C', 'A', 'C'), ('C', 'B', 'A'), ('C', 'B', 'B'), ('C', 'B', 'C'), ('C', 'C', 'A'), ('C', 'C', 'B'), ('C', 'C', 'C')]

* ``permutations(iterable, r=None)``

  * vrať iterátor s permutacemi v n-tici::

       >>> from itertools import permutations
       >>> i = "ABC"
       >>> permutations(i)
       <itertools.permutations object at 0x7f745dea2e08>
       >>> list(permutations(i))
       [('A', 'B', 'C'), ('A', 'C', 'B'), ('B', 'A', 'C'), ('B', 'C', 'A'), ('C', 'A', 'B'), ('C', 'B', 'A')]
       >>> list(permutations(i, 1))
       [('A',), ('B',), ('C',)]
       >>> list(permutations(i, 2))
       [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]
       >>> list(permutations(i, 3))
       [('A', 'B', 'C'), ('A', 'C', 'B'), ('B', 'A', 'C'), ('B', 'C', 'A'), ('C', 'A', 'B'), ('C', 'B', 'A')]

* ``combinations(iterable, r)``

  * vrať iterátor se seřazenými kombinacemi bez opakování v n-tici::

       >>> from itertools import combinations
       >>> i = "ABC"
       >>> combinations(i, 1)
       <itertools.combinations object at 0x7f745d7ff458>
       >>> list(combinations(i, 1))
       [('A',), ('B',), ('C',)]
       >>> list(combinations(i, 2))
       [('A', 'B'), ('A', 'C'), ('B', 'C')]
       >>> list(combinations(i, 3))
       [('A', 'B', 'C')]

* ``combinations_with_replacement(iterable, r)``

  * vrať iterátor se seřazenými kombinacemi s opakováním v n-tici::

       >>> from itertools import combinations_with_replacement
       >>> i = "ABC"
       >>> combinations_with_replacement(i, 1)
       <itertools.combinations_with_replacement object at 0x7f745d80c368>
       >>> list(combinations_with_replacement(i, 1))
       [('A',), ('B',), ('C',)]
       >>> list(combinations_with_replacement(i, 2))
       [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'B'), ('B', 'C'), ('C', 'C')]
       >>> list(combinations_with_replacement(i, 3))
       [('A', 'A', 'A'), ('A', 'A', 'B'), ('A', 'A', 'C'), ('A', 'B', 'B'), ('A', 'B', 'C'), ('A', 'C', 'C'), ('B', 'B', 'B'), ('B', 'B', 'C'), ('B', 'C', 'C'), ('C', 'C', 'C')]

Generátory
^^^^^^^^^^

Vytvoř generátor, respektive iterátor z funkce::

   >>> def fibonacci(n):
   ...     a, b = 0, 1
   ...     while a <= n:
   ...         yield a
   ...         a, b = b, a + b
   ...
   >>> fibonacci(100)
   <generator object fibonacci at 0x7faf49e69f68>
   >>> for number in fibonacci(100):
   ...     print(number, end=" ")
   ... else:
   ...     print()
   ...
   0 1 1 2 3 5 8 13 21 34 55 89

Vytvoř generátor, který tahá data z dalšího generátoru::

   >>> def flatten(sequence):
   ...     for item in sequence:
   ...         if isinstance(item, (list, tuple)):
   ...             yield from flatten(item)
   ...         else:
   ...             yield item
   ...
   >>> l = [1, [2, [3, [4, [5]]]]]
   >>> flatten(l)
   <generator object flatten at 0x7faf46c52360>
   >>> list(flatten(l))
   [1, 2, 3, 4, 5]

.. note::

   Generátor automaticky na pozadí vytvoří iterátor s ``__iter__`` a
   ``__next__`` metodou včetně vyvolání ``StopIteration`` výjimky, pokud je
   iterace u konce.

   Na rozdíl od obyčejné funkce pro výpočet fibonacciho posloupnosti generátor
   spotřebovává méně paměti, neboť nepotřebuje v paměti celou posloupnost, ale
   jen její část, kterou postupně interně tahá z cyklu::

      >>> def fibonacci(n):
      ...     a, b = 0, 1
      ...     while a <= n:
      ...         yield a
      ...         a, b = b, a + b
      ...
      >>> fibo = fibonacci(3)
      >>> next(fibo)
      0
      >>> next(fibo)
      1
      >>> next(fibo)
      1
      >>> next(fibo)
      3
      >>> next(fibo)
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      StopIteration

   Pokud je iterace u konce (iterátor je prázdný), lze ``StopIteration`` error
   potlačit pomocí výchozí hodnoty v zabudované funkci ``next``::

      >>> next(iter([]))
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      StopIteration
      >>> next(iter([]), None)
      >>>

.. tip::

   Vytvoř jednorázový generátor pomocí jednořádkového cyklu ``for`` uvnitř
   závorek::

      >>> (number for number in range(10))
      <generator object <genexpr> at 0x7f91f57f5410>
      >>> number for number in range(10)
        File "<stdin>", line 1
          number for number in range(10)
                   ^
      SyntaxError: invalid syntax
      >>> list(number for number in range(10) if number % 2 == 0)
      [0, 2, 4, 6, 8]
      >>> list(True if number % 2 == 0 else False for number in range(10))
      [True, False, True, False, True, False, True, False, True, False]
      >>> sum(number for number in range(11))
      55
      >>> numbers = (number for number in range(10))
      >>> list(numbers)
      [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
      >>> list(numbers)
      []

Kontejnery
^^^^^^^^^^

Emulace objektů, které se chovájí obdobně, jaké zabudované typy, tj. seznamy,
n-tice, množiny, slovníky aj.

Jako pomoc pro vytváření kontejnerů existují abstraktivní třídy ze zabudované
knihovny ``collections.abc``, které umí včas detekovat, jestli nechybí nějaká
magická metoda nebo naopak umí přidat další metody na základě již existujích
metod.

.. note::

   Jestliže kontejner nemá definovanou metodu ``__bool__``, tak se pravdivost
   kontejneru vyhodnotí automaticky pomocí metody ``__len__``. Pokud tato
   metoda vrátí nulu, jedná se o kontejner nepravdivý a naopak (>= 1).

Sekvence
""""""""

Vytvoř napodobeninu neměnitelné n-tice::

   >>> from collections.abc import Sequence
   >>> class Tuple(Sequence):
   ...     def __init__(self, *args):
   ...         self._tuple = args
   ...     def __contains__(self, item):
   ...         return item in self._tuple
   ...     def __getitem__(self, key):
   ...         return self._tuple[key]
   ...     def __iter__(self):
   ...         return iter(self._tuple)
   ...     def __len__(self):
   ...         return len(self._tuple)
   ...
   >>> t = Tuple(1, 2, 3)
   >>> 1 in t
   True
   >>> 0 not in t
   True
   >>> t[0]
   1
   >>> t[-1]
   3
   >>> for item in t:
   ...     print(item)
   ...
   1
   2
   3
   >>> len(t)
   3
   >>> reversed(t)
   <generator object Sequence.__reversed__ at 0x7f062ed6a678>
   >>> list(reversed(t))
   [3, 2, 1]
   >>> list(filter(lambda attr: not attr.startswith("_"), dir(t)))
   ['count', 'index']

Vytvoř napodobeninu měnitelného seznamu::

   >>> from collections.abc import MutableSequence
   >>> class List(MutableSequence):
   ...     def __init__(self, *args):
   ...         self._list = list(args)
   ...     def __contains__(self, item):
   ...         return item in self._list
   ...     def __delitem__(self, index):
   ...         del self._list[index]
   ...     def __getitem__(self, index):
   ...         return self._list[index]
   ...     def __iter__(self):
   ...         return iter(self._list)
   ...     def __len__(self):
   ...         return len(self._list)
   ...     def __setitem__(self, index, value):
   ...         self._list[index] = value
   ...     def __repr__(self):
   ...         return f"<List {self._list}>"
   ...     def insert(self, index, value):
   ...         self._list.insert(index, value)
   ...
   >>> l = List(1, 2, 3)
   >>> 1 in l
   True
   >>> 0 not in l
   True
   >>> del l[0]
   >>> l[0]
   2
   >>> for item in l
   ...     print(item)
   ...
   2
   3
   >>> len(l)
   2
   >>> l[0] = 1
   >>> l
   <List [1, 3]>
   >>> l.insert(1, 2)
   >>> l
   <List [1, 2, 3]>
   >>> reversed(l)
   <generator object Sequence.__reversed__ at 0x7f062ed6a678>
   >>> list(reversed(l))
   [3, 2, 1]
   >>> list(filter(lambda attr: not attr.startswith("_"), dir(l)))
   ['append', 'clear', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse']

.. note::

   Metody ``__getitem__``, ``__setitem__`` a ``__delitem__``. by měly vyvolat
   ``TypeError`` výjimku, pokud požadovaný index není celé číslo nebo objekt
   ``Slice``.

   Jestlíže je index celé číslo a je mimo rozmezí sekvence, měla by se vyvolat
   ``IndexError`` výjimka.

.. tip::

   Sčítání a násobení sekvenci celými čísly::

      >>> from collections.abc import Sequence
      >>> class Tuple(Sequence):
      ...     def __init__(self, *args):
      ...         if args and len(args) == 1 and isinstance(args, tuple):
      ...             self._tuple = args[0]
      ...         else:
      ...             self._tuple = args
      ...     def __contains__(self, item):
      ...         return item in self._tuple
      ...     def __getitem__(self, key):
      ...         return self._tuple[key]
      ...     def __iter__(self):
      ...         return iter(self._tuple)
      ...     def __len__(self):
      ...         return len(self._tuple)
      ...     def __add__(self, other):
      ...         if not isinstance(other, Tuple):
      ...             return NotImplemented
      ...         return Tuple(self._tuple + other._tuple)
      ...     def __radd__(self, other):
      ...         return self.__add__(other)
      ...     def __mul__(self, other):
      ...         if not isinstance(other, int):
      ...             return NotImplemented
      ...         return Tuple(self._tuple * other)
      ...     def __rmul__(self, other):
      ...         return self.__mul__(other)
      ...     def __repr__(self):
      ...         return f"<Tuple {self._tuple}>"
      ...
      >>> t = Tuple(1, 2, 3)
      >>> t
      <Tuple (1, 2, 3)>
      >>> u = Tuple(4, 5, 6)
      >>> t + u
      <Tuple (1, 2, 3, 4, 5, 6)>
      >>> u + t
      <Tuple (4, 5, 6, 1, 2, 3)>
      >>> t * 2
      <Tuple (1, 2, 3, 1, 2, 3)>
      >>> 2 * t
      <Tuple (1, 2, 3, 1, 2, 3)>

Množiny
"""""""

Vytvoř napodobeninu neměnitelné množiny::

   >>> from collections.abc import Set
   >>> class ImmutableSet(Set):
   ...     def __init__(self, *args):
   ...         self._set = set(args)
   ...     def __contains__(self, item):
   ...         return item in self._set
   ...     def __iter__(self):
   ...         return iter(self._set)
   ...     def __len__(self):
   ...         return len(self._set)
   ...
   >>> s = ImmutableSet(1, 1, 1)
   >>> 1 in s
   True
   >>> 0 not in s
   True
   >>> for item in s:
   ...     print(item)
   ...
   1
   >>> len(s)
   1
   >>> t = ImmutableSet(2, 3)
   >>> s == t
   False
   >>> s & t
   <__main__.ImmutableSet object at 0x7f062ed7f438>
   >>> list(filter(lambda attr: not attr.startswith("_"), dir(s)))
   ['isdisjoint']

Vytvoř napodobeninu měnitelné množiny::

   >>> from collections.abc import MutableSet
   >>> class MutableSetCollection(MutableSet):
   ...     def __init__(self, *args):
   ...         self._set = set(args)
   ...     def __contains__(self, item):
   ...         return item in self._set
   ...     def __iter__(self):
   ...         return iter(self._set)
   ...     def __len__(self):
   ...         return len(self._set)
   ...     def __repr__(self):
   ...         return f"<MutableSetCollection {self._set}>"
   ...     def add(self, value):
   ...         self._set.add(value)
   ...     def discard(self, value):
   ...         self._set.discard(value)
   ...
   >>> s = MutableSetCollection()
   >>> len(s)
   0
   >>> s.add(1)
   >>> s
   <MutableSetCollection {1}>
   >>> s.discard(1)
   >>> s
   <MutableSetCollection set()>
   >>> s.add(0)
   >>> t = MutableSetCollection(1)
   >>> s & t
   <MutableSetCollection {<generator object Set.__and__.<locals>.<genexpr> at 0x7f062ed6a2b0>}>
   >>> list(filter(lambda attr: not attr.startswith("_"), dir(s)))
   ['add', 'clear', 'discard', 'isdisjoint', 'pop', 'remove']

.. note::

   Pro správné zobrazení výsledků množinových operací je třeba upravit
   metody pro sjednocení (``__or__``), průnik (``__and__``), rozdíl
   (``__sub__``) a doplněk (``__xor__``)::

      >>> from collections.abc import Set
      >>> class ImmutableSet(Set):
      ...     def __init__(self, *args):
      ...         if args and len(args) == 1 and isinstance(args[0], set):
      ...             self._set = args[0]
      ...         else:
      ...             self._set = set(args)
      ...     def __contains__(self, item):
      ...         return item in self._set
      ...     def __iter__(self):
      ...         return iter(self._set)
      ...     def __len__(self):
      ...         return len(self._set)
      ...     def __or__(self, other):
      ...         return ImmutableSet(self._set | other._set)
      ...     def __repr__(self):
      ...         return f"<ImmutableSet {self._set}>"
      ...
      >>> s = ImmutableSet(0)
      >>> t = ImmutableSet(1)
      >>> s | t
      <ImmutableSet {0, 1}>

Slovníky
""""""""

Vytvoř napodobeninu neměnitelného slovníku::

   >>> from collections.abc import Mapping
   >>> class ImmutableDict(Mapping):
   ...     def __init__(self, **kwargs):
   ...         self._dict = kwargs
   ...     def __contains__(self, key):
   ...         return key in self._dict
   ...     def __getitem__(self, key):
   ...         return self._dict[key]
   ...     def __iter__(self):
   ...         return iter(self._dict.keys())
   ...     def __len__(self):
   ...         return len(self._dict)
   ...
   >>> d = ImmutableDict(name="Davie", age=22)
   >>> "name" in d
   True
   >>> "gender" not in d
   True
   >>> d["age"]
   22
   >>> for key in d:
   ...     print(key)
   ...
   name
   age
   >>> len(d)
   2
   >>> bool(d)
   True
   >>> list(filter(lambda attr: not attr.startswith("_"), dir(d)))
   ['get', 'items', 'keys', 'values']
   >>> d["age"] = 23
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: 'ImmutableDict' object does not support item assignment
   >>> del d["age"]
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: 'ImmutableDict' object does not support item assignment

Vytvoř napodobeninu měnitelného slovníku::

   >>> from collections.abc import MutableMapping
   >>> class MutableDict(MutableMapping):
   ...     def __init__(self, **kwargs):
   ...         self._dict = kwargs
   ...     def __contains__(self, key):
   ...         return key in self._dict
   ...     def __delitem__(self, key):
   ...         del self._dict[key]
   ...     def __getitem__(self, key):
   ...         return self._dict[key]
   ...     def __iter__(self):
   ...         return iter(self._dict.keys())
   ...     def __len__(self):
   ...         return len(self._dict)
   ...     def __setitem__(self, key, value):
   ...         self._dict[key] = value
   ...
   >>> d = MutableDict()
   >>> d["name"] = "Davie"
   >>> d["name"]
   'Davie'
   >>> del d["name"]
   >>> d["name"]
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "<stdin>", line 9, in __getitem__
   KeyError: 'name'
   >>> list(filter(lambda attr: not attr.startswith("_"), dir(d)))
   ['clear', 'get', 'items', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values']

.. note::

   Pokud se klíč nenachází ve slovníků, měla by metoda ``__getitem__`` vyvolat
   ``KeyError`` výjimku. Stejný princip lze uplatnit u ``__setitem__`` nebo
   ``__delitem__``.

.. tip::

   Pokud se klíč nenachází ve slovníků, lze vrátit nějakou výchozí hodnotu
   pomocí metody ``__missing__``::

      >>> class Dict(object):
      ...     def __init__(self, **kwargs):
      ...         self._dict = kwargs
      ...     def __getitem__(self, key):
      ...         if key not in self._dict:
      ...             return self.__missing__(key)
      ...         return self._dict[key]
      ...     def __missing__(self, key):
      ...         return 0
      ...
      >>> d = Dict()
      >>> d["test"]
      0

Odbočka k přístupu k atributům
""""""""""""""""""""""""""""""

Povol přístupování ke klíčům slovníků i přes atributy::

   >>> class SuperDict(dict):
   ...     def __getattr__(self, name):
   ...         try:
   ...             return dict.__getitem__(self, name)
   ...         except KeyError:
   ...             raise AttributeError(f"'{self.__class__.__name__}' object has no attribute '{name}'")
   ...
   >>> d = SuperDict(a=0)
   >>> d["a"]
   >>> d.a
   0
   >>> d.b
   Traceback (most recent call last):
     File "<stdin>", line 4, in __getattr__
   KeyError: 'b'

   During handling of the above exception, another exception occurred:

   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "<stdin>", line 6, in __getattr__
   AttributeError: 'SuperDict' object has no attribute 'b'
   >>> getattr(d, "b", 1)
   >>> d.pop
   <built-in method pop of SuperDict object at 0x7f4886801f68>
   >>> d.pop("a")
   0
   >>> d
   {}
   >>> d.keys()
   dict_keys([])

Povol změnu hodnotu klíčů přes atribut::

   >>> class SuperDict(dict):
   ...     def __getattr__(self, name):
   ...         try:
   ...             return dict.__getitem__(self, name)
   ...         except KeyError:
   ...             raise AttributeError(f"'{self.__class__.__name__}' object has no attribute '{name}'")
   ...     def __setattr__(self, name, value):
   ...         dict.__setitem__(self, name, value)
   ...
   >>> d = SuperDict(a=0)
   >>> d.a
   0
   >>> d.a = 1
   >>> d.a
   1
   >>> setattr(d, "b", 2)
   >>> d
   {'a': 1, 'b': 2}
   >>> d.pop = 3
   >>> d.pop
   <built-in method pop of SuperDict object at 0x7f48835b19e8>
   >>> d
   {'a': 1, 'b': 2, 'pop': 3}
   >>> d.pop("pop")
   3

Povol mázání klíčů přes atribut::

   >>> class SuperDict(dict):
   ...     def __getattr__(self, name):
   ...         try:
   ...             return dict.__getitem__(self, name)
   ...         except KeyError:
   ...             raise AttributeError(f"'{self.__class__.__name__}' object has no attribute '{name}'")
   ...     def __delattr__(self, name):
   ...         try:
   ...             dict.__delitem__(self, name)
   ...         except KeyError:
   ...             raise AttributeError(f"{name}")
   ...
   >>> d = SuperDict(a=0)
   >>> d.a
   0
   >>> del d.a
   >>> d
   {}
   >>> del d.a
   Traceback (most recent call last):
     File "<stdin>", line 9, in __delattr__
   KeyError: 'a'

   During handling of the above exception, another exception occurred:

   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "<stdin>", line 11, in __delattr__
   AttributeError: a
   >>> d
   {}
   >>> del d.pop
   Traceback (most recent call last):
     File "<stdin>", line 9, in __delattr__
   KeyError: 'pop'

   During handling of the above exception, another exception occurred:

   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "<stdin>", line 11, in __delattr__
   AttributeError: pop
   >>> d.pop
   <built-in method pop of SuperDict object at 0x7f4886801f68>

.. note::

   Pro volání původních magických metod je lepší místo zabudované funkce
   ``super`` volat explicitně předka, např. ``dict.__setattr__`` nebo u
   vlastních objektů skrze ``object.__setattr__``.

   Volání metod ``__getattr__``, ``__setattr__`` a ``__delattr__`` lze také
   kromě volání těchto verzi na předcích přeskočit díky přímé manipulaci
   atributů uložených v ``__dict__``::

      >>> class Dog(object):
      ...     def __init__(self, name):
      ...         self.name = name
      ...     def __setattr__(self, name, value):
      ...         raise AttributeError("Forbidden")
      ...
      >>> dog = Dog("Buddy")
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "<stdin>", line 3, in __init__
        File "<stdin>", line 5, in __setattr__
      AttributeError: Forbidden
      >>> class Dog(object):
      ...     def __init__(self, name):
      ...         object.__setattr__(self, "name", name)
      ...     def __setattr__(self, name, value):
      ...         raise AttributeError("Forbidden")
      ...
      >>> dog = Dog("Buddy")
      >>> dog.name
      'Buddy'
      >>> class Dog(object):
      ...     def __init__(self, name):
      ...         self.__dict__["name"] = name
      ...     def __setattr__(self, name, value):
      ...         raise AttributeError("Forbidden")
      ...
      >>> dog = Dog("Buddy")
      >>> dog.name
      'Buddy'

.. tip::

   Pomocí metody ``__dir__`` lze upravit introspekci atributů na objektu::

      >>> class SuperDict(dict):
      ...     def __getattr__(self, name):
      ...         try:
      ...             return dict.__getitem__(self, name)
      ...         except KeyError:
      ...             raise AttributeError(f"'{self.__class__.__name__}' object has no attribute '{name}'")
      ...     def __dir__(self):
      ...         return set(dict.__dir__(self) + list(self.keys()))
      ...
      >>> d = SuperDict(a=0, pop=1)
      >>> dir(d)
      ['__class__', '__contains__', '__delattr__', '__delitem__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattr__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'a', 'clear', 'copy', 'fromkeys', 'get', 'items', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values']
      >>> "a" in dir(d)
      True
      >>> d.pop
      <built-in method pop of SuperDict object at 0x7f48835b1b48>

   Ve vlastní metodě ``__dir__`` stačí vrátit sekvenci, přičemž Python si sám
   tuto sekveni převede na seznam a položky v něm seřadí.

Čísla
^^^^^

Vytvoř číselný objekt s podporou pro základní aritmetické operace::

   >>> class Number(object):
   ...     def __init__(self, value):
   ...         self._value = value
   ...     def __add__(self, other):
   ...         if isinstance(other, Number):
   ...             return Number(self._value + other._value)
   ...         return Number(self._value + other)
   ...     def __sub__(self, other):
   ...         if isinstance(other, Number):
   ...             return Number(self._value - other._value)
   ...         return Number(self._value - other)
   ...     def __mul__(self, other):
   ...         if isinstance(other, Number):
   ...             return Number(self._value * other._value)
   ...         return Number(self._value * other)
   ...     def __truediv__(self, other):
   ...         if isinstance(other, Number):
   ...             return Number(self._value / other._value)
   ...         return Number(self._value / other)
   ...     def __floordiv__(self, other):
   ...         if isinstance(other, Number):
   ...             return Number(self._value // other._value)
   ...         return Number(self._value // other)
   ...     def __mod__(self, other):
   ...         if isinstance(other, Number):
   ...             return Number(self._value % other._value)
   ...         return Number(self._value % other)
   ...     def __divmod__(self, other):
   ...         if isinstance(other, Number):
   ...             return divmod(self._value, other._value)
   ...         return divmod(self._value, other)
   ...     def __pow__(self, other):
   ...         if isinstance(other, Number):
   ...             return Number(self._value ** other._value)
   ...         return Number(self._value ** other)
   ...     def __repr__(self):
   ...         return f"<Number {self._value}>"
   ...
   >>> n = Number(3)
   >>> n
   <Number 3>
   >>> n + 3
   <Number 6>
   >>> n - 3
   <Number 0>
   >>> n * 3
   <Number 9>
   >>> n / 3
   <Number 1.0>
   >>> n // 3
   <Number 1>
   >>> divmod(n, 2)
   (1, 1)
   >>> n ** 2
   <Number 9>

Vytvoř číselný objekt s podporou pro unární operace::

   >>> class Number(object):
   ...     def __init__(self, value):
   ...         self._value = value
   ...     def __pos__(self):
   ...         return Number(+(self._value))
   ...     def __neg__(self):
   ...         return Number(-(self._value))
   ...     def __abs__(self):
   ...         return Number(abs(self._value))
   ...     def __repr__(self):
   ...         return f"<Number {self._value}>"
   ...
   >>> n = Number(-3)
   >>> +n
   <Number -3>
   >>> -n
   <Number 3>
   >>> abs(n)
   <Number 3>

Vytvoř číselný objekt s podporou pro zabudované číselné funkce::

   >>> class Number(object):
   ...     def __init__(self, value):
   ...         self._value = value
   ...     def __int__(self):
   ...         return int(self._value)
   ...     def __float__(self):
   ...         return float(self._value)
   ...     def __round__(self, ndigits=None):
   ...         return Number(round(self._value, ndigits))
   ...     def __repr__(self):
   ...         return f"<Number {self._value}>"
   ...
   >>> n = Number(3.3)
   >>> int(n)
   3
   >>> float(n)
   3.3
   >>> round(n, 1)
   <Number 3.3>

.. note::

   Pokud je u operací s čísly nalevo jiný datový typ a napravo vlastní číselný
   objekt, tak operace nebude povolena, dokud se nenaimplementuje patřičná
   obrácená metoda::

      >>> class Number(object):
      ...     def __init__(self, value):
      ...         self._value = value
      ...     def __add__(self, other):
      ...         if isinstance(other, Number):
      ...             return Number(self._value + other._value)
      ...         return Number(self._value + other)
      ...     def __radd__(self, other):
      ...         return self.__add__(other)
      ...     def __repr__(self):
      ...         return f"<Number {self._value}>"
      ...
      >>> n = Number(0)
      >>> 1 + n
      <Number 1>

   Operace se zkráceným přiřazením hodnot do proměnné automaticky volají na
   pozadí patřičné callbackové metody, aniž by bylo např. nutné implementovat
   vlastní ``__iadd__`` metodu::

      >>> class Number(object):
      ...     def __init__(self, value):
      ...         self._value = value
      ...     def __add__(self, other):
      ...         if isinstance(other, Number):
      ...             return Number(self._value + other._value)
      ...         return Number(self._value + other)
      ...     def __repr__(self):
      ...         return f"<Number {self._value}>"
      ...
      >>> n = Number(0)
      >>> n += 1
      >>> n
      <Number 1>

   Ostatní metody včetně podpory pro bínární operace ``&``, ``^``, ``|`` aj.
   lze nalézt `ZDE <https://docs.python.org/3.6/reference/datamodel.html#emulating-numeric-types>`_

.. tip::

   Pokud není v číselném objektu definována speciální metoda pro určitou
   operaci, tak daná operace nebude fungovat, neboť není implementována.

   Stejné nefunkčnosti operace lze docílit, pokud je u operací použit
   nevhodný typ::

      >>> class Number(object):
      ...     def __init__(self, value):
      ...         self._value = value
      ...     def __add__(self, other):
      ...         if isinstance(other, Number):
      ...             return Number(self._value + other._value)
      ...         elif isinstance(other, (int, float)):
      ...             return Number(self._value + other)
      ...         else:
      ...             return NotImplemented
      ...     def __repr__(self):
      ...         return f"<Number {self._value}>"
      ...
      >>> n = Number(3)
      >>> n + Number(3)
      <Number 6>
      >>> n + 3
      <Number 6>
      >>> n + 3.0
      <Number 6.0>
      >>> n + "3"
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      TypeError: unsupported operand type(s) for +: 'Number' and 'str'

Odbočka k porovnávání objektů
"""""""""""""""""""""""""""""

Povol použití relačních operátorů na vlastní objekty::

   >>> class Number(object):
   ...     def __init__(self, value):
   ...         self._value = value
   ...
   >>> x = Number(0)
   >>> y = Number(1)
   >>> x < y
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: '<' not supported between instances of 'Number' and 'Number'
   >>> class Number(object):
   ...     def __init__(self, value):
   ...         self._value = value
   ...     def __lt__(self, other):
   ...         return isinstance(other, Number) and self._value < other._value
   ...     def __le__(self, other):
   ...         return isinstance(other, Number) and self._value <= other._value
   ...     def __eq__(self, other):
   ...         return isinstance(other, Number) and self._value == other._value
   ...
   >>> x = Number(0)
   >>> y = Number(1)
   >>> x < y
   True
   >>> x <= y
   True
   >>> x == y
   False
   >>> x != y
   True
   >>> x > y
   False
   >>> x >= y
   False

.. note::

   Relační magické metody mohou taktéž vracet ``NotImplemented`` objekt,
   avšak žádná výjimka se nevyvolá u porovnávání různých objektů, neboť Python
   bude místo ``NotImplemented`` hodnoty pracovat s ``__bool__`` hodnotou::

      >>> class Number(object):
      ...     def __init__(self, value=0):
      ...         self._value = value
      ...     def __eq__(self, other):
      ...         if not isinstance(other, Number):
      ...             return NotImplemented
      ...         return self._value == other._value
      ...
      >>> n = Number()
      >>> n._value
      0
      >>> n == 0
      False
      >>> bool(n)
      True
      >>> True == 0
      False

   Pokud už je definována vlastní ``__eq__``, tak se objekt stane
   nehashovatelným a nepůjde jej použít jako prvek v množine nebo klíč ve
   slovníku, neboť tyto datové typy pracují s hashovací tabulkou::

      >>> class Test(object):
      ...     pass
      ...
      >>> hash(Test)
      -9223372036852324379
      >>> t = Test()
      >>> hash(t)
      -9223363262430825023
      >>> {1, 2, 3, t}
      {1, 2, 3, <__main__.Test object at 0x7faf46c35c18>}
      >>> class Number(object):
      ...     def __init__(self, value):
      ...         self._value = value
      ...     def __eq__(self, other):
      ...         return isinstance(other, Number) and self._value == other._value
      ...
      >>> hash(Number)
      -9223372036852324213
      >>> n = Number(0)
      >>> hash(n)
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      TypeError: unhashable type: 'Number'
      >>> {n: 0}
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      TypeError: unhashable type: 'Number'
      >>> {0: 0}
      {0: 0}

   Hashovatelné jsou všechny neměnitelný objekty a vlastní objekty bez upravené
   ``__eq__`` metody. Pokud se vlastní objekt chová jako neměnitelný datový typ
   a má vlastní ``__eq__`` metodu, měl by mít i vlastní ``__hash__`` metodu::

      >>> class Point(object):
      ...     __slots__ = ["x", "y"]
      ...     def __init__(self, x, y):
      ...         object.__setattr__(self, "x", x)
      ...         object.__setattr__(self, "y", y)
      ...     def __setattr__(self, name, value):
      ...         if hasattr(self, name):
      ...             raise AttributeError(f"Cannot change value of {name} to {value}")
      ...         else:
      ...             raise AttributeError(f"Cannot set value of {name} to {value}")
      ...     def __delattr__(self, name):
      ...         raise AttributeError(f"Cannot delete {name}")
      ...     def __eq__(self, other):
      ...         return (
      ...             isinstance(other, Point)
      ...             and self.x == other.x
      ...             and self.y == other.y
      ...         )
      ...     def __hash__(self):
      ...         return hash((self.x, self.y))
      ...
      >>> p = Point(0, 1)
      >>> p.x
      0
      >>> p.x = 1
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "<stdin>", line 8, in __setattr__
      AttributeError: Cannot change value of x to 1
      >>> del p.x
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "<stdin>", line 12, in __delattr__
      AttributeError: Cannot delete x
      >>> hash(p)
      3713080549409410656
      >>> {1, 2, 3, p}
      {<__main__.Point object at 0x7faf46bed940>, 1, 2, 3}

   Vlastní objekty, které jsou měnitelné a mají upravenou ``__eq__`` metodu,
   tak implicitně je atribut ``__hash__`` nastaven na ``None``. V žádném
   případě by neměla ``__hash__`` metoda existovat sama bez ``__eq__`` metody.

.. tip::

   Pomocí dekorátoru ``total_ordering`` z knihovny ``functools`` stačí
   vytvořit jen ``__eq__`` a jednu z ``__lt__`` / ``__le__`` / ``__gt__`` /
   ``__ge__`` metod, aby dekorátor sám odvodil ostatní relační operace::

      >>> from functools import total_ordering
      >>> @total_ordering
      ... class Number(object):
      ...     def __init__(self, value=0):
      ...         self._value = value
      ...     def __lt__(self, other):
      ...         return isinstance(other, Number) and self._value < other._value
      ...     def __eq__(self, other):
      ...         return isinstance(other, Number) and self._value == other._value
      ...
      >>> x = Number(0)
      >>> y = Number(1)
      >>> x < y
      True
      >>> x <= y
      True
      >>> x == y
      False
      >>> x != y
      True
      >>> x > y
      False
      >>> x >= y
      False

   Avšak nevýhodou této verze je o něco pomalejší exekuce kódu při porovnávání
   objektů. Nejlepší je explicitně popsat všechny relační operace.

Odbočka k vyhodnocování pravdivosti objektu
"""""""""""""""""""""""""""""""""""""""""""

Nastav pravdivost objektu::

   >>> class Number(object):
   ...     def __init__(self, number):
   ...         self._number = number
   ...     def __repr__(self):
   ...         return str(self._number)
   ...
   >>> x = Number(0)
   >>> x
   0
   >>> bool(x)
   True
   >>> y = Number(1)
   >>> y
   1
   >>> bool(y)
   True
   >>> class Number(object):
   ...     def __init__(self, number):
   ...         self._number = number
   ...     def __bool__(self):
   ...         return self._number != 0
   ...
   >>> x = Number(0)
   >>> bool(x)
   False
   >>> y = Number(-1)
   >>> bool(y)
   True
   >>> z = Number(1)
   >>> bool(z)
   True

.. note::

   Pokud třída nemá definovanou metodu ``__bool__``, ale má aspoň ``__len__``
   metodu, tak pravdivý je každý objekt, jehož návratova hodnota z funkce
   ``len`` na objekt se nerovná nule.

   Bez definovaných metod ``__bool__`` a ``__len__`` je objekt vždy pravdivý.

Kontextový manažer
^^^^^^^^^^^^^^^^^^

Vytvoř vlastní kontextový manažer na způsob funkce ``open``, který na pozadí
otevře soubor před exekucí kódu uvnitř bloku ``with`` a pak jej také na pozadí
zavře::

   >>> class File(object):
   ...     def __init__(self, filename, mode="r"):
   ...         self.filename = filename
   ...         self.mode = mode
   ...     def __enter__(self):
   ...         self.open_file = open(self.filename, self.mode)
   ...         return self.open_file
   ...     def __exit__(self, exc_type, exc_value, traceback):
   ...         self.open_file.close()
   ...
   >>> with File("test.txt", "w") as file:
   ...     file.write("test")
   ...
   4
   >>> with File("text.txt") as file:
   ...     print(file.read())
   ...
   test
   >>> with open("file.txt") as file:
   ...     print(file.read())
   ...
   test

.. note::

   Když uvnitř ``with`` bloku nastane výjimka, tak argumenty pro parametry
   magické metody ``__exit__`` budou obsahovat hodnotu ``None``.

   Parametry v ``__exit__`` metodě lze zkrátit do jednoho, pokud nepotřebuji
   pracovat s výjimkou z ``with`` bloku::

      >>> class File(object):
      ...     def __init__(self, filename, mode="r"):
      ...         self.filename = filename
      ...         self.mode = mode
      ...     def __enter__(self):
      ...         self.open_file = open(self.filename, self.mode)
      ...         return self.open_file
      ...     def __exit__(self, *args):
      ...         self.open_file.close()
      ...
      >>>

.. tip::

   Vytvoř kontextový manažer z generátoru pomocí dekorátoru
   ``contextmanager``::

      >>> from contextlib import contextmanager
      >>> @contextmanager
      ... def open_file(filename, mode="r"):
      ...     print("opening file")
      ...     file = open(filename, mode)
      ...     yield file
      ...     print("closing file")
      ...     file.close()
      ...
      >>> with open_file("test.txt") as file:
      ...     print(file.read())
      ...
      opening file
      test
      closing file

   Pokud nastane uvnitř ``with`` bloku výjimka, tak se nespustí závěrečný kód
   za příkazem ``yield``::

      >>> with open_file("test.txt") as file:
      ...     print(file.read())
      ...     assert 0
      ...
      opening file
      test
      Traceback (most recent call last):
        File "<stdin>", line 3, in <module>
      AssertionError

   Pro ošetření exitového kódu je třeba použít konstrukci ``try/finally``::

      >>> from contextlib import contextmanager
      >>> @contextmanager
      ... def open_file(filename, mode="r"):
      ...     print("opening file")
      ...     file = open(filename, mode)
      ...     try:
      ...         yield file
      ...     finally:
      ...         print("closing file")
      ...         file.close()
      ...
      >>> with open_file("test.txt") as file:
      ...     print(file.read())
      ...     assert 0
      ...
      opening file
      test
      closing file
      Traceback (most recent call last):
        File "<stdin>", line 3, in <module>
      AssertionError

   Vytvoř hybridní kontextový manažer, který lze použít i jako dekorátor::

      >>> import time
      >>> from contexlib import ContextDecorator
      >>> class timeit(ContextDecorator):
      ...     def __enter__(self):
      ...         self.start = time.time()
      ...         return self
      ...     def __exit__(self, *args):
      ...         self.end = time.time()
      ...         print(f"It took {self.end - self.start:.2f} seconds")
      ...
      >>> with timeit():
      ...     time.sleep(1)
      ...
      It took 1.00 seconds
      >>> @timeit()
      ... def sleep(seconds):
      ...     time.sleep(seconds)
      ...
      >>> sleep(3)
      It took 3.00 seconds

Dekorátory
----------

Vlastní dekorátory
^^^^^^^^^^^^^^^^^^

Vytvoř a použij vlastní časovací dekorátor::

   >>> import time
   >>> def timeit(func):
   ...     def wrapper(*args, **kwargs):
   ...         start = time.time()
   ...         func(*args, **kwargs)
   ...         end = time.time()
   ...         print(f"It took {end - start:.2f} seconds")
   ...     return wrapper
   ...
   >>> def sleep(seconds):
   ...     time.sleep(seconds)
   ...
   >>> sleep = timeit(sleep)
   >>> sleep(1)
   It took 1.00 seconds
   >>> @timeit
   ... def sleep(seconds):
   ...     time.sleep(seconds)
   ...
   >>> sleep(1)
   It took 1.00 seconds
   >>> sleep.__name__  # should be 'sleep'
   'wrapper'

Vytvoř a použíj vlastní kešovací dekorátor s návratovou hodnotou::

   >>> def memoize(func):
   ...     cache = {}
   ...     def wrapper(n):
   ...         if n not in cache:
   ...             cache[n] = func(n)
   ...         return cache[n]
   ...     return wrapper
   ...
   >>> @memoize
   ... def recursive_fibonacci(n):
   ...     if n in [0, 1]:
   ...         return n
   ...     else:
   ...         return recursive_fibonacci(n - 1) + recursive_fibonacci(n - 2)
   ...
   >>> recursive_fibonacci(1)
   1
   >>> recursive_fibonacci(10)
   55
   >>> recursive_fibonacci(100)
   354224848179261915075

Vytvoř a použij vlastní dekorátor pro počitání volání funkcí::

   >>> def count(func):
   ...     def wrapper(*args, **kwargs):
   ...         wrapper.count += 1
   ...         return func(*args, **kwargs)
   ...     wrapper.count = 0
   ...     return wrapper
   ...
   >>> @count
   ... def nothing():
   ...     pass
   ...
   >>> nothing()
   >>> nothing()
   >>> nothing()
   >>> nothing.count
   3

Vytvoř a použij vlastní dekorátor, který automaticky spustí kód při dekorování
funkcí::

   >>> decorated_functions = []
   >>> def decorate(func):
   ...     decorated_functions.append(func.__name__)
   ...     return func
   ...
   >>> @decorate
   ... def nothing():
   ...     pass
   ...
   >>> decorated_functions
   ['nothing']

Vytvoř a použij vlastní kešovací dekorátor pomocí třídy s návratou hodnotou::

   >>> class memoize(object):
   ...     def __init__(self, func):
   ...         self.func = func
   ...         self.cache = {}
   ...     def __call__(self, n):
   ...         if n not in self.cache:
   ...             self.cache[n] = self.func(n)
   ...         return self.cache[n]
   ...
   >>> @memoize
   ... def recursive_fibonacci(n):
   ...     if n in [0, 1]:
   ...         return n
   ...     else:
   ...         return recursive_fibonacci(n - 1) + recursive_fibonacci(n - 2)
   ...
   >>> recursive_fibonacci(100)
   354224848179261915075

Vytvoř a použij několik dekorátorů za sebou::

   >>> def bold(func):
   ...     def wrapper(*args, **kwargs):
   ...         return f"<b>{func(*args, **kwargs)}</b>"
   ...     return wrapper
   ...
   >>> def italic(func):
   ...     def wrapper(*args, **kwargs):
   ...         return f"<i>{func(*args, **kwargs)}</i>"
   ...     return wrapper
   >>> @bold
   ... @italic
   ... def say_hello():
   ...     return "Hello"
   ...
   >>> say_hello()
   '<b><i>Hello</i></b>'

.. note::

   Při použití vlastního dekorátoru se změní název dekorované funkce v atributu
   ``__name__`` a taktéž její dokumentace uchována v atributu ``__doc__``.

   Tumuto přepisu lze zabránit pomocí dekorátoru ``wraps`` ze zabudované
   knihovny ``functools``::

      >>> import time
      >>> from functools import wraps
      >>> def timeit(func):
      ...     @wraps(func)
      ...     def wrapper(*args, **kwargs):
      ...         start = time.time()
      ...         func(*args, **kwargs)
      ...         end = time.time()
      ...         print(f"It took {end - start:.2f} seconds")
      ...     return wrapper
      ...
      >>> @timeit
      ... def sleep(seconds):
      ...     time.sleep(seconds)
      ...
      >>> sleep(1)
      It took 1.00 seconds
      >>> sleep.__name__
      'sleep'

   V případě dekorátoru pomocí třídy je třeba použit v inicializační metodě
   funkci ``update_wrapper`` z ``functools``::

      >>> from functools import update_wrapper
      >>> class memoize(object):
      ...     def __init__(self, func):
      ...         self.func = func
      ...         self.cache = {}
      ...         update_wrapper(self, func)
      ...     def __call__(self, n):
      ...         if n not in self.cache:
      ...             self.cache[n] = self.func(n)
      ...         return self.cache[n]
      >>>

   V obou případech má dekorovaná funkce magický atribut ``__wrapped__``, ve
   kterém je ukryta původní funkce bez dekorátorů::

      >>> from functools import wraps
      ... def verbose(func):
      ...     @wraps(func)
      ...     def wrapper(*args, **kwargs):
      ...         print("before function call")
      ...         return func(*args, **kwargs)
      ...     return wrapper
      ...
      >>> @verbose
      ... def add(x, y):
      ...     return x + y
      ...
      >>> add(1, 1)
      before function call
      2
      >>> add.__wrapped__(1, 1)
      2

.. tip::

   Vytvoř a použij dekorátor, který přijímá argumenty::

      >>> import time
      >>> from functools import wraps
      >>> def logit(logfile):
      ...     def decorator(func):
      ...         @wraps(func)
      ...         def wrapper(*args, **kwargs):
      ...             log = f"Calling function '{func.__name__}'"
      ...             print(log)
      ...             with open(logfile, "a") as file:
      ...                 file.write(f"{log}\n")
      ...             return func(*args, **kwargs)
      ...         return wrapper
      ...     return decorator
      ...
      >>> def sleep(seconds):
      ...     print("before sleep")
      ...     time.sleep(seconds)
      ...     print("after sleep")
      >>> sleep = logit("test.log")(sleep)
      >>> sleep(1)
      Calling function 'sleep'
      before sleep
      after sleep
      >>> @logit("test.log")
      ... def sleep(seconds):
      ...     print("before sleep")
      ...     time.sleep(seconds)
      ...     print("after sleep")
      ...
      >>> sleep(1)
      Calling function 'sleep'
      before sleep
      after sleep

Odbočka k memoizaci
"""""""""""""""""""

Pokud se funkce často volá se stejnými argumenty, lze použit memoizaci pro
kešování výsledků. Kromě vlastní implementace memoizace lze použit i dekorátor
``lru_cache`` z ``functools`` knihovny::

   >>> from functools import lru_cache
   >>> @lru_cache(maxsize=None)
   ... def recursive_fibonacci(n):
   ...     if n in [0, 1]:
   ...         return n
   ...     return recursive_fibonacci(n - 1) + recursive_fibonacci(n - 2)
   ...
   >>> [recursive_fibonacci(n) for n in range(10)]
   [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
   >>> recursive_fibonacci.cache_info()
   CacheInfo(hits=16, misses=10, maxsize=None, currsize=10)
   >>> recursive_fibonacci.cache_clear()
   >>> recursive_fibonacci.cache_info()
   CacheInfo(hits=0, misses=0, maxsize=None, currsize=0)

.. note::

   Maximální pamět může být neomezená (``None``) nebo nejlepé omezená s
   mocninami dvojky (2, 4, 8, 16, 32, 64, 128, 256 atd.).

Odbočka k uzávěrám
""""""""""""""""""

Vytvoř uzávěru, která pracuje se zadaným kontextem::

   >>> def validate_countries(countries):
   ...     def validate_country(country):
   ...         return country in countries
   ...     return validate_country
   ...
   >>> validate_country = validate_countries(["CZ", "SK"])
   >>> validate_country("CZ")
   True
   >>> validate_country("PL")
   False
   >>> callable(validate_country)
   True
   >>> callable(validate_countries)
   True
   >>> validate_country.__closure__
   (<cell at 0x7faf49ecc438: list object at 0x7faf46c58108>,)
   >>> validate_country.__closure__[0].cell_contents
   ['CZ', 'SK']

.. note::

   Uzávěru lze vytvořit i pomocí třídy::

      >>> class Multiplier(object):
      ...     def __init__(self, factor):
      ...         self.factor = factor
      ...     def __call__(self, number):
      ...         return self.factor * number
      ...
      >>> multiply_with3 = Multiplier(3)
      >>> multiply_with3(3)
      9
      >>> multiply_with3.factor
      3
      >>> callable(multiply_with3)
      True
      >>> callable(Multiplier)
      True

.. tip::

   Uzávěru lze napodobit pomocí funkce ``partial`` z knihovny ``functools``,
   která vytvoří z jiné funkce předpřipravenou funkci s argumenty::

      >>> from functools import partial
      >>> def multiply(x, y):
      ...     return x * y
      ...
      >>> multiply_with3 = partial(multiply, 3)
      >>> multiply_with3(3)
      9
      >>> callable(multiply_with3)
      True
      >>> multiply_with3.func
      <function multiply at 0x7faf46be9e18>
      >>> multiply_with3.args
      (3,)
      >>> multiply_with3.keywords
      {}

   Stejný princip lze aplikovat i u metod pomocí funkce ``partialmethod``::

      >>> from functools import partialmethod
      >>> class Request(object):
      ...     @staticmethod
      ...     def request(method, **kwargs):
      ...         return method, kwargs
      ...     get = partialmethod(request, "GET")
      ...     post = partialmethod(request, "POST")
      ...     put = partialmethod(request, "PUT")
      ...     patch = partialmethod(request, "PATCH")
      ...     delete = partialmethod(request, "DELETE")
      ...
      >>> Request.get()
      ('GET', {})
      >>> Request.request("POST", name="Davie")
      ('POST', {'name': 'Davie'})

   V případě nanesení ``partial`` funkce na sebe sama není nutné zadávat
   argumenty zleva doprava podle parametrů, ale lze i volně pomocí klíčových
   argumentů::

      >>> from functools import partial
      >>> def multiply(x, y):
      ...     return x * y
      ...
      >>> multiply_with3 = partial(partial, multiply)
      >>> multiply_with3(y=3)
      functools.partial(<function multiply at 0x7f3e26f31ea0>, y=3)
      >>> multiply_with3(y=3)()
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      TypeError: multiply() missing 1 required positional argument: 'x'
      >>> multiply_with3(y=3)(1)
      3

Zabudované dekorátory
^^^^^^^^^^^^^^^^^^^^^

property
""""""""

Vytvoř z metody read-only atribut (property)::

   >>> class Person(object):
   ...     def __init__(self, first_name, last_name):
   ...         self.first_name = first_name
   ...         self.last_name = last_name
   ...     @property
   ...     def full_name(self):
   ...         return f"{self.first_name} {self.last_name}"
   ...
   >>> person = Person("Davie", "Badger")
   >>> person.full_name
   'Davie Badger'
   >>> employee.full_name = "John Doe"
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   AttributeError: can't set attribute
   >>> del employee.full_name
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   AttributeError: can't delete attribute

Použij property pro validaci vstupu, jako u deskriptoru::

   >>> class Person(object):
   ...     def __init__(self, name, age):
   ...         self.name = name
   ...         self.age = age
   ...     @property
   ...     def age(self):
   ...         return self._age
   ...     @age.setter
   ...     def age(self, value):
   ...         if value < 1:
   ...             raise ValueError("age must be greater than zero")
   ...         self._age = value
   ...     @age.deleter
   ...     def age(self):
   ...         del self._age
   ...
   >>> p = Person("Davie", -1)
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "<stdin>", line 4, in __init__
     File "<stdin>", line 11, in age
   ValueError: age must be greater than zero
   >>> p = Person("Davie", 22)
   >>> del p.age
   >>>

.. note::

   Property dekorátor, ale i staticmethod nebo classmethod dekorátory jsou
   abstrakci nad deskriptory.

.. tip::

   Vytvoř kešovanou verzi property atributu::

      >>> from functools import update_wrapper
      >>> class cached_property(object):
      ...     def __init__(self, func):
      ...         self.func = func
      ...         update_wrapper(self, func)
      ...     def __get__(self, instance, owner):
      ...         if instance is not None:
      ...             value = instance.__dict__[self.func.__name__] = self.func(instance)
      ...             return value
      ...         else:
      ...             return self
      ...
      >>> class Person(object):
      ...     def __init__(self, first_name, last_name):
      ...         self.first_name = first_name
      ...         self.last_name = last_name
      ...     @cached_property
      ...     def full_name(self):
      ...         return f"{self.first_name} {self.last_name}"
      ...
      >>> p = Person("Davie", "Badger")
      >>> p.full_name
      'Davie Badger'
      >>> p.first_name = "Jacob"
      >>> p.full_name
      'Davie Badger'

   Vytvoř kešovanou property s volitelnou možnosti nastavení délky keše
   (defaultně neomezeno) a taktéž její smazaní::

      >>> import time
      >>> from functools import update_wrapper
      >>> class cached_property(object):
      ...     def __init__(self, ttl):
      ...         if callable(ttl):  # ttl is not set
      ...             func = ttl
      ...             ttl = None
      ...         else:
      ...             func = None
      ...         self.ttl = ttl
      ...         self._set_func(func)
      ...     def __call__(self, func):
      ...         self._set_func(func)
      ...         return self
      ...     def __get__(self, instance, owner):
      ...         if instance is None:
      ...             return self
      ...         now = time.time()
      ...         name = self.__name__
      ...         instance_dict = instance.__dict__
      ...         if name in instance_dict:
      ...             value, last_update = instance_dict[name]
      ...             ttl_expired = self.ttl < (now - last_update) if self.ttl is not None else False
      ...             if not ttl_expired:
      ...                 return value
      ...         value = self.func(instance)
      ...         instance_dict[name] = (value, now)
      ...         return value
      ...     def __set__(self, instance, value):
      ...         raise AttributeError(f"can't set {self.__name__}")
      ...     def __delete__(self, instance):
      ...         instance.__dict__.pop(self.__name__, None)
      ...     def _set_func(self, func):
      ...         self.func = func
      ...         if self.func is not None:
      ...             update_wrapper(self, func)
      ...
      >>> class Person(object):
      ...     def __init__(self, first_name, last_name):
      ...         self.first_name = first_name
      ...         self.last_name = last_name
      ...     @cached_property(10)  # seconds
      ...     def full_name(self):
      ...         return f"{self.first_name} {self.last_name}"
      ...
      >>> p = Person("Davie", "Badger")
      >>> p.full_name
      'Davie Badger'
      >>> p.first_name = "Jacob"
      >>> p.full_name
      'Davie Badger'
      >>> time.sleep(10)
      >>> p.full_name
      'Jacob Badger'
      >>> del p.full_name
      >>> p.first_name = "Davie"
      >>> p.full_name
      'Davie Badger'

staticmethod
""""""""""""

Vytvoř statickou metodu, která nepotřebuje pracovat s ``self`` objektem::

   >>> class Dog(object):
   ...     def __init__(name):
   ...         self.name = name
   ...     @staticmethod
   ...     def bark():
   ...         return "Woof! Woof!"
   ...
   >>> dog = Dog("Buddy")
   >>> dog.bark()
   'Woof! Woof!'

.. note::

   Statickou metodu lze volat i bez nutnosti vytvářoní instance třídy::

      >>> class Dog(object):
      ...     @staticmethod
      ...     def bark():
      ...         return "Woof! Woof!"
      ...
      >>> Dog.bark()
      'Woof! Woof!'

classmethod
"""""""""""

Vytvoř metodu, která bude pracovat se třídou, tak jak bylo definována a nikoliv
její instancí::

   >>> class Date(object):
   ...     def __init__(self, day, month, year)
   ...         self.day = day
   ...         self.month = month
   ...         self.year = year
   ...     @classmethod
   ...     def from_string(cls, date)
   ...         day, month, year = map(int, date.split("-"))
   ...         return cls(day, month, year)
   ...
   >>> date = Date.from_string("11-04-1995")
   >>> date.day
   11
   >>> date.month
   4
   >>> date.year
   1995

.. note::

   Pomocí ``cls`` objektu lze přistupovat i k defaultním atributům na třídě::

      >>> class Point(object):
      ...     x = 0
      ...     y = 1
      ...     @classmethod
      ...     def origin_x(cls):
      ...         return cls.x
      ...     @classmethod
      ...     def origin_y(cls):
      ...         return cls.y
      ...
      >>> point = Point()
      >>> point.x = 1
      >>> point.y = 0
      >>> point.x
      1
      >>> point.origin_x()
      0
      >>> point.y
      0
      >>> point.origin_y()
      1

Odbočka k delegaci argumentů
""""""""""""""""""""""""""""

Spusť různé funkce na základě datového typu argumentu::

   >>> from functools import singledispatch
   >>> @singledispatch
   >>> def hello(name):
   ...     pass
   ...
   >>> @hello.register(str)
   ... def hello_str(name):
   ...     return f"Hello {name}"
   ...
   >>> hello(0)
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "/usr/lib/python3.6/functools.py", line 803, in wrapper
       return dispatch(args[0].__class__)(*args, **kw)
     File "<stdin>", line 3, in hello
   ValueError: int is not supported
   >>> hello("Davie")
   'Hello Davie'

.. note::

   Povolené datové typy lze seskupovat do sebe::

      >>> from functools import singledispatch
      >>> @singledispatch
      >>> def hello(name):
      ...     pass
      ...
      >>> @hello.register(list)
      ... @hello.register(tuple)
      ... def hello_container(name):
      ...     conjuction = " and "
      ...     names = " and ".join(name).rstrip(conjuction)
      ...     return f"Hello {names}"
      ...
      >>> hello(["Davie", "Jacob"])
      'Hello Davie and Jacob'

.. tip::

   Pro komplexnější podporu datových typů a jejich definování u vícero
   argumentů najednou lze použít externí knihovnu
   `multipledispatch <https://github.com/mrocklin/multipledispatch>`.

Základní datové typy
====================

Čísla
-----

Vytvoření čísel
^^^^^^^^^^^^^^^

::

   >>> 0
   0
   >>> 1
   1
   >>> -1
   -1
   >>> 0.0
   0.0
   >>> 1.1
   1.1
   >>> -1.1
   -1.1
   >>> int(1.1)
   1
   >>> float(-1)
   -1.0
   >>> x = 1
   >>> -x
   -1
   >>> -(-x)
   1

.. tip::

   Od Pythonu 3.6 lze použít podtržítko pro přehlednější oddělování tísíců
   u velkých čísel::

      >>> 1_000_000 == 1000000
      True
      >>> 1_000_000
      1000000
      >>> 1_0_0
      100

Operace s čísly
^^^^^^^^^^^^^^^

::

   >>> 1 + 1
   2
   >>> 1 - 1.0
   0.0
   >>> 1 * 1
   1
   >>> 1 / 3
   0.3333333333333333
   >>> 1 // 3
   0
   >>> 1 % 3
   1
   >>> 2 ** 2
   4
   >>> 4 * 0.5
   2.0
   >>> abs(-1)
   1
   >>> divmod(2, 2)
   (1, 0)
   >>> round(1.45, 1)  # Correct is 1.5
   1.4

.. note::

   Další operace lze provádět pomocí ``math`` knihovny.

.. tip::

   Pro lepší a přesnější výsledky operací s desetinnými čísly lze použít
   ``decimal`` knihovnu.

Řetězce
-------

Vytvoření řetězců
^^^^^^^^^^^^^^^^^

::

   >>> ''
   ''
   >>> ""
   ''
   >>> 'text'
   'text'
   >>> "text"
   'text'
   >>> name = "Davie"
   >>> 'Name: {}'.format(name)
   'Name: Davie'
   >>> f"Name: {name}"
   'Name: Davie'
   >>> str(1)
   '1'

.. note::

   Ještě existuje zastaralý způsob formátování pomocí ``%``, kterými by však
   měl být nahrazen novějšimi variantami::

      >>> "Name: %s" % "Davie"
      'Name: Davie'

.. tip::

   Další způsoby `formátování řetězců`_.

Operace s řetězcemi
^^^^^^^^^^^^^^^^^^^

::

   >>> name = "Davie"
   >>> name + " " + "Badger"
   'Davie Badger'
   >>> "Davie" " " "Badger"
   'Davie Badger'
   >>> name * 3
   'DavieDavieDavie'
   >>> 3 * name
   'DavieDavieDavie'
   >>> "D" in name
   True
   >>> "D" not in name
   False
   >>> name[0]
   'D'
   >>> name[0:3]
   'Dav'
   >>> name[0:5:2]
   'Dve'
   >>> len(name)
   5
   >>> max(name)
   'v'
   >>> min(name)
   'D'

Metody řetězců
^^^^^^^^^^^^^^

* ``.capitalize()``

  * vrať řetězec, kde první znak je velkým písmem::

       >>> "davie badger".capitalize()
       'Davie badger'

* ``.center(width, fillchar=" ")``

  * vrať řetězec, který bude vycentrovaný na střed podle velikost ``width`` a
    zbylé okraje vyplněné znakem ``fillchar``::

       >>> "Davie".center(i3)
       '    Davie    '

* ``.count(sub, start=0, end=-1)``

  * vrať počet výskytů ``sub`` v daném řetězci::

       >>> "Davie".count("D")
       1

* ``.endswith(suffix, start=-1, end=0)``

  * vrať ``True``, pokud řetězec končí od konce ``start`` na daný ``suffix``
    nebo alespoň jeden z prefixů::

       >>> name = "Davie"
       >>> name.endswith("e")
       True
       >>> name.endswith("E")
       False
       >>> name.endswith(("a", "e", "i", "o", "u"))
       True
       >>> name.endswith(("a", "e", "i", "o", "u"))
       True

* ``.find(sub, start=0, end=-1)``

  * vrať index prvního výskytu ``sub`` v řetězcí, jinak ``-1``, pokud ``sub``
    neexistuje v řetězci::

       >>> name = "Davie"
       >>> name.find("e")
       4
       >>> name.find("E")
       -1

* ``.format(*args, **kwargs)``

  * vrať naformátovaný řetězec::

       >>> "Davie {}".format("Badger")
       'Davie Badger'
       >>> "{} {1}".format("Davie", "Badger")
       'Davie Badger'
       >>> "{first_name} {last_name}".format(first_name="Davie", last_name="Badger")
       'Davie Badger'

* ``.index(sub, start=0, end=-1)``

  * vrať index prvního výskytu ``sub`` v řetězci, jinak vyvolej
    ``ValueError``::

       >>> name = "Davie"
       >>> name.index("D")
       0
       >>> name.index("d")
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       ValueError: substring not found

* ``.isalnum()``

  * vrať ``True``, pokud se v řetězci nacházejí písmena a čísla::

       >>> "Davie".isalnum()
       True
       >>> "Davie123".isalnum()
       True
       >>> "Davie 123".isalnum()
       False

* ``.isalpha()``

  * vrať ``True``, pokud jsou v řetězci jenom písmena::

       >>> "Davie".isalpha()
       True
       >>> "Davie Badger".isalpha()
       False

* ``.islower()``

  * vrať ``True``, pokud jsou všechna písmena v řetězci malými písmeny::

       >>> name = "Davie"
       >>> name.islower()
       False
       >>> name.lower().islower()
       True

* ``.isnumeric()``

  * vrať ``True``, pokud jsou v řetězci jenom čísla::

       >>> "123".isnumeric()
       True
       >>> "123 456".isnumeric()
       False

* ``.istitle()``

  * vrať ``True``, pokud jsou první písmeno v řetězci je velkým písmem::

       >>> name = "Davie"
       >>> name.istitle()
       True
       >>> name.lower().istitle()
       False

* ``.isupper()``

  * vrať ``True``, pokud jsou všechna písmena v řetězci velkými písmeny::

       >>> name = "Davie"
       >>> name.isupper()
       False
       >>> name.upper().isupper()
       True

* ``.join(iterable)``

  * vrať řetězec, kde jsou řetězcové položky z ``iterable`` zřetězeny podle
    daného oddělovače::

       >>> iterable = ["Davie", "Badger"]
       >>> "".join(iterable)
       'DavieBadger'
       >>> " ".join(iterable)
       'Davie Badger'
       >>> "\n".join(iterable)
       'Davie\nBadger'

* ``.ljust(width, fillchar=" ")``

  * vrať řetězec, který bude zarovnaný vlevo podle velikost ``width`` a zbylé
    znaky budou vyplněné znakem ``fillchar``::

       >>> "Davie".ljust(i3)
       'Davie        '

* ``.lower()``

  * vrať řetězec, kde veškeré písmena jsou malými písmeny::

       >>> "Davie".lower()
       'davie'

* ``.lstrip(chars=" ")``

  * vrať řetězec, kde jsou z levé strany odstraněné znaky ``chars``::

       >>> "   Davie".lstrip()
       'Davie'
       >>> "Davie".lstrip("Da")
       'vie'

* ``.replace(old, new, count=-1)``

  * vrat řetězec, kde znak(y) ``old`` budou nahrazeny znak(y) ``new`` podle
    výskytu ``count``, defaultně všechny::

       >>> "Davie".replace("v", "D")
       'DaDie'

* ``.rjust(width, fillchar=" ")``

  * vrať řetězec, který bude zarovnaný pravo podle velikost ``width`` a zbylé
    znaky budou vyplněné znakem ``fillchar``::

       >>> "Davie".rjust(i3)
       '        Davie'

* ``.rstrip(chars=" ")``

  * vrať řetězec, kde jsou z pravé strany odstraněné znaky ``chars``::

       >>> "Davie   ".rstrip()
       'Davie'
       >>> "Davie".rstrip("vie")
       'Da'

* ``.split(sep=None, maxsplit=-1)``

  * vrať seznam, ve kterém jsou položky z řetězce rozdělené podle ``sep`` v
    množství ``maxsplit``, defaultně neomezeno::

       >>> name = "Davie Badger"
       >>> name.split()
       ['Davie', 'Badger']
       >>> name.split(" ")
       ['Davie', 'Badger']

* ``.splitlines()``

  * vrať seznam, ve kterém jsou položky rozsekané z řetězce podle oddělovačů
    řádků::

       >>> text = "Hello World,\n\nmy name is Davie\n"
       >>> text.splitlines()
       ['Hello World,', '', 'my name is Davie']
       >>> text.split("\n")
       ['Hello World,', '', 'my name is Davie', '']

* ``.startswith(prefix, start=0, end=-1)``

  * vrať ``True``, pokud řetězec začíná od začátku ``start`` na daný ``prefix``
    nebo alespoň jeden z prefixů::

       >>> name = "Davie"
       >>> name.startswith("d")
       False
       >>> name.startswith("D")
       True
       >>> name.startswith(("a", "b", "c", "d"))
       False
       >>> name.startswith(("A", "B", "C", "D"))
       True

* ``.strip(chars=" ")``

  * vrať řetězec, kde jsou z obou stran řetězce odstraněné znaky ``chars``::

       >>> "  Davie   ".strip()
       'Davie'
       >>> "Davie".strip("De")
       'avi'

* ``.swapcase()``

  * vrať řetězec, kde jsou prohozené velikosti písmen::

       >>> "Davie".swapcase()
       'dAVIE'

* ``.title()``

  * vrať řetězec, kde každé počáteční písmo slova velkým písmenem::

       >>> "davie badger".title()
       'Davie Badger'

* ``.upper()``

  * vrať řetězec, kde veškerá písmena jsou velkými písmeny::

       >>> "Davie".upper()
       'DAVIE'

Seznamy
-------

Vytvoření seznamu
^^^^^^^^^^^^^^^^^

::

   >>> []
   >>> [1, 2, 3]
   >>> list("abc")
   ['a', 'b', 'c']

.. note::

   Seznamy jsou měnitelné::

      >>> x = [1, 2, 3]
      >>> y = x
      >>> y.append(4)
      >>> y
      [1, 2, 3, 4]
      >>> x
      [1, 2, 3, 4]

.. tip::

   Vytvoř seznam pomocí jednořádkového cyklu a případně podmínky::

      >>> [number for number in range(3)]
      [0, 1, 2]
      >>> [number + 1 for number in range(3)]
      [1, 2, 3]
      >>> [number for number in range(11) if number % 2 == 0]
      [0, 2, 4, 6, 8, 10]
      >>> [True if number % 2 == 0 else False for number in range(11)]
      [True, False, True, False, True, False, True, False, True, False, True]

Operace se seznamy
^^^^^^^^^^^^^^^^^^

::

   >>> numbers = [1, 2, 3]
   >>> numbers + [4, 5, 6]
   [1, 2, 3, 4, 5, 6]
   >>> numbers * 2
   [1, 2, 3, 1, 2, 3]
   >>> 1 in numbers
   True
   >>> 0 not in numbers
   True
   >>> numbers[0]
   1
   >>> numbers[0] = 0
   >>> numbers
   [0, 2, 3]
   >>> numbers[:] = [1, 2, 3]
   >>> numbers
   [1, 2, 3]
   >>> len(numbers)
   3
   >>> min(numbers)
   1
   >>> max(numbers)
   3
   >>> del numbers[2]
   >>> numbers
   [1, 2]

.. note::

   K vnořeným seznamům lze taktéž přístupovat pomocí indexů::

      >>> nested_numbers = [[1, 2, 3], [4, 5, 6]]
      >>> nested_numbers[0]
      [1, 2, 3]
      >>> nested_numbers[1][0]
      4

Metody seznamů
^^^^^^^^^^^^^^

* ``.append(item)``

  * přidej položku ``item`` na konec seznamu::

       >>> x = [1, 2, 3]
       >>> x.append(4)
       >>> x
       [1, 2, 3, 4]

* ``.clear()``

  * vyprázdní seznam::

       >>> x = [1, 2, 3]
       >>> x.clear()
       >>> x
       []

* ``.count(item)``

  * vrať počet výskytů položky ``item`` v seznamu::

       >>> x = [1, 2, 3]
       >>> x.count(1)
       1

* ``.copy()``

  * vrať nový seznam, kde jsou zkopírované prvky z předchozího seznamu::

       >>> x = [1, 2, 3]
       >>> y = x.copy()
       >>> y.append(4)
       >>> y
       [1, 2, 3, 4]
       >>> x
       [1, 2, 3]

* ``.extend(sequence)``

  * rozšíř seznam o další položky z ``sequence``::

       >>> x = [1, 2, 3]
       >>> x.extend("abc")
       >>> x
       [1, 2, 3, 'a', 'b', 'c']

* ``.index(item, start=0, end=-1)``

  * vrať pořadí položky ``item`` v seznamu, pokud položka existuje, jinak
    vyvolej ``ValueError``::

       >>> x = [1, 2, 3]
       >>> x.index(3)
       2
       >>> x.index(4)
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       ValueError: 4 is not in list

* ``.insert(index, item)``

  * vlož do seznamu na místě ``index`` položku ``item``::

       >>> x = []
       >>> x.insert(0, 1)
       >>> x
       [1]
       >>> x.insert(100, 2)
       [1, 2]
       >>> x.insert(-100, 0)
       [0, 1, 2]

* ``.pop(index=-1)``

  * odstraň se seznamu položku na místě ``index``, pokud index existuje,
    jinak vyvolej ``IndexError``::

       >>> x = [1, 2, 3]
       >>> x.pop()
       3
       >>> x.pop(1)
       2
       >>> x
       [1]
       >>> x.pop(0)
       1
       >>> x
       []
       >>> x.pop()
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       IndexError: pop from empty list

* ``.remove(item)``

  * odstraň položku ``item`` ze seznamu, pokud existuje, jinak vyvolej
    ``ValueError``::

       >>> x = [1, 2, 3]
       >>> x.remove(3)
       >>> x
       [1, 2]
       >>> x.remove(3)
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       ValueError: list.remove(x): x not in list

* ``.reverse()``

  * obrať pořadí položek v seznamu::

       >>> x = [1, 2, 3]
       >>> x.reverse()
       >>> x
       [3, 2, 1]

* ``.sort(key=None, reverse=None)``

  * seřaď položky v seznamu s / bez klíče ``key``::

       >>> x = [3, 2, 1]
       >>> x.sort()
       >>> x
       [1, 2, 3]
       >>> y = [{"name": "Davie", "age": 22}, {"name": "Jacob", "age": 17}]
       >>> y.sort(key=lambda person: person["age"])
       >>> y
       [{'name': 'Jacob', 'age': 17}, {'name': 'Davie', 'age': 22}]

.. tip::

   Pokud seznam tvoří seřazené položky, tak lze pomocí funkce ``insort`` z
   knihovny ``bisect`` vložit další položku tak, aby seznam byl stále seřazený
   bez nutnosti volat seřazovací funkci::

      >>> from bisect import insort
      >>> x = list(range(10))
      >>> insort(x, -1)
      >>> x
      [-1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
      >>> insort(x, 10)
      >>> x
      [-1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
      >>> y = ["a", "b", "c"]
      >>> insort(y, "d")
      >>> y
      ['a', 'b', 'c', 'd']

   Na jaké misto bude položka vložena lze zjístit pomocí funkce ``bisect``::

      >>> from bisect import bisect
      >>> x = list(range(10))
      >>> bisect(x, -1)
      0
      >>> x.insert(0, -1)
      >>> x
      [-1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
      >>> bisect(x, -1)
      1

   Pokud se už položka nachází v seznamu, tak ``bisect`` defaultně vrací index
   následující za existující položkou. Stejný principem se chová i funkce
   ``insort``, není-li použit opačný algoritmus::

      >>> from bisect import bisect, bisect_left, insort, insort_left
      >>> x = list(range(10))
      >>> bisect(x, 0)
      1
      >>> bisect_left(x, 0)
      0
      >>> insort(x, 0)
      >>> x
      [0, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
      >>> insort_left(x, 0)
      [0, 0, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

N-tice
------

Vytvoření n-tic
^^^^^^^^^^^^^^^

::

   >>> ()
   >>> (1,)
   >>> (1, 2, 3)
   >>> tuple(range(3))
   (0, 1, 2)

.. note::

   Jednořádkový cyklus nevytvoří n-tici, ale jednorázový generátor pro
   iteraci::

      >>> generator = (number for number in range(3))
      >>> generator
      <generator object <genexpr> at 0x7f7256fee1a8>
      >>> list(generator)
      [0, 1, 2]
      >>> list(generator)
      []

.. tip::

   N-tice a další sekvence lze rozbalit do proměnných::

      >>> x, y, z = (1, 2, 3)
      >>> x
      1
      >>> y
      2
      >>> z
      3
      >>> first, *_, last = range(11)
      >>> first
      0
      >>> _
      [1, 2, 3, 4, 5, 6, 7, 8, 9]
      >>> last
      10

   Rozbalit lze i z vnořených sekvencí pomocí n-tic::

      >>> x, (y, z) = [1, [2, 3]]
      >>> print(x, y, z)
      1 2 3
      >>> x, (y, (z,)) = [1, [2, [3]]]
      >>> print(x, y, z)
      1 2 3

Operace s n-ticemi
^^^^^^^^^^^^^^^^^^

::

   >>> numbers = (1, 2, 3)
   >>> numbers + (4, 5, 6)
   (1, 2, 3, 4, 5, 6)
   >>> numbers * 2
   (1, 2, 3, 1, 2, 3)
   >>> 1 in numbers
   True
   >>> 0 not in numbers
   True
   >>> numbers[0]
   1
   >>> len(numbers)
   3
   >>> min(numbers)
   1
   >>> max(numbers)
   3

.. note::

   Operace pro modifikaci položky budou vždy končit typovým errorem, neboť
   n-tice je neměnitelný seznam::

      >>> numbers = (1, 2, 3)
      >>> numbers[0] = 0
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      TypeError: 'tuple' object does not support item assignment
      >>> del numbers[0]
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      TypeError: 'tuple' object doesn't support item deletion

Metody n-tic
^^^^^^^^^^^^

* ``.count(item)``

  * vrať počet výskytů položky ``item`` v n-tici::

       >>> x = (1, 2, 3)
       >>> x.count(1)
       1

* ``.index(item, start=0, end=-1)``

  * vrať pořadí položky ``item`` v seznamu, pokud položka existuje, jinak
    vyvolej ``ValueError``::

       >>> x = [1, 2, 3]
       >>> x.index(3)
       2
       >>> x.index(4)
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       ValueError: tuple.index(x): x not in tuple

Množiny
-------

Vytvoření množin
^^^^^^^^^^^^^^^^

::

   >>> set()
   set()
   >>> frozenset()
   frozenset()
   >>> {1, 2, 3}
   {1, 2, 3}
   >>> frozenset({1, 2, 3})
   frozenset({1, 2, 3})
   >>> set([1, 1, 1])
   {1}
   >>> {number for number in range(11) if number % 2 == 0}
   {0, 2, 4, 6, 8, 10}

.. note::

   Obyčejné množiny jsou měnitelné::

      >>> x = {1, 2, 3}
      >>> y = x
      >>> y.add(4)
      >>> y
      {1, 2, 3, 4}
      >>> x
      {1, 2, 3, 4}
      >>> z = frozenset(x)
      >>> z.add(5)
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      AttributeError: 'frozenset' object has no attribute 'add'

Operace s množinami
^^^^^^^^^^^^^^^^^^^

::

   >>> x = {1, 2, 3}
   >>> len(x)
   3
   >>> 1 in x
   True
   >>> 4 not in x
   >>> y = {2, 3, 4}
   >>> x | y
   {1, 2, 3, 4}
   >>> x & y
   {2, 3}
   >>> x - y
   {1}
   >>> y - x
   {4}
   >>> x ^ y
   {1, 4}
   >>> {1} <= x
   True
   >>> x >= {1}
   True

.. note::

   Při použití metod namísto operátorů pro množinové operace nemusí být nutně
   na druhé straně množina, neboť dojde k automatické konverzi::

      >>> {1} | {2}
      {1, 2}
      >>> {1} | "a"
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      TypeError: unsupported operand type(s) for |: 'set' and 'str'
      >>> {1}.union("abc")
      {1, 'c', 'b', 'a'}

Metody množin
^^^^^^^^^^^^^

* ``.add(elem)`` (set)

  * přidej ``elem`` do množiny::

       >>> x = {1, 2, 3}
       >>> x.add(4)
       >>> x
       {1, 2, 3, 4}

* ``.clear()`` (set)

  * vyprázdní množinu::

       >>> x = {1, 2, 3}
       >>> x.clear()
       >>> x
       set()

* ``.copy()`` (set, frozenset)

  * vrať novou množinu, kde jsou zkopírované prvky z předchozí množiny::

       >>> x = {1, 2, 3}
       >>> y = y.copy()
       >>> y.add(4)
       >>> y
       {1, 2, 3, 4}
       >>> x
       {1, 2, 3}

* ``.difference(*iterables)`` (set, frozenset)

  * vrať množinu po rozdílu mezi množinou a ``iterables``::

       >>> x = {1, 2, 3}
       >>> x.difference({2, 3, 4})
       {1}
       >>> x.difference({2, 3, 4}, "1", [1])
       set()

* ``.difference_update(*iterables)`` (set)

  * ponechej v množině jen prvky po rozdílu množiny a ``iterables``::

       >>> x = {1, 2, 3}
       >>> x.difference_update({2, 3, 4})
       >>> x
       {1}
       >>> y = {1, 2, 3}
       >>> y -= {2, 3, 4}
       >>> y
       {1}

* ``.discard(elem)`` (set)

  * odstraň ``elem`` z množiny, pokud ``elem`` existuje v množině::

       >>> x = {1, 2, 3}
       >>> x.discard(3)
       >>> x
       {1, 2}
       >>> x.discard(3)
       >>> x
       {1, 2}

* ``.intersection(*iterables)`` (set, frozenset)

  * vrať množinu po průniku množiny a ``iterables``::

       >>> x = {1, 2, 3}
       >>> x.intersection({2})
       {2}
       >>> x.intersection({2}, "1", [4])
       set()

* ``.intersection_update(*iterables)`` (set)

  * ponechej v množině jen prvky po průniku množiny a ``iterables``::

       >>> x = {1, 2, 3}
       >>> x.intersection_update({2})
       >>> x
       {2}
       >>> y = {1, 2, 3}
       >>> y &= {2}
       {2}

* ``.isdisjoint(iterable)`` (set, frozenset)

  * vrať ``True``, pokud množiny nemají žádný společný prvek::

       >>> x = {1, 2, 3}
       >>> x.disjoint({4})
       True
       >>> x.disjoint("abc")
       True

* ``.issubset(iterable)`` (set, frozenset)

  * vrať ``True``, pokud množina je podmnožinou ``iterable``::

       >>> x = {1, 2, 3}
       >>> x.issubset({1, 2, 3})
       True
       >>> x.issubset([1, 2, 3])
       True

* ``.issuperset(iterable)`` (set, frozenset)

  * vrať ``True``, pokud množina je nadmnožinou ``iterable``::

       >>> x = {1, 2, 3}
       >>> x.issuperset({1})
       True
       >>> x.issuperset((1,))
       True

* ``.pop()`` (set)

  * vrať odstraněný počáteční prvek z množiny::

       >>> x = {1, 2, 3}
       >>> y = x.pop()
       >>> y
       1
       >>> x
       {2, 3}

* ``.remove(elem)`` (set)

  * odstraň ``elem`` z množiny, avšak pokud ``elem`` neexistuje v množině,
    vyvolej ``KeyError``::

       >>> x = {1, 2, 3}
       >>> x.remove(3)
       >>> x
       {1, 2}
       >>> x.remove(3)
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       KeyError: 3

* ``.symmetric_difference(iterable)`` (set, frozenset)

  * vrať množinu po doplňku množiny a ``iterable``::

       >>> x = {1, 2, 3}
       >>> y = {2, 3, 4}
       >>> x.symmetric_difference(y)
       {1, 4}

* ``.symmetric_difference_update(other)`` (set)

  * ponechej v množine jen prvky po doplňku množiny a ``other``::

       >>> x = {1, 2, 3}
       >>> x.symmetric_difference({2, 3, 4})
       >>> x
       {1, 4}
       >>> y = {1, 2, 3}
       >>> y ^= {2, 3, 4}
       {1, 4}

* ``.union(*iterables)`` (set, frozenset)

  * vrať množinu po sjednocení množiny a ``iterables``::

       >>> x = {1, 2, 3}
       >>> x.union({4})
       {1, 2, 3, 4}
       >>> x.union({4}, "5", [6])
       {1, 2, 3, 4, 6, '5'}

* ``.update(*iterables)`` (set)

  * přidej do množiny další položky z ``iterables``::

       >>> x = set()
       >>> x.update({1}, [2], (3,))
       >>> x
       {1, 2, 3}
       >>> y = set()
       >>> y |= {1, 2, 3}
       >>> y
       {1, 2, 3}

Slovníky
--------

Vytvoření slovníku
^^^^^^^^^^^^^^^^^^

::

   >>> {}
   >>> {"one": 1, "two": 2, "three": 3}
   {'one': 1, 'two': 2, 'three': 3}
   >>> dict(one=1, two=2, three=3)
   {'one': 1, 'two': 2, 'three': 3}
   >>> dict([("one", 1), ("two", 2), ("three", 3)])
   {'one': 1, 'two': 2, 'three': 3}
   >>> x = {"one": 1, "two": 2, "three": 3}
   >>> y = {value: key for key, value in x.items()}
   >>> x
   {'one': 1, 'two': 2, 'three': 3}
   >>> y
   {1: 'one', 2: 'two', 3: 'three'}

.. note::

   Slovníky jsou měnitelné::

      >>> x = {"a": 1, "b": 2, "c": 3}
      >>> y = x
      >>> y.popitem()
      ('c', 3)
      >>> y
      {'a': 1, 'b': 2}
      >>> x
      {'a': 1, 'b': 2}

.. tip::

   U rozsáhlejších slovníku nebo i jiných kolekcí lze použít vylepšený
   ``print`` pro strukturovanější výpis hodnot::

      >>> people = [{"name": "Davie", "gender": "M", "age": 22}, {"name": "Jacob", "gender": "M", "age": 17}]
      >>> print(people)
      [{'name': 'Davie', 'gender': 'M', 'age': 22}, {'name': 'Jacob', 'gender': 'M', 'age': 17}]
      >>> import pprint
      >>> pprint.pprint(people)
      [{'age': 22, 'gender': 'M', 'name': 'Davie'},
       {'age': 17, 'gender': 'M', 'name': 'Jacob'}]

Operace se slovníky
^^^^^^^^^^^^^^^^^^^

::

   >>> person = {"name": "Davie Badger", "age": 22}
   >>> len(person)
   2
   >>> person["name"]
   'Davie Badger'
   >>> person["gender"] = "male"
   >>> person
   {'name': 'Davie Badger', 'age': 22, 'gender': 'male'}
   >>> del person["gender"]
   >>> del person["gender"]
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   KeyError: 'gender'
   >>> "name" in person
   True
   >>> "gender" not in person
   True

.. note::

   Od verze Pythonu 3.6 jsou klíče ve slovníku seřazeny podle jejich vzniku a
   případně další aktualizaci slovníku.

.. tip::

   Sloučení dvou slovníků do jednoho nového slovníku::

      >>> x = {"one": 1, "two": 2}
      >>> y = {"three": 3}
      >>> z = {**x, **e}
      >>> z
      {'one': 1, 'two': 2, 'three': 3}

Metody slovníků
^^^^^^^^^^^^^^^

* ``.clear()``

  * odstraň všechny klíče s hodnotami ze slovníku::

       >>> x = {"age": 22}
       >>> x.clear()
       >>> x
       {}

* ``.copy()``

  * vrať nový slovník, kde jsou zkopírované klíče a hodnoty z předchozího
    slovníku::

       >>> x = {"age": 22}
       >>> y = y.copy()
       >>> y.pop("age")
       22
       >>> y
       {}
       >>> x
       {'age': 22}

* ``.fromkeys(sequence, default=None)``

  * vytvoř slovník z položek ``sequence`` a defaultní hodnotou ``default``::

       >>> x = ["a", "b", "c"]
       >>> dict.fromkeys(x)
       {'a': None, 'b': None, 'c': None}
       >>> dict.fromkeys(x, 0)
       {'a': 0, 'b': 0, 'c': 0}
       >>> y = dict.fromkeys(x, [])
       >>> y["a"].append(0)
       >>> y
       {'a': [0], 'b': [0], 'c': [0]}
       >>> y = {item: [] for item in x}
       >>> y["a"].append(0)
       >>> y
       {'a': [0], 'b': [], 'c': []}

* ``.get(key, default=None)``

  * vrať hodnotu pro klíč ``key``, pokud existuje, jinak ``default`` hodnotu::

       >>> x = {"age": 22}
       >>> x.get("age")
       22
       >>> x.get("age", 23)
       22
       >>> x.get("gender", "male")
       'male'

* ``.items()``

  * vrať ``dict_items`` objekt, ve kterém jsou n-tice s klíčem a hodnotou::

       >>> x = {"age": 22}
       >>> y = x.items()
       >>> y
       dict_items([('age', 22)])
       >>> ('age', 22) in y
       True
       >>> list(y)
       [('age', 22)]
       >>> for key, value in x.items():
       ...     print(f"Key: {key}, Value: {value}")
       ...
       Key: age, Value: 22
       >>> key, value = next(iter(x.items()))
       >>> key
       'age'
       >>> value
       22

* ``.keys()``

  * vrať ``dict_keys`` objekt, ve kterém je seznam klíčů ze slovníku::

       >>> x = {"age": 22}
       >>> y = x.keys()
       >>> y
       dict_keys(['age'])
       >>> list(y)
       ['age']

* ``.pop(key, default=None)``

  * vrať hodnotu pro odstraněný klíč ``key``, pokud existoval ve slovníku,
    jinak vyvolej ``KeyError``, pokud neni uvedena hodnota ``default``, když
    klíč neexistuje::

       >>> x = {"age": 22}
       >>> x.pop("age")
       22
       >>> x
       {}
       >>> x.pop("age")
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       KeyError: 'age'
       >>> x.pop("age", None)
       >>> x.pop("age", 0)
       0

* ``.popitem()``

  * odstraň ze slovníku poslední položku, dokud slovník není prázdny,
    jinak vyvolej ``KeyError``::

       >>> x = {"age": 22}
       >>> x.popitem()
       ('age', 22)
       >>> x
       {}
       >>> x.popitem()
       Traceback (most recent call last):
         File "<stdin>", line 1, in <module>
       KeyError: 'popitem(): dictionary is empty'

* ``.setdefault(key, default=None)``

  * vrať hodnotu pro klíč ``key``, pokud existuje, jinak jej vytvoř spolu s
    hodnotou ``default``::

       >>> x = {"age": 22}
       >>> x.setdefault("age")
       22
       >>> x.setdefault("gender", "male")
       >>> x
       {'age': 22, 'gender': 'male'}

* ``.update(other)``

  * aktualizuj slovník podle klíčů a hodnot v ``other``::

       >>> x = {"age": 22}
       >>> x.update(age=23)
       >>> x
       {'age': 23}
       >>> x.update({"age": 22})
       >>> x
       {'age': 22}
       >>> x.update(zip(["age"], [23]))
       >>> x
       {'age': 23}
       >>> x.update(gender="male")
       >>> x
       {'age': 23, gender: "male"}

* ``.values()``

  * vrať ``dict_values`` objekt, ve kterém jsou vytaženy všechny hodnoty
    ze slovníku::

       >>> x = {"age": 22}
       >>> y = x.values()
       >>> y
       dict_values([22])
       >>> 22 in y
       True
       >>> list(y)
       [22]

.. note::

   Objekty ``dict_...`` jsou taktéž měnitelné::

      >>> x = {"age": 22}
      >>> y = x.values()
      >>> x.update(age=23)
      >>> x
      {'age': 23}
      >>> y
      dict_values([23])

Pokročilé datové typy
=====================

Modifikované seznamy
--------------------

deque
^^^^^

Vytvoř speciální seznam, do kterého lze přidávat nebo mazat položky z obou
stran::

   >>> from collections import deque
   >>> d = deque()
   >>> d
   deque([])
   >>> d.append(0)
   >>> d
   deque([0])
   >>> d.append(1)
   >>> d.appendleft(-1)
   >>> d
   deque([-1, 0, 1])
   >>> d.extend("cba")
   >>> d.extendleft("abc")
   >>> d
   deque(['c', 'b', 'a', -1, 0, 1, 'c', 'b', 'a'])
   >>> d.pop()
   'a'
   >>> d.popleft()
   'c'
   >>> d
   deque(['b', 'a', -1, 0, 1, 'c', 'b'])

.. note::

   Pomocí metody ``rotate`` lze přesouvat položky na krajích na opačnou
   stranu::

      >>> from collections import deque
      >>> d = deque(range(10))
      >>> d
      deque([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
      >>> d.rotate()  # last to first
      >>> d
      deque([9, 0, 1, 2, 3, 4, 5, 6, 7, 8])
      >>> d.rotate(1)  # last to first
      >>> d
      deque([8, 9, 0, 1, 2, 3, 4, 5, 6, 7])
      >>> d.rotate(-1)  # first to last
      >>> d
      deque([9, 0, 1, 2, 3, 4, 5, 6, 7, 8])
      >>> d.rotate(-2)  # first two to last
      deque([1, 2, 3, 4, 5, 6, 7, 8, 9, 0])

.. tip::

   Nastav fixní velikost ``deque``::

      >>> from collections import deque
      >>> d = deque(range(3), maxlen=3)
      >>> d
      deque([0, 1, 2], maxlen=3)
      >>> d.append(3)
      >>> d
      deque([1, 2, 3], maxlen=3)
      >>> d.appendleft(0)
      >>> d
      deque([0, 1, 2], maxlen=3)
      >>> d.pop()
      2
      >>> d
      deque([0, 1], maxlen=3)
      >>> d.appendleft(-1)
      >>> d
      deque([-1, 0, 1], maxlen=3)
      >>> d.insert(0, 0)
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      IndexError: deque already at its maximum size

Modifikované n-tice
-------------------

namedtuple
^^^^^^^^^^

Vytvoř speciální n-tici, kde k položkám n-tice lze přistupovat jako k
atributům::

   >>> from collections import namedtuple
   >>> point = (0, 1)
   >>> point.x
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   AttributeError: 'tuple' object has no attribute 'x'
   >>> Point = namedtuple("Point", ["x", "y"])
   >>> point = Point(0, 1)
   >>> point.x
   0
   >>> point.y
   1
   >>> point[0]
   0
   >>> point[1]
   1
   >>> point[2]
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   IndexError: tuple index out of range
   >>> x, y = point
   >>> x
   0
   >>> y
   1
   >>> point
   Point(x=0, y=1)
   >>> point["x"]
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: tuple indices must be integers or slices, not str
   >>> point._fields
   ('x', 'y')

Vytvoř ``namedtuple`` včetně dědičnosti::

   >>> from collections import namedtuple
   >>> Point2D = namedtuple("Point2D", ["x", "y"])
   >>> Point3D = namedtuple("Point3D", Point2D._fields + ("z",))
   >>> point = Point3D(0, 1, 2)
   >>> point
   Point3D(x=0, y=1, z=2)

.. note::

   Názvy atributů lze zadat i pomocí řetězce, kde oddělovačem je mezera nebo
   čárka::

      >>> from collections import namedtuple
      >>> Point = namedtuple("Point", "x y")
      >>> Point(0, y=1)._asdict()
      OrderedDict([('x', 0), ('y', 1)])
      >>> Point = namedtuple("Point", "x, y")
      >>> Point(x=0, y=1)._asdict()
      OrderedDict([('x', 0), ('y', 1)])

.. tip::

   Vytvoř vlastní neměnitelný objekt z ``namedtuple``::

      >>> from collections import namedtuple
      >>> class Point(namedtuple("Point", ["x", "y"])):
      ...     __slots__ = ()
      ...     @property
      ...     def distance_from_zero(self):
      ...         return (self.x ** 2 + self.y ** 2) ** 0.5
      ...     def __str__(self):
      ...         return f"Point: x={self.x}, y={self.y}, distance_from_zero={self.distance_from_zero}"
      ...
      >>> point = Point(0, 1)
      >>> point
      Point(x=0, y=1)
      >>> print(point)
      Point: x=0, y=1, distance_from_zero=1.0
      >>> point.x
      0
      >>> point[0]
      0
      >>> point.y
      1
      >>> point[1]
      1
      >>> point.distance_from_zero
      1.0
      >>> point.x = 1
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      AttributeError: can't set attribute
      >>> del point.x
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      AttributeError: can't delete attribute

Modifikované slovníky
---------------------

ChainMap
^^^^^^^^

Spoj několik slovníků do jednoho jednoho velkého::

   >>> from collections import ChainMap
   >>> default = {"user": "admin", "password": "admin", "host": "localhost", "port": 12345}
   >>> real = {"user": "davie", "password": "password"}
   >>> config = ChainMap(real, default)
   >>> config["user"]
   'davie'
   >>> config["password"]
   'password'
   >>> config["host"]
   'localhost'
   >>> config["port"]
   12345
   >>> config
   ChainMap({'user': 'davie', 'password': 'password'}, {'user': 'admin', 'password': 'admin', 'host': 'localhost', 'port': 12345})
   >>> config
   ChainMap({'user': 'davie', 'password': 'password', 'ssl': True}, {'user': 'admin', 'password': 'admin', 'host': 'localhost', 'port': 12345})
   >>> del config["user"]
   >>> config["user"]
   'admin'
   >>> del config["host"]
   Traceback (most recent call last):
     File "/usr/lib/python3.6/collections/__init__.py", line 934, in __delitem__
       del self.maps[0][key]
   KeyError: 'host'

   During handling of the above exception, another exception occurred:

   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "/usr/lib/python3.6/collections/__init__.py", line 936, in __delitem__
       raise KeyError('Key not found in the first mapping: {!r}'.format(key))
   KeyError: "Key not found in the first mapping: 'host'"
   >>> config.parents
   ChainMap({'user': 'admin', 'password': 'admin', 'host': 'localhost', 'port': 12345})
   >>> config.maps
   [{'user': 'davie', 'password': 'password'}, {'user': 'admin', 'password': 'admin', 'host': 'localhost', 'port': 12345}]
   >>> dict(config)
   {'port': 12345, 'host': 'localhost', 'password': 'password', 'user': 'davie'}

.. note::

   Pokud se ve slovnících v ``ChainMap`` nachází duplicitní klíče, tak hodnota
   těchto duplicitních klíčů výchází z prvního slovníku nalevo, ve kterém se
   klíč nachází.

   Je-li třeba na první místo přesunout jiný slovník, je nutné vytvořit nový
   ``ChainMap``::

      >>> from collections import ChainMap
      >>> default = {"user": "admin", "password": "admin", "host": "localhost", "port": 12345}
      >>> config = ChainMap(default)
      >>> config
      ChainMap({'user': 'admin', 'password': 'admin', 'host': 'localhost', 'port': 12345})
      >>> config_new = config.new_child()
      >>> config_new
      ChainMap({}, {'user': 'admin', 'password': 'admin', 'host': 'localhost', 'port': 12345})
      >>> config_new = config.new_child({"host": "10.0.0.10", "port": 54321})
      >>> config_new
      ChainMap({'host': '10.0.0.10', 'port': 54321}, {'user': 'admin', 'password': 'admin', 'host': 'localhost', 'port': 12345})
      >>> config_new["host"]
      '10.0.0.10'
      >>> config_new["port"]
      54321

.. tip::

   Upravuj a maž klíče jen v těch slovnících, ve kterých existují, nikoliv jen
   z prvního slovníku::

      >>> from collections import ChainMap
      >>> class DeepChainMap(ChainMap):
      ...     def __setitem__(self, key, value):
      ...         for mapping in self.maps:
      ...             if key in mapping:
      ...                 mapping[key] = value
      ...                 return
      ...         self.maps[0][key] = value
      ...     def __delitem__(self, key):
      ...         for mapping in self.maps:
      ...             if key in mapping:
      ...                 del mapping[key]
      ...                 return
      ...         raise KeyError(key)
      ...
      >>> default = {"user": "admin", "password": "admin"}
      >>> real = {"password": "password"}
      >>> config = DeepChainMap(real, default)
      DeepChainMap({'password': 'password'}, {'user': 'admin', 'password': 'admin'})
      >>> config["user"] = "davie"
      DeepChainMap({'password': 'password'}, {'user': 'davie', 'password': 'admin'})
      >>> del config["password"]
      >>> config["password"]
      'admin'
      >>> del config["password"]
      >>> config["password"]
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        File "/usr/lib/python3.6/collections/__init__.py", line 883, in __getitem__
          return self.__missing__(key)            # support subclasses that define __missing__
        File "/usr/lib/python3.6/collections/__init__.py", line 875, in __missing__
          raise KeyError(key)
      KeyError: 'password'

Counter
^^^^^^^

Vytvoř slovník s počtem jednotlivých položek z ``iterable``::

   >>> from collections import Counter
   >>> count = Counter("Davie Badger")
   >>> count
   Counter({'a': 2, 'e': 2, 'D': 1, 'v': 1, 'i': 1, ' ': 1, 'B': 1, 'd': 1, 'g': 1, 'r': 1})
   >>> counter["a"]
   2

Vytvoř ``Counter`` z již předpřipraveného slovníku::

   >>> from collections import Counter
   >>> Counter(cats=0, dog=1)
   Counter({'dog': 1, 'cats': 0})
   >>> Counter({"cats": 0, "dog": 1})
   Counter({'dog': 1, 'cats': 0})

.. note::

   Pokud se klíč nenachází v ``Counter`` objektu, tak defaultně se vrátí nula::

      >>> from collections import Counter
      >>> count = Counter()
      >>> count["test"]
      0
      >>> count
      Counter()

.. tip::

   Zobraz nejvyskytovanější prvky::

      >>> from collections import Counter
      >>> count = Counter("Hello World!")
      >>> count.most_common(1)
      [('l', 3)]
      >>> count.most_common(3)
      [('l', 3), ('o', 2), ('H', 1)]
      >>> count.most_common()
      [('l', 3), ('o', 2), ('H', 1), ('e', 1), (' ', 1), ('W', 1), ('r', 1), ('d', 1), ('!', 1)]

   Zobraz nejméně vyskytované prvky::

      >>> from collections import Counter
      >>> count = Counter("Hello World!")
      >>>
      >>> # last 1
      ...
      >>> count.most_common()[:-1-1:-1]
      [('!', 1)]
      >>> count.most_common()[:-2:-1]
      [('!', 1)]
      >>>
      >>> # last 2
      ...
      >>> count.most_common()[:-2-1:-1]
      [('!', 1), ('d', 1)]
      >>> count.most_common()[:-3:-1]
      [('!', 1), ('d', 1)]
      >>>
      >>> # last 3
      ...
      >>> count.most_common()[:-3-1:-1]
      [('!', 1), ('d', 1), ('r', 1)]
      >>> count.most_common()[:-4:-1]
      [('!', 1), ('d', 1), ('r', 1)]

defaultdict
^^^^^^^^^^^

Vytvoř slovník, kde chybějící klíč se bude chovat jako konkrétní datový typ::

   >>> from collections import defaultdict
   >>> harvest = defaultdict(int)
   >>> harvest["apples"] += 1
   >>> harvest["bananas"] += 2
   >>> harvest
   defaultdict(<class 'int'>, {'apples': 1, 'bananas': 2})
   >>> harvest["apples"]
   1
   >>> harvest["bananas"]
   2
   >>> harvest["cherries"]
   0
   >>> harvest
   defaultdict(<class 'int'>, {'apples': 1, 'bananas': 2, 'cherries': 0})

Vytvoř slovník, kde chybějící klíč bude mít konkrétní výchozí hodnotu::

   >>> from collections import defaultdict
   >>> harvest = defaultdict(1)
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: first argument must be callable or None
   >>> harvest = defaultdict(lambda: 1)
   >>> harvest["apples"]
   1

.. note::

   Pokud ``defaultdict`` nemá zadanou výchozí hodnotu, bude se chovat stejně
   jako obyčejný slovník::

      >>> from collections import defaultdict
      >>> harvest = defaultdict()
      >>> harvest["apples"] += 3
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      KeyError: 'apples'

.. tip::

   Vytvoř rekurzivně chybějící klíče::

      >>> from collections import defaultdict
      >>> tree = lambda: defaultdict(tree)
      >>> harvest = tree()
      >>> harvest["fruit"]["berries"]["strawberries"] = 3
      >>> harvest
      defaultdict(<function <lambda> at 0x7f85817d36a8>, {'fruit': defaultdict(<function <lambda> at 0x7f85817d36a8>, {'berries': defaultdict(<function <lambda> at 0x7f85817d36a8>, {'strawberries': 3})})})
      >>> harvest["fruit"]["berries"]["strawberries"]
      3
      >>> harvest["fruit"]["berries"]["blueberries"]
      defaultdict(<function <lambda> at 0x7f85817d36a8>, {})

   Rekurzivně lze vytvořít klíče i pomocí ``dict`` objektu, avšak jen do
   první úrovně vnoření::

      >>> harvest = defaultdict(dict)
      >>> harvest["fruit"]["berries"] = 3
      >>> harvest["vegetable"]["roots"]["carrots"] = 3
      Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
      KeyError: 'roots'

OrderedDict
^^^^^^^^^^^

Vytvoř seřazený slovník včetně podpory pro obrácenou iteraci nad slovníky,
která chybí u klasického slovníku::

   >>> x = OrderedDict.fromkeys("abc")
   >>> for key in x:
   ...     print(key)
   ...
   a
   b
   c
   >>> for key in reversed(x):
   ...     print(key)
   ...
   c
   b
   a

.. note::

   Pomocí ``OrderedDict`` slovníku lze mít zpětně kompatibilní seřazený
   slovník i pro starší verze Pythonu než je 3.6.

.. tip::

   Vytvoř obrácený seřazený slovník::

      >>> x = OrderedDict.fromkeys("abc")
      >>> y = OrderedDict(reversed(x.items()))
      >>> y
      OrderedDict([('c', None), ('b', None), ('a', None)])

Ostatní
-------

enum
^^^^

Vytvoř manuálně speciální neměnitelnou třídu s pojmenovanými hodnotami::

   >>> from enum import Enum
   >>> class Color(Enum):
   ...     red = 255, 0, 0
   ...     green = 0, 255, 0
   ...     blue = 0, 0, 255
   ...
   >>> Color
   <enum 'Color'>
   >>> Color.red
   <Color.red: (255, 0, 0)>
   >>> Color["red"]
   <Color.red: (255, 0, 0)>
   >>> Color((255, 0, 0))
   <Color.red: (255, 0, 0)>
   >>> Color.red.name
   'red'
   >>> Color.red.value
   (255, 0, 0)
   >>> Color.red = "ff0000"
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
     File "/usr/lib/python3.6/enum.py", line 361, in __setattr__
       raise AttributeError('Cannot reassign members.')
   AttributeError: Cannot reassign members.
   >>> Color.red == (255, 0, 0)
   False
   >>> Color.red.value == (255, 0, 0)
   True
   >>> Color.red is Color.green
   False
   >>> Color.red is not Color.blue
   True
   >>> list(Color)
   [<Color.red: (255, 0, 0)>, <Color.green: (0, 255, 0)>, <Color.blue: (0, 0, 255)>]

Vytvoř automaticky ``Enum`` ze seznamu pojmenovaných hodnot::

   >>> from enum import Enum
   >>> Fruit = Enum("Fruit", ["apple", "banana", "cherry"])
   >>> Fruit.apple
   <Fruit.apple: 1>
   >>> Fruit.apple.name
   'apple'
   >>> Fruit.apple.value
   1
   >>> Fruit.banana
   <Fruit.banana: 2>
   >>> Fruit.cherry
   <Fruit.cherry: 3>

.. note::

   Pojmenované hodnoty mohou obsahovat aliasy::

      >>> from enum import Enum
      >>> class Fruit(Enum):
      ...     apple = 0
      ...     apples = 0
      ...     banana = 1
      ...     bananas = 1
      ...     cherry = 2
      ...     cherries = 2
      ...
      >>> Fruit(0)
      <Fruit.apple: 0>
      >>> Fruit["apples"]
      <Fruit.apple: 0>

   Pro zabránění vytváření aliasů lze použít ``unique`` dekorátor na ``Enum``
   třídě::

      >>> from enum import Enum, unique
      >>> @unique
      ... class Fruit(Enum):
      ...     apple = 0
      ...     apples = 0
      ...
      Traceback (most recent call last):
        File "<stdin>", line 2, in <module>
        File "/usr/lib/python3.6/enum.py", line 834, in unique
          (enumeration, alias_details))
      ValueError: duplicate values found in <enum 'Fruit'>: apples -> apple

.. tip::

   Jestliže pojmenované hodnoty obsahují jen celá čísla, lze dědit přímo z
   ``IntEnum`` třídy pro lepší porovnávání hodnot::

      >>> from enum import IntEnum
      >>> class Firewall(IntEnum):
      ...     disabled = 0
      ...     enabled = 1
      ...
      >>> Firewall
      <enum 'Firewall'>
      >>> Firewall.enabled
      <Firewall.enabled: 1>
      >>> Firewall.enabled == 1
      True
      >>> Firewall.disabled != 0
      False
      >>> Firewall.enabled is Firewall.enabled
      True
      >>> Firewall.disabled is Firewall.disabled
      False

PEPs
====

PEP_ je formální návrh pro vylepšení jazyka Pythonu jako takového. Mezi
nejznámější PEPy patří:

1. `PEP 8`_

   * konvence pro psání kódu

2. `PEP 20`_

   * filosofie pro psání kódu::

        >>> import this
        The Zen of Python, by Tim Peters

        Beautiful is better than ugly.
        Explicit is better than implicit.
        Simple is better than complex.
        Complex is better than complicated.
        Flat is better than nested.
        Sparse is better than dense.
        Readability counts.
        Special cases aren't special enough to break the rules.
        Although practicality beats purity.
        Errors should never pass silently.
        Unless explicitly silenced.
        In the face of ambiguity, refuse the temptation to guess.
        There should be one-- and preferably only one --obvious way to do it.
        Although that way may not be obvious at first unless you're Dutch.
        Now is better than never.
        Although never is often better than *right* now.
        If the implementation is hard to explain, it's a bad idea.
        If the implementation is easy to explain, it may be a good idea.
        Namespaces are one honking great idea -- let's do more of those!

.. _Awesome Python: https://github.com/vinta/awesome-python
.. _formátování řetězců: https://docs.python.org/3/library/string.html#format-specification-mini-language
.. _Google: http://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html#example-google
.. _IPython: https://ipython.org/index.html
.. _Mypy: https://github.com/python/mypy
.. _Numpy: http://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_numpy.html
.. _Ostatní výjimky: https://docs.python.org/3/library/exceptions.html
.. _PEP: https://www.python.org/dev/peps/
.. _PEP 8: https://www.python.org/dev/peps/pep-0008/
.. _PEP 20: https://www.python.org/dev/peps/pep-0020/
.. _pip: https://pip.pypa.io/en/stable/
.. _PyPI: https://pypi.python.org/pypi
