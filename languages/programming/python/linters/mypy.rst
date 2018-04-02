======
 Mypy
======
------------------------------
 Kontrolovač typových anotací
------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user mypy

Ovládání
========

mypy
----

Zkontroluj správné používání datových typů v souboru::

   $ cat file.py
   print(abs("0"))
   $ mypy file.py
   file.py:1: error: Argument 1 to "abs" has incompatible type "str"; expected SupportsAbs[<nothing>]

Zkontroluj správné používání datových typů v adresáři::

   $ ls test
   a.py  b.py  c.py
   $ mypy test
   test/c.py:1: error: Argument 1 to "abs" has incompatible type Dict[<nothing>, <nothing>]; expected SupportsAbs[<nothing>]
   test/b.py:1: error: Argument 1 to "abs" has incompatible type "Tuple[]"; expected SupportsAbs[<nothing>]
   test/a.py:1: error: Argument 1 to "abs" has incompatible type List[<nothing>]; expected SupportsAbs[<nothing>]

.. tip::

   Stejně jako u jiných kontrolovaču, i zde jde pomocí komentářů ignorovat
   chyby::

      $ cat file.py
      import foo
      $ mypy file.py
      file.py:1: error: Cannot find module named 'foo'
      file.py:1: note: (Perhaps setting MYPYPATH or using the "--ignore-missing-imports" flag would help)
      $ echo "import foo  # type: ignore" > file.py
      $ mypy file.py
      $

   Komentáře lze kombinovat i s jinými specifickými komentáři, např. pro
   ``flake8``::

      $ cat file.py
      import foo  # type: ignore
      $ flake8 file.py
      file.py:1:1: F401 'foo' imported but unused
      $ echo "import foo  # type: ignore  # noqa" > file.py
      $ mypy file.py
      $ flake8 file.py
      $

Odbočka k typování
^^^^^^^^^^^^^^^^^^

Základní typy
"""""""""""""

* ``int``::
* ``float``::
* ``bool``::
* ``str``
* ``list``
* ``tuple``
* ``set``
* ``frozenset``
* ``dict``

.. note::

   Ze základních typů lze použít i speciální objekt ``object`` pro povolení
   jakéhokoliv jiného typu::

      $ cat file.py
      def say_hi(name: object) -> object:
          return name

      print(say_hi("Davie"))
      $ mypy file.py
      $

   Avšak problém nastává v případě, kdy volám na daném objektu metody, které
   ve skutečnosti objekt ``object`` z funkce ``object`` nemá nebo nepodporuje
   konkrétní operace::

      $ cat file.py
      def say_hi(name: object) -> object:
          return name + " " + name * 3


      print(say_hi("Davie"))
      $ python3 file.py
      Davie DavieDavieDavie
      $ mypy file.py
      file.py:2: error: Unsupported left operand type for + ("object")
      file.py:2: error: Unsupported operand types for * ("object" and "int")

   Proto je bezpečnější používat speciální typ ``Any`` z modulu ``typing``
   pro specifikování jakéhokoliv typu::

      $ cat file.py
      from typing import Any


      def say_hi(name: Any) -> Any:
          return name + " " + name * 3


      print(say_hi("Davie"))
      $ python3 file.py
      Davie DavieDavieDavie
      $ mypy file.py
      $

.. tip::

   Jako typy lze použít i původní třídy, ze kterých vznikly objekty. Tyto
   třídy je možné importovat přímo nebo postačí použít cestu k nim v řetězci::

      $ cat file.py
      class Person(object):
          pass


      person_object: Person = Person()
      person_object_str: "Person" = Person()  # Avoid cyclic imports e.g.
      $ mypy file.py
      $

Rozšiřující základní typy
"""""""""""""""""""""""""

Typy rozšiřující základní typy:

* ``List[]``::

     $ cat file.py
     from typing import List

     numbers: List[int] = [1, 2, 3]
     $ mypy file.py
     $

* ``Tuple[]``::

     $ cat file.py
     from typing import Tuple

     one_tuple: Tuple[int] = (0,)
     two_tuple: Tuple[int, str] = (0, "apple")
     n_tuple: Tuple[int, ...] = (1, 2, 3)
     $ mypy file.py
     $

* ``Set[]``::

     $ cat file.py
     from typing import Set

     numbers: Set[int] = {1, 2, 3}
     $ mypy file.py
     $

* ``FrozenSet[]``::

     $ cat file.py
     from typing import FrozenSet

     numbers: FrozenSet[int] = frozenset({1, 2, 3})
     $ mypy file.py
     $

* ``Dict[]``::

     $ cat file.py
     from typing import Dict

     mapping: Dict[str, int] = {"a": 1, "b": 2, "c": 3}
     $ mypy file.py
     $

.. note::

   Ačkoliv se ``mypy`` snaží samo odvodit patřičné typy z kódu, tak i přesto
   existují situace, kdy toho odvození selže, např. u prázdných slovníků či
   sekvencí, které je třeba více specifikovat::

      $ cat file.py
      x = []
      $ mypy file.py
      file.py:1: error: Need type annotation for variable
      $ cat another_file.py
      from typing import List

      x: List[int] = []

      x.append(0)
      x.append(1)
      $ mypy another_file.py
      $

.. tip::

   TypedDict from mypy-extensions?

Typy podle protokolů
""""""""""""""""""""

* ``Sequence``::

     $ cat file.py
     from typing import Sequence  # Immutable, mutable is MutableSequence
     from typing import TypeVar

     T = TypeVar("T")


     def first(seq: MutableSequence[T]) -> T:
         return seq[0]


     print(first(["a", "b", "c"]))
     print(first(("a", "b", "c")))
     print(first("abc"))
     $ python3 file.py
     a
     a
     a
     $ mypy file.py
     %

* ``Iterator``::

     $ cat file.py
     from typing import Iterator


     def numbers(number: int) -> Iterator[int]:
         for n in range(number):
             yield n


     print(list(numbers(10)))
     $ python3 file.py
     [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
     $ mypy file.py
     $

* ``Callable``::

     $ cat file.py
     from typing import Callable
     from typing import List
     from typing import Sequence


     def is_even(value: int) -> bool:
         return value % 2 == 0


     def filter_even(elements: Sequence[int],
                     function: Callable[[int], bool]
                     ) -> List[int]:
         # Unlimeted arguments are marked as ..., e.g. Callable[..., bool]
         return list(filter(function, elements))


     print(list(filter_even(range(10), is_even)))
     $ python3 file.py
     [0, 2, 4, 6, 8]
     $ mypy file.py
     $

.. note::

   Další typy pro jednotlivé abstraktní třídy z modulu ``collections.abc`` lze
   najít v ``typing`` modulu.

.. tip::

   Pokud jsou pokročilé typy moc dlouhé v rámci jejich definice, lze si
   vypomoct aliasy::

      $ cat file.py
      from typing import Sequence
      from typing import TypeVar

      Numbers = TypeVar("Numbers", int, float)
      Vector = Sequence[Numbers]


      def sum_vector(vector: Vector) -> int:
          return sum(vector)


      print(sum_vector([1, 2, 3]))
      print(sum_vector((1.0, 2.0, 3.0)))
      $ python3 file.py
      6
      6.0
      $ mypy file.py
      $

   Logicky lze použít i speciální typ ``Union`` namísto ``TypeVar`` pro
   povolení alespoň jednoho typu z předepsaného seznamu možností, avšak na
   rozdíl od ``TypeVar`` musí být i návratová hodnota u funkcí ``Union``::

      $ cat file.py
      from typing import Sequence
      from typing import TypeVar

      Numbers = TypeVar("Numbers", int, float)
      Vector = Sequence[Numbers]


      def sum_vector(vector: Vector) -> int:
          return sum(vector)


      print(sum_vector([1, 2, 3]))
      print(sum_vector((1.0, 2.0, 3.0)))
      $ python3 file.py
      6
      6.0
      $ mypy file.py
      file.py:9: error: Incompatible return value type (got "Union[int, float]", expected "int")
      $ cat another_file.py
      from typing import Sequence
      from typing import Union

      Numbers = Union[int, float]
      Vector = Sequence[Numbers]


      def sum_vector(vector: Vector) -> Numbers:
          return sum(vector)


      print(sum_vector([1, 2, 3]))
      print(sum_vector((1.0, 2.0, 3.0)))
      $ python3 another_file.py
      6
      6.0
      $ mypy another_file.py
      $

   Samotný ``TypeVar`` jen s názvem typu se chová stejně jako typ ``object``::

      $ cat file.py
      from typing import TypeVar

      T = TypeVar("T")


      def say_hi(name: T) -> str:
          return f"Hi {name}"


      def say_hello(name: T) -> str:
          name = name.upper()

          return f"Hello {name}"


      print(say_hi("Davie"))
      print(say_hello("Jacob"))
      $ python3 file.py
      Hi Davie
      Hello JACOB
      $ mypy file.py
      file.py:11: error: "T" has no attribute "upper"

Typy podle kolekcí
""""""""""""""""""

* ``Deque``::

     $ cat file.py
     from typing import Deque

     d: Deque[int] = Deque()

     d.appendleft(0)
     d.append(1)
     $ mypy file.py
     $

* ``NamedTuple``::

     $ cat file.py
     from typing import NamedTuple


     class PersonA(NamedTuple):
         name: str
         age: int


     PersonB = NamedTuple("PersonB", [("name", str), ("age", int)])

     p1 = PersonA("Davie", 22)
     p2 = PersonB("Davie", 22)

     print(p1.name == p2.name)
     $ python3 file.py
     True
     $ mypy file.py
     $

* ``ChainMap``::

     $ cat file.py
     from typing import Any
     from typing import ChainMap

     default = {"user": "admin", "password": "admin", "host": "localhost", "port": 12345}
     real = {"user": "davie", "password": "password"}

     config: ChainMap[str, Any] = ChainMap(real, default)

     print(config)
     $ python3 file.py
     ChainMap({'user': 'davie', 'password': 'password'}, {'user': 'admin', 'password': 'admin', 'host': 'localhost', 'port': 12345})
     $ mypy file.py
     $

* ``Counter``::

     $ cat file.py
     from typing import Counter

     count: Counter[str] = Counter("Davie Badger")

     print(count)
     $ python3 file.py
     Counter({'a': 2, 'e': 2, 'D': 1, 'v': 1, 'i': 1, ' ': 1, 'B': 1, 'd': 1, 'g': 1, 'r': 1})
     $ mypy file.py
     $

* ``DefaultDict``::

     $ cat file.py
     from typing import DefaultDict

     stats: DefaultDict[str, int] = DefaultDict(int)

     print(stats["home"])
     print(stats["away"])
     $ python3 file.py
     0
     0
     $ mypy file.py
     0

.. note::

   Tyto kolekce se již neimportují z ``collections``, ale používají se přímo
   třídy z ``typing`` modulu.

Speciální typy
""""""""""""""

* ``Any``::

     $ cat file.py
     from typing import Any

     def print_args_and_kwargs(*args: Any, **kwargs: Any) -> None:
         print(args)
         print(kwargs)


     print_args_and_kwargs(1, 2, 3, name="Davie")
     $ python3 file.py
     (1, 2, 3)
     {'name': 'Davie'}
     $ mypy file.py
     $

* ``Optional``::

     $ cat file.py
     from typing import Any
     from typing import Optional


     def greet_user(name: Any = None) -> Optional[str]:
         return f"Hello {name}" if name is not None else None


     print(greet_user())
     print(greet_user("Davie"))
     $ python3 file.py
     None
     Hello Davie
     $ mypy file.py
     $

* ``Union``::

     $ cat file.py
     from typing import Union

     x: Union[int, str]

     x = 0
     x = "1"
     $ mypy file.py
     $

.. note::

   V ``typing`` modulu lze nalézt i další speciální typy, např. pro regulární
   výrazy::

      $ cat file.py
      import re
      import typing

      pattern = re.compile(r"[0-9]$")


      def is_valid(pattern: typing.Pattern, value: str) -> bool:
          return bool(pattern.match(value))


      print(is_valid(pattern, "0"))
      print(is_valid(pattern, "123"))
      $ python3 file.py
      True
      False
      $ mypy file.py
      $

.. tip::

   Speciální typ ``Any`` z modulu ``typing`` lze použít i pro dynamickou
   proměnnou, která střída datové typy::

      $ cat file.py
      x = 0
      x = "0"
      $ mypy file.py
      file.py:2: error: Incompatible types in assignment (expression has type "str", variable has type "int")
      $ cat another_file.py
      from typing import Any

      x: Any = 0
      x = "0"
      $ mypy another_file.py
      $

mypy --strict-optional
^^^^^^^^^^^^^^^^^^^^^^

Povol striktnější typovou kontrolu u ``None`` hodnot::

   $ cat file.py
   from typing import Optional


   def say_hi(name: str = "Noname") -> Optional[str]:
       if name != "Noname":
           return f"Hi {name}"

       return None


   print(say_hi() + "!")  # Could be None + "!"
   $ mypy file.py
   $ mypy --strict-optional file.py
   file.py:11: error: Unsupported left operand type for + (some union)

Konfigurace
===========

Ulož volby příkazu ``mypy`` do konfiguračního souboru ``setup.cfg``::

   $ cat setup.cfg
   [mypy]
   strict_optional = true
