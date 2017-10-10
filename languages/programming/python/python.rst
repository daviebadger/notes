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

   Jsou-li nainstalované i jiné verze Pythonu, lze je spustit s označením
   vedlejší verze:

   .. code:: none

      $ python3.5
      Python 3.5.3+ (default, Jun  7 2017, 23:23:48)
      [GCC 6.3.0 20170519] on linux
      Type "help", "copyright", "credits" or "license" for more information.
      >>>

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

.. tip::

   Délka řádku v souboru včetně komentářů by neměla překročit počet 79 znaků::

      # Strašně dlouhý ukázkový komentář,
      # který je pro ilustraci rozložen do tří řádků,
      # namísto jednoho dlouhého řádku překračující limit 79 znaků.

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

* násobení (``*``)::

     >>> 2 * 1
     2
     >>> 3 * "a"
     'aaa'

* dělení:

  * beze zbytku (``/``)::

       >>> 2 / 1  # Division always returns a floating point number
       2.0

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

   Formátovaný řetězec lze ještě dále naformátovat::

      >>> "{}".format(123)
      '123'
      >>> "{:13}".format(123)
      '          123'
      >>> "{:>13}".format(123)
      '123          '
      >>> "{:^13}".format(123)
      '     123     '

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
      >>> is_active = not is_activate
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

      is_even = True if number % 2 else False

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
   >>> word = input("Enter word which contains only letters 'd' or 'g' or 'o': ")
   Enter word which contains only letters 'd' or 'g' or 'o': test
   >>> for letter in word:
   ...     if letter not in allowed_letters:
   ...         print(f"Word '{word}' is not allowed")
   ...         break
   ...
   Word 'test' is not allowed

.. tip::

   Spusť kód, pokud v cyklu nedošlo k jeho násilnému ukončení nebo jiné chybě::

      >>> allowed_letter = ["d", "g", "o"]
      >>> word = input("Enter word which contains only letters 'd' or 'g' or 'o': ")
      Enter word which contains only letters 'd' or 'g' or 'o': dog
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
   Hi

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

Vytvoř a zavolej vlastní Funkci s neomezeným počtem volitelných argumentů::

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
      >>> year = int(input("Enter year: "))
      Enter year: 1995
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

   U skriptů zpravidla existuje jedna hlavní funkce, která řídí běh programu::

      def main():
          print("Hello World!")


      if __name__ == "__main__":
          main()

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
   ...     if number * 2 == 0:
   ...         return True
   ...     return False
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
   delattr()       hash()        memoryviews()   set()

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
       >>> def test(): pass
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

  * vrať entici s výsledkem celočíselného dělení a zbytkem::

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

       >>> open("/etc/passwd")
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

  * převeď ``iterable`` na entici, je-li to možné::

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
    entic::

       >>> zip([1, 2, 3], ["a", "b", "c"])
       <zip object at 0x7fdb4258dc88>
       >>> list(zip([1, 2, 3], ["a", "b", "c"]))
       [(1, 'a'), (2, 'b'), (3, 'c')]

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


Pokročila syntaxe
=================

Datové typy
===========

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

N-tice
------

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

  * vrať množinu, kde jsou odstraněny prvky::

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

  * vrať libovolně odstraněný prvek z množiny::

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

Vytvoření slovníků
^^^^^^^^^^^^^^^^^^

::

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

Operace se slovníky
^^^^^^^^^^^^^^^^^^^

::

   >>> person = {"name": "Davie Badger", "age": 22}
   >>> len(person)
   2
   >>> person["name"]
   'Davie Badger'
   >>> person["sex"] = "male"
   >>> person
   {'name': 'Davie Badger', 'age': 22, 'sex': 'male'}
   >>> del person["sex"]
   >>> del person["sex"]
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   KeyError: 'sex'
   >>> "name" in person
   True
   >>> "sex" not in person
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

* ``.get(key, default=None)``

  * vrať hodnotu pro klíč ``key``, pokud existuje, jinak ``default`` hodnotu::

       >>> x = {"age": 22}
       >>> x.get("age")
       22
       >>> x.get("age", 23)
       22
       >>> x.get("sex", "male")
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

  * odstraň ze slovníku položku, dokud slovník není prázdny, jinak vyvolej
    ``KeyError``::

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
       >>> x.setdefault("sex", "male")
       >>> x
       {'age': 22, 'sex': 'male'}

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
       >>> x.update(sex="male")
       >>> x
       {'age': 23, sex: "male"}

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

TODO
====

* odmocnina (moduly)
* ostastní typy
* zalomení kódu
* třídy (dědičnost, kompozice)
* try except finally else
* except Exception pro zachycení jakékoliv výjimky
* vnořené seznamy [x][y]
* [number for number in numbers if number % 2 != 1] + vnořené
* pass u obyčejných vlastních exception
* enum třídy
* rozbalení sekvencí do proměnných, x, \*_, y
* vlastní iterable + její definice
* vlastní sekvence + její definice
* callable objekt definice (__call__ metoda)
* iterátor
* IO operace
* kontextový manažer
* global a nonlocal
* generátor
* NotImplemented objekt u vlastních objektů

.. _formátování řetězců: https://docs.python.org/3/library/string.html#format-specification-mini-language
.. _Google: http://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html#example-google
.. _IPython: https://ipython.org/index.html
.. _Mypy: https://github.com/python/mypy
.. _Numpy: http://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_numpy.html
