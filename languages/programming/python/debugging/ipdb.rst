======
 Ipdb
======
------------------------------------------------------
 Sloučený debugger z výchozí pdb debuggeru a IPythonu
------------------------------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user ipdb

Debugger
========

Spuštění a ukončení debuggeru
-----------------------------

Spuštení debuggeru:

* od počátku programu::

     $ cat file.py
     def say_hi():
         print("Hi!")


     say_hi()
     $ ipdb3 file.py
     > /home/davie/test/file.py(1)<module>()
     ----> 1 def say_hi():
           2     print("Hi!")
           3

     ipdb>

* od konkrétního místa v programu (breakpoint)::

     $ cat file.py
     day = 11
     month = 4
     year = 1995
     import ipdb; ipdb.set_trace()
     print(f"Today is {day}.{month}.{year}")
     $ python3 file.py
     > /home/davie/test/file.py(5)<module>()
           3 year = 1995
           4 import ipdb; ipdb.set_trace()
     ----> 5 print(f"Today is {day}.{month}.{year}")

     ipdb>

* až když program spadne::

     $ ipython --no-banner

     In [1]: import ipdb

     In [2]: try:
        ...:     print(x)
        ...: except NameError:
        ...:     ipdb.post_mortem()
        ...:
     > <ipython-input-2-5a54608b71d3>(2)<module>()
           1 try:
     ----> 2     print(x)
           3 except NameError:

     ipdb>

Ukončení debuggeru:

* ``q``::

     $ cat file.py
     $
     $ ipdb3 file.py
     > /home/davie/test/file.py(1)<module>()

     ipdb> q
     $

* ``exit``::

     $ cat file.py
     $
     $ ipdb3 file.py
     > /home/davie/test/file.py(1)<module>()

     ipdb> exit
     $

.. note::

   Ukončit debugger lze také klávesovou zkratkou pro ukončení shellu, tj.
   ``CTRL + d``.

.. tip::

   Standardně lze vidět jen tři řádky v každém kroku. Toto výchozí nastavení
   lze upravit pomocí argumentu ``context``::

      $ cat file.py
      day = 11
      month = 4
      year = 1995
      import ipdb; ipdb.set_trace(context=5)
      print(f"Today is {day}.{month}.{year}")
      $ python3 file.py
      > /home/davie/test/file.py(5)<module>()
            1 day = 11
            2 month = 4
            3 year = 1995
            4 import ipdb; ipdb.set_trace(context=5)
      ----> 5 print(f"Today is {day}.{month}.{year}")

      ipdb>

Příkazy
-------

Nápověda
^^^^^^^^

h[elp]
""""""

Zobraz seznam příkazů::

   ipdb> h

   Documented commands (type help <topic>):
   ========================================
   EOF    cl         disable  interact  next    psource  rv         unt
   a      clear      display  j         p       q        s          until
   alias  commands   down     jump      pdef    quit     source     up
   args   condition  enable   l         pdoc    r        step       w
   b      cont       exit     list      pfile   restart  tbreak     whatis
   break  continue   h        ll        pinfo   return   u          where
   bt     d          help     longlist  pinfo2  retval   unalias
   c      debug      ignore   n         pp      run      undisplay

   Miscellaneous help topics:
   ==========================
   exec  pdb

   ipdb> help

   Documented commands (type help <topic>):
   ========================================
   EOF    cl         disable  interact  next    psource  rv         unt
   a      clear      display  j         p       q        s          until
   alias  commands   down     jump      pdef    quit     source     up
   args   condition  enable   l         pdoc    r        step       w
   b      cont       exit     list      pfile   restart  tbreak     whatis
   break  continue   h        ll        pinfo   return   u          where
   bt     d          help     longlist  pinfo2  retval   unalias
   c      debug      ignore   n         pp      run      undisplay

   Miscellaneous help topics:
   ==========================
   exec  pdb

Zobraz nápovědu pro konkrétní debugger příkaz::

   ipdb> h n
   n(ext)
           Continue execution until the next line in the current function
           is reached or it returns.
   ipdb>

.. note::

   Pokud je třeba vytvořit proměnnou pro otestování, tak tato proměnná
   nesmí obsahovat stejný název jako zabudované příkazy v debuggeru::

      ipdb> h = 1
      *** No help for '1'

   Pro zamezení kolize proměnných je nutné použít prefix ``!``::

      ipdb> !h = 1
      ipdb> !h
      1

.. tip::

   Alternativně místo ``h`` lze použít i ``?``::

      ipdb> ? h
      h(elp)
              Without argument, print the list of available commands.
              With a command name as argument, print help about that command.
              "help pdb" shows the full pdb documentation.
              "help exec" gives help on the ! command.
      ipdb>

Navigace
^^^^^^^^

n[ext]
""""""

Spusť kód na daném řádku označený symbolem ``---->`` a skoč na další řádek::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/f1le.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> day
   *** NameError: name 'day' is not defined
   ipdb> n
   > /home/davie/test/file.py(2)<module>()
         1 day = 11
   ----> 2 month = 4
         3 year = 1995

   ipdb> day
   11

s[step]
"""""""

Spusť kód na daném řádku a skoč na další řádek nebo dovnitř funkce či metody::

   $ cat file.py
   def say_hi(name):
       print(f"Hi {name}!")


   say_hi("Davie")
   say_hi("Jacob")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 def say_hi(name):
         2     print(f"Hi {name}!")
         3

   ipdb> n
   > /home/davie/test/file.py(6)<module>()
         3
         4
   ----> 5 say_hi("Davie")

   ipdb> s
   --Call--
   > /home/davie/test/file.py(1)say_hi()
   ----> 1 def say_hi(name):
         2     print(f"Hi {name}!")
         3

   ipdb> n
   > /home/davie/test/file.py(2)say_hi()
         1 def say_hi(name):
   ----> 2     print(f"Hi {name}!")
         3

   ipdb> n
   Hi Davie!
   --Return--
   None
   > /home/davie/test/file.py(2)say_hi()
         1 def say_hi(name):
   ----> 2     print(f"Hi {name}!")
         3

   ipdb> n
   --Return--
   None
   > /home/davie/test/file.py(5)<module>()
         3
         4
         5 say_hi("Davie")

.. note::

   Pomocí příkazu ``n`` se nelze dostat dovnitř funkce::

      $ ipdb3 file.py
      > /home/davie/test/file.py(1)<module>()
      ----> 1 def say_hi(name):
            2     print(f"Hi {name}!")
            3

      ipdb> n
      > /home/davie/test/file.py(5)<module>()
            3
            4
      ----> 5 say_hi("Davie")

      ipdb> n
      Hi Davie!
      --Return--
      None
      > /home/davie/test/file.py(5)<module>()
            3
            4
      ----> 5 say_hi("Davie")

.. tip::

   Pomocí příkazu ``w[here]`` lze zjistit celé zanoření, kde se přesně nacházím
   po skoku dovnitř funkcí::

      $ cat file.py
      def say_hi(name):
          print(f"Hi {name}!")


      say_hi("Davie")
      $ ipdb3 file.py
      > /home/davie/test/file.py(1)<module>()
      ----> 1 def say_hi(name):
            2     print(f"Hi {name}!")
            3

      ipdb> n
      > /home/davie/test/file.py(5)<module>()
            3
            4
      ----> 5 say_hi("Davie")

      ipdb> s
      --Call--
      > /home/davie/test/file.py(1)say_hi()
      ----> 1 def say_hi(name):
            2     print(f"Hi {name}!")
            3

      ipdb> w
        /usr/lib/python3.6/bdb.py(431)run()
          430         try:
      --> 431             exec(cmd, globals, locals)
          432         except BdbQuit:

        <string>(1)<module>()

        /home/davie/test/file.py(5)<module>()
            3
            4
      ----> 5 say_hi("Davie")

      > /home/davie/test/file.py(1)say_hi()
      ----> 1 def say_hi(name):
            2     print(f"Hi {name}!")
            3

r[eturn]
""""""""

Spusť kód až na konec funkce a setrvej na posledním řádku funkce::

   $ cat file.py
   def say_hi(name):
       print(f"Hi {name}!")


   say_hi("Davie")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 def say_hi(name):
         2     print(f"Hi {name}!")
         3

   ipdb> n
   > /home/davie/test/file.py(5)<module>()
         3
         4
   ----> 5 say_hi("Davie")

   ipdb> s
   --Call--
   > /home/davie/test/file.py(1)say_hi()
   ----> 1 def say_hi(name):
         2     print(f"Hi {name}!")
         3

   ipdb> r
   Hi Davie!
   --Return--
   None
   > /home/davie/test/file.py(2)say_hi()
         1 def say_hi(name):
   ----> 2     print(f"Hi {name}!")
         3

   ipdb> n
   --Return--
   None
   > /home/davie/test/file.py(5)<module>()
         3
         4
   ----> 5 say_hi("Davie")

.. note::

   Mimo funkci se spustí kód až do konce programu.

.. tip::

   Vrátít se zpátky na místo, odkud byla funkce zavolána bez potřeby vidět
   znovu návratou hodnotu lze příkazem ``u[p]``::

      $ cat file.py
      def say_hi(name):
          print(f"Hi {name}!")


      say_hi("Davie")
      $ ipdb3 file.py
      > /home/davie/test/file.py(1)<module>()
      ----> 1 def say_hi(name):
            2     print(f"Hi {name}!")
            3

      ipdb> n
      > /home/davie/test/file.py(5)<module>()
            3
            4
      ----> 5 say_hi("Davie")

      ipdb> s
      --Call--
      > /home/davie/test/file.py(1)say_hi()
      ----> 1 def say_hi(name):
            2     print(f"Hi {name}!")
            3

      ipdb> r
      Hi Davie!
      --Return--
      None
      > /home/davie/test/file.py(2)say_hi()
            1 def say_hi(name):
      ----> 2     print(f"Hi {name}!")
            3

      ipdb> u
      > /home/davie/test/file.py(5)<module>()
            3
            4
      ----> 5 say_hi("Davie")

   Zpět dovnitř funkce se pak lze vrátit pomocí příkazu ``d[own]``::

      $ cat file.py
      def say_hi(name):
          print(f"Hi {name}!")


      say_hi("Davie")
      $ ipdb3 file.py
      > /home/davie/test/file.py(1)<module>()
      ----> 1 def say_hi(name):
            2     print(f"Hi {name}!")
            3

      ipdb> n
      > /home/davie/test/file.py(5)<module>()
            3
            4
      ----> 5 say_hi("Davie")

      ipdb> d
      *** Newest frame
      ipdb> s
      --Call--
      > /home/davie/test/file.py(1)say_hi()
      ----> 1 def say_hi(name):
            2     print(f"Hi {name}!")
            3

      ipdb> u
      > /home/davie/test/file.py(5)<module>()
            3
            4
      ----> 5 say_hi("Davie")

      ipdb> d
      > /home/davie/test/file.py(1)say_hi()
      ----> 1 def say_hi(name):
            2     print(f"Hi {name}!")
            3

unt[il]
"""""""

Pokračuj v exekuci kódu až do daného řádku::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> unt 3
   > /home/davie/test/file.py(3)<module>()
         2 month = 4
   ----> 3 year = 1995
         4 print(f"Today is {day}.{month}.{year}")

   ipdb> p year
   *** NameError: name 'year' is not defined
   ipdb> p month
   4

.. note::

   Pomocí ``unt`` příkazu lze efektivně nechat doběhnout smyčku namísto
   neustáleho mačkání ``n`` příkazu.

j[ump]
""""""

Skoč dopředu nebo dozadu na konkrétní řádek v souboru::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/f1le.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> j 3
   > /home/davie/test/file.py(3)<module>()
         2 month = 4
   ----> 3 year = 1995
         4 print(f"Today is {day}.{month}.{year}")

   ipdb> j 2
   > /home/davie/test/file.py(2)<module>()
         1 day = 11
   ----> 2 month = 4
         3 year = 1995

.. note::

   Při skočení na jiný řádek v souboru se budou předchozí řádky ignorovat
   a nebudou se vůbec spouštět::

      $ cat file.py
      day = 11
      month = 4
      year = 1995
      print(f"Today is {day}.{month}.{year}")
      $ ipdb3 file.py
      > /home/davie/test/file.py(1)<module>()
      ----> 1 day = 11
            2 month = 4
            3 year = 1995

      ipdb> j 3
      > /home/davie/test/file.py(3)<module>()
            2 month = 4
      ----> 3 year = 1995
            4 print(f"Today is {day}.{month}.{year}")

      ipdb> p month
      *** NameError: name 'month' is not defined

c[ontinue]
""""""""""

Pokračuj v exekuci kódu, dokud program nenarazí na další breakpoint::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> c
   Today is 11.4.1995
   The program finished and will be restarted
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> b 3
   Breakpoint 1 at /home/davie/test/file.py:3
   ipdb> c
   > /home/davie/test/file.py(3)<module>()
         2 month = 4
   1---> 3 year = 1995
         4 print(f"Today is {day}.{month}.{year}")

.. note::

   Pokud se v debuggeru nenachází breakpoint, tak se nechá program doběhnout
   a pak znova zrestartovat na začátek.

run
"""

Spusť odznova debugger::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> n
   > /home/davie/test/file.py(2)<module>()
         1 day = 11
   ----> 2 month = 4
         3 year = 1995

   ipdb> run
   Restarting file.py with arguments:

   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

.. note::

   Alernativně lze použít taktéž alias ``restart``.

.. tip::

   Pokud se jedná o skript, který příjímá argumenty pří spuštení programu
   z příkazového řádku, lze debugger restartovat i s těmito argumenty::

      $ cat file.py
      import sys

      print(sys.argv)
      $ ipdb3 file.py
      > /home/davie/test/file.py(1)<module>()
      ----> 1 import sys
            2
            3 print(sys.argv)

      ipdb> run 1 2 3 name=Davie
      Restarting file.py with arguments:
         1 2 3 name=Davie
      > /home/davie/test/file.py(1)<module>()
      ----> 1 import sys
            2
            3 print(sys.argv)

      ipdb> c
      ['file.py', '1', '2', '3', 'name=Davie']
      The program finished and will be restarted
      > /home/davie/test/file.py(1)<module>()
      ----> 1 import sys
            2
            3 print(sys.argv)

Kontext
^^^^^^^

p[rint]
"""""""

Použij funkci ``print`` na daný objekt::

   ipdb> people = [{"name": "Davie", "gender": "M", "age": 22}, {"name": "Jacob", "gender": "M", "age": 17}]
   ipdb> p people
   [{"name": "Davie", "gender": "M", "age": 22}, {"name": "Jacob", "gender": "M", "age": 17}]
   ipdb> p 1 * 1
   1

.. note::

   Použítí příkazu ``p`` pro vytisknutí objektu je daleko bezpečnější, než
   zobrazovat hodnotu objektu bez příkaz ``p``, kdy může nechtěně dojít ke
   spuštení příkazu v debuggeru::

      ipdb> !p = 1
      ipdb> p
      *** SyntaxError: unexpected EOF while parsing
      ipdb> p p
      1

pp[rint]
""""""""

Použij funkci ``pprint`` z modulu ``pprint`` na daný objekt::

   ipdb> people = people = [{"name": "Davie", "gender": "M", "age": 22}, {"name": "Jacob", "gender": "M", "age": 17}]
   ipdb> pp people
   [{'age': 22, 'gender': 'M', 'name': 'Davie'},
    {'age': 17, 'gender': 'M', 'name': 'Jacob'}]

.. tip::

   Zobraz všechny proměnné z lokálního nebo globálního jmenného prostoru::

      ipdb> pp locals()
      {'__annotations__': {},
       '__builtins__': <module 'builtins' (built-in)>,
       '__cached__': None,
       '__doc__': None,
       '__file__': 'file.py',
       '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x7f6ae6f908d0>,
       '__name__': '__main__',
       '__package__': None,
       '__spec__': None,
       'ipdb': <module 'ipdb' from '/home/davie/.local/lib/python3.6/site-packages/ipdb/__init__.py'>}
       ipdb> pp globals()
      {'__annotations__': {},
       '__builtins__': <module 'builtins' (built-in)>,
       '__cached__': None,
       '__doc__': None,
       '__file__': 'file.py',
       '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x7f6ae6f908d0>,
       '__name__': '__main__',
       '__package__': None,
       '__spec__': None,
       'ipdb': <module 'ipdb' from '/home/davie/.local/lib/python3.6/site-packages/ipdb/__init__.py'>}

a[rgs]
""""""

Zobraz argumenty pro danou funkci či metodu::

   $ cat file.py
   def say_hi(name):
       print(f"Hi {name}!")


   say_hi("Davie")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 def say_hi(name):
         2     print(f"Hi {name}!")
         3

   ipdb> n
   > /home/davie/test/file.py(5)<module>()
         3
         4
   ----> 5 say_hi("Davie")

   ipdb> s
   --Call--
   > /home/davie/test/file.py(1)say_hi()
   ----> 1 def say_hi(name):
         2     print(f"Hi {name}!")
         3

   ipdb> a
   name = 'Davie'

l[ist]
""""""

Zobraz více řádku okolo aktuálního řádku::

   $ cat file.py
   def say_hi(name):
       """
       Greet a user.

       Args:
           name (str): Name of user.
       """
       print(f"Hi {name}!")


   say_hi("Davie")


   def say_hello(name):
       """
       Greet a user.

       Args:
           name (str): Name of user.
       """
       print(f"Hi {name}!")


   say_hi("Jacob")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 def say_hi(name):
         2     """
         3     Greet a user.

   ipdb> l
   ----> 1 def say_hi(name):
         2     """
         3     Greet a user.
         4
         5     Args:
         6         name (str): Name of user.
         7     """
         8     print(f"Hi {name}!")
         9
        10
        11 say_hi("Davie")

   ipdb> n
   > /home/davie/test/file.py(11)<module>()
        10
   ---> 11 say_hi("Davie")
        12

   ipdb> l
         6         name (str): Name of user.
         7     """
         8     print(f"Hi {name}!")
         9
        10
   ---> 11 say_hi("Davie")
        12
        13
        14 def say_hello(name):
        15     """
        16     Greet a user.

.. note::

   Zpravidla se zobrazí pět řádku nahoru a dolu (celkem 11 řádků), je-li to
   možné. Řádky okolo lze zobrazit i pro konkrétní řádek::

      $ cat file.py
      def say_hi(name):
          """
          Greet a user.

          Args:
              name (str): Name of user.
          """
          print(f"Hi {name}!")


      say_hi("Davie")


      def say_hello(name):
          """
          Greet a user.

          Args:
              name (str): Name of user.
          """
          print(f"Hi {name}!")


      say_hi("Jacob")
      $ ipdb3 file.py
      > /home/davie/test/file.py(1)<module>()
      ----> 1 def say_hi(name):
            2     """
            3     Greet a user.

      ipdb> l 11
            6         name (str): Name of user.
            7     """
            8     print(f"Hi {name}!")
            9
           10
           11 say_hi("Davie")
           12
           13
           14 def say_hello(name):
           15     """
           16     Greet a user.

.. tip::

   Zobraz jen řádky od do::

      $ cat file.py
      def say_hi(name):
          """
          Greet a user.

          Args:
              name (str): Name of user.
          """
          print(f"Hi {name}!")


      say_hi("Davie")
      $ ipdb3 file.py
      > /home/davie/test/file.py(1)<module>()
      ----> 1 def say_hi(name):
            2     """
            3     Greet a user.

      ipdb> l 1,0
      ----> 1 def say_hi(name):

      ipdb> l 3,0
            3     Greet a user.

      ipdb> l 3,3
            3     Greet a user.

      ipdb> l 5,8
            5     Args:
            6         name (str): Name of user.
            7     """
            8     print(f"Hi {name}!")

ll
""

Zobraz všechny zdrojové kódu v daném rámci, ať už se jedná o funkci nebo
celý program::

   $ cat file.py
   def say_hi(name):
       """
       Greet a user.

       Args:
           name (str): Name of user.
       """
       print(f"Hi {name}!")


   say_hi("Davie")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 def say_hi(name):
         2     """
         3     Greet a user.

   ipdb> ll
   ----> 1 def say_hi(name):
         2     """
         3     Greet a user.
         4
         5     Args:
         6         name (str): Name of user.
         7     """
         8     print(f"Hi {name}!")
         9
        10
        11 say_hi("Davie")

   ipdb> n
   > /home/davie/test/file.py(11)<module>()
         9
        10
   ---> 11 say_hi("Davie")

   ipdb> s
   --Call--
   > /home/davie/test/file.py(1)say_hi()
   ----> 1 def say_hi(name):
         2     """
         3     Greet a user.

   ipdb> ll
   ----> 1 def say_hi(name):
         2     """
         3     Greet a user.
         4
         5     Args:
         6         name (str): Name of user.
         7     """
         8     print(f"Hi {name}!")
         9

.. note::

   Příkazem celým svým jménem zní ``longlist``.

Breakpointy
^^^^^^^^^^^

b[reak]
"""""""

Vytvoř trvalý breakpoint na konkrétním řádku::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> b 3
   Breakpoint 1 at /home/davie/test/file.py:3
   ipdb> c
   > /home/davie/test/file.py(3)<module>()
         2 month = 4
   1---> 3 year = 1995
         4 print(f"Today is {day}.{month}.{year}")

   ipdb> c
   Today is 11.4.1995
   The program finished and will be restarted
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
   1     3 year = 1995

   ipdb> c
   > /home/davie/test/file.py(3)<module>()
         2 month = 4
   1---> 3 year = 1995
         4 print(f"Today is {day}.{month}.{year}")

Vytvoř trvalý breakpoint na konkrétním řádku v jiném souboru::

   $ cat file.py
   """
   Showcase
   """

   from another_file import make_text_bold
   from another_file import make_text_italic


   def make_text_bold_and_italic(text):
       return make_text_bold(make_text_italic(text))


   print(make_text_bold_and_italic("test"))
   $ cat another_file.py
   def make_text_bold(text):
       return f"<b>{text}</b>"


   def make_text_italic(text):
       return f"<i>{text}</i>"
   $ ipdb3 file.py
   > /home/davie/test/file.py(3)<module>()
         2 Showcase
   ----> 3 """
         4

   ipdb> b another_file:5
   Breakpoint 1 at /home/davie/test/another_file.py:5
   ipdb> b another_file.py:5
   Breakpoint 2 at /home/davie/test/another_file.py:5
   ipdb> c
   > /home/davie/test/another_file.py(5)<module>()
         4
   2---> 5 def make_text_italic(text):
         6     return f"<i>{text}</i>"

Vytvoř trvalý breakpoint na konkrétní funkci::

   $ cat file.py
   """
   Showcase
   """

   from another_file import make_text_bold
   from another_file import make_text_italic


   def make_text_bold_and_italic(text):
       return make_text_bold(make_text_italic(text))


   print(make_text_bold_and_italic("test"))
   $ ipdb3 file.py
   > /home/davie/test/file.py(3)<module>()
         2 Showcase
   ----> 3 """
         4

   ipdb> b make_text_bold_and_italic
   Breakpoint 1 at /home/davie/test/file.py:9
   ipdb> c
   > /home/davie/test/file.py(10)make_text_bold_and_italic()
   1     9 def make_text_bold_and_italic(text):
   ---> 10     return make_text_bold(make_text_italic(text))
        11

   ipdb>

Vypiš všechny trvalé breakpointy v debuggeru::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> b 2
   Breakpoint 1 at /home/davie/test/file.py:2
   ipdb> b 3
   Breakpoint 2 at /home/davie/test/file.py:3
   ipdb> b 4
   Breakpoint 3 at /home/davie/test/file.py:4
   ipdb> b
   Num Type         Disp Enb   Where
   1   breakpoint   keep yes   at /home/davie/test/file.py:2
   2   breakpoint   keep yes   at /home/davie/test/file.py:3
   3   breakpoint   keep yes   at /home/davie/test/file.py:4

.. tip::

   Vytvoř breakpoint jen v případě, pokud je podmínka platná pro jeho
   vytvoření::

      $ cat file.py
      for number in range(10):
          print(number)
      $ ipdb3 file.py
      > /home/davie/test/file.py(1)<module>()
      ----> 1 for number in range(10):
            2     print(number)

      ipdb> b 2, number % 2 != 0
      Breakpoint 1 at /home/davie/test/file.py:2
      ipdb> c
      0
      > /home/davie/test/file.py(2)<module>()
            1 for number in range(10):
      1---> 2     print(number)

      ipdb> p number
      1

   Podmínku lze dodatečně upravit pomocí příkazu ``condition``::

      > /home/davie/test/file.py(1)<module>()
      ----> 1 for number in range(10):
            2     print(number)

      ipdb> b 2, number % 2 == 0
      Breakpoint 1 at /home/davie/test/file.py:2
      ipdb> b
      Num Type         Disp Enb   Where
      1   breakpoint   keep yes   at /home/davie/test/file.py:2
         stop only if number % 2 == 0
      ipdb> condition 1 number % 2 != 0
      New condition set for breakpoint 1.
      ipdb> b
      Num Type         Disp Enb   Where
      1   breakpoint   keep yes   at /home/davie/test/file.py:2
         stop only if number % 2 != 0

tbreak
""""""

Vytvoř dočasný breakpoint, který se smaže při zastavení debuggeru na daném
místě::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> tbreak 3
   Breakpoint 1 at /home/davie/test/file.py:3
   ipdb> c
   Deleted breakpoint 1 at /home/davie/test/file.py:3
   > /home/davie/test/file.py(3)<module>()
         2 month = 4
   ----> 3 year = 1995
         4 print(f"Today is {day}.{month}.{year}")

   ipdb> b
   ipdb>

commands
""""""""

Spusť příkazy v daném breakpointu::

   $ cat file.py
   for number in range(10):
       print(number)
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 for number in range(10):
         2     print(number)

   ipdb> b 2
   Breakpoint 1 at /home/davie/test/file.py:2
   ipdb> b
   Num Type         Disp Enb   Where
   1   breakpoint   keep yes   at /home/davie/test/file.py:2
   ipdb> commands 1
   (com) p number
   (com) p number >= 0
   (com) end
   ipdb> c
   0
   True
   > /home/davie/test/file.py(2)<module>()
         1 for number in range(10):
   1---> 2     print(number)


disable
"""""""

Deaktivuj daný breakpoint::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> b 3
   Breakpoint 1 at /home/davie/test/file.py:3
   ipdb> b
   Num Type         Disp Enb   Where
   1   breakpoint   keep yes   at /home/davie/test/file.py:3
   ipdb> disable 1
   Disabled breakpoint 1 at /home/davie/test/file.py:3
   ipdb> b
   Num Type         Disp Enb   Where
   1   breakpoint   keep no    at /home/davie/test/file.py:3

.. tip::

   Pokud je třeba daný breakpoint deaktivovat jen N-krát, lze použít příkaz
   ``ignore``::

      $ cat file.py
      for number in range(10):
          print(number)
      $ ipdb3 file.py
      > /home/davie/test/file.py(1)<module>()
      ----> 1 for number in range(10):
            2     print(number)

      ipdb> b 2
      Breakpoint 1 at /home/davie/test/file.py:2
      ipdb> b
      Num Type         Disp Enb   Where
      1   breakpoint   keep yes   at /home/davie/test/file.py:2
      ipdb> ignore 1 3
      Will ignore next 3 crossings of breakpoint 1.
      ipdb> c
      0
      1
      2
      > /home/davie/test/file.py(2)<module>()
            1 for number in range(10):
      1---> 2     print(number)

      ipdb> p number
      3

enable
""""""

Znova aktivuj daný breakpoint::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> b 3
   Breakpoint 1 at /home/davie/test/file.py:3
   ipdb> b
   Num Type         Disp Enb   Where
   1   breakpoint   keep yes   at /home/davie/test/file.py:3
   ipdb> disable 1
   Disabled breakpoint 1 at /home/davie/test/file.py:3
   ipdb> b
   Num Type         Disp Enb   Where
   1   breakpoint   keep no    at /home/davie/test/file.py:3
   ipdb> enable 1
   Enabled breakpoint 1 at /home/davie/test/file.py:3
   ipdb> b
   Num Type         Disp Enb   Where
   1   breakpoint   keep yes   at /home/davie/test/file.py:3

cl[ear]
"""""""

Smaž trvale konkrétní breakpoint::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> b 3
   Breakpoint 1 at /home/davie/test/file.py:3
   ipdb> b
   Num Type         Disp Enb   Where
   1   breakpoint   keep yes   at /home/davie/test/file.py:3
   ipdb> cl 1
   Deleted breakpoint 1 at /home/davie/test/file.py:3
   ipdb> b
   ipdb>

Smaž trvale všechny breakpointy::

   $ cat file.py
   day = 11
   month = 4
   year = 1995
   print(f"Today is {day}.{month}.{year}")
   $ ipdb3 file.py
   > /home/davie/test/file.py(1)<module>()
   ----> 1 day = 11
         2 month = 4
         3 year = 1995

   ipdb> b 2
   Breakpoint 1 at /home/davie/test/file.py:2
   ipdb> b 3
   Breakpoint 2 at /home/davie/test/file.py:3
   ipdb> b 4
   Breakpoint 3 at /home/davie/test/file.py:4
   ipdb> b
   Num Type         Disp Enb   Where
   1   breakpoint   keep yes   at /home/davie/test/file.py:2
   2   breakpoint   keep yes   at /home/davie/test/file.py:3
   3   breakpoint   keep yes   at /home/davie/test/file.py:4
   ipdb> cl
   Clear all breaks? y
   Deleted breakpoint 1 at /home/davie/test/file.py:2
   Deleted breakpoint 2 at /home/davie/test/file.py:3
   Deleted breakpoint 3 at /home/davie/test/file.py:4
   ipdb> b
   ipdb>
