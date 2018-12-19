======
 Mock
======
-----------------------------------------
 Nahrazovač realného kódu falešným kódem
-----------------------------------------

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user pytest-mock

Ovládání
========

Plugin poskytuje fixturu ``mocker``, pomocí které lze snadno mockovat objekty
v testech. Jedná o obal nad standardní knihovnou ``unittest.mock``, díky
kterému se snadnějí pracuje s mocky bez použití kontextových manažeru.

mocker.patch
------------

Nahraď hodnotu v globální proměnné / konstantě jinou hodnotou::

   $ cat test_variable.py
   boolean = False


   def test_boolean(mocker):
       assert __name__ == "test_variable"  # module name

       mocker.patch("test_variable.boolean", True)

       assert boolean

Nahraď vlastní funkci jinou funkcí::

   $ cat test_function.py
   def add(x, y):
       return x + y


   def test_add(mocker):
       mocker.patch("test_function.add", lambda *args, **kwargs: 0)

       assert add(1, 1) == 0

Nahraď zabudovanou funkci jinou funkci::

   $ cat test_builtin_function.py
   def test_abs(mocker):
       mocker.patch("builtins.abs", lambda number: -number)

       assert abs(1) == -1

Nahraď volanou funkci uvnitř funkce jinou funkcí::

   $ cat test_function_call.py
   import os
   from pathlib import Path


   def remove_file(file):
       os.remove(file)


   def test_remove_file(mocker):
       mocker.patch("os.remove", lambda *args, **kwargs: None)

       file = "test_function_call.py"
       remove_file(file)

       assert Path(file).exists()

Nahraď třídu jinou třídou::

   $ cat test_class.py
   class Foo(object):
       def foo(self):
           pass


   def test_class(mocker):
       class Bar(object):
           def bar(self):
               pass

       mocker.patch("test_class.Foo", Bar)

       assert "bar" in dir(Foo)
       assert "foo" not in dir(Foo)

Nahraď proměnnou na tříde jinou hodnotou::

   $ cat test_class_variable.py
   class Foo(object):
       x = 0


   def test_class_variable(mocker):
       mocker.patch("test_class_variable.Foo.x", 1)

       assert Foo.x == 1

Nahraď atribut na třídě jinou hodnotou::

   $ cat test_class_attribute.py
   class Foo(object):
       @property
       def foo(self):
           return "foo"


   def test_class_attribute(mocker):
       mocker.patch("test_class_attribute.Foo.foo", "bar")

       assert Foo().foo == "bar"

Nahraď instanční atribut jinou hodnotou::

   $ cat test_instance_attribute.py
   class Foo(object):
       def __init__(self, x):
           self.x = x


   def test_init(mocker):
       def fake_init(self, *args, **kwargs):
           self.x = 0

       mocker.patch("test_instance_attribute.Foo.__init__", fake_init)

       assert Foo(1).x == 0

Nahraď metody na tříde jinými funkcemi::

   $ cat test_class_method.py
   class Foo(object):

       def foo(self):
           return "foo"

       @classmethod
       def class_foo(cls):
           return "foo"

       @staticmethod
       def static_foo():
           return "foo"


   def test_class_method(mocker):
       mocker.patch("test_class_method.Foo.foo", lambda self: "bar")
       mocker.patch("test_class_method.Foo.class_foo", lambda cls: "bar")
       mocker.patch("test_class_method.Foo.static_foo", lambda: "bar")

       assert Foo().foo() == "bar"
       assert Foo.class_foo(Foo) == "bar"
       assert Foo.static_foo() == "bar"

.. note::

   Při mockovaní objektů pomocí patche je třeba dávat pozor na cestu k danému
   objektu, která vždy začína názvem daného modulu, či balíčku nebo názvem
   ``builtins`` pro zabudované funkce.

.. tip::

   Při nahrazování funkcí či metod, obecně callable objektů, není nutné vždy
   uvádět vlastní falešnou náhradu. Místo toho lze použít defaultní falešný
   objekt ``MagicMock``, který lze uložit do proměnné a později kontrolovat
   práci s timto objektem::

      $ cat test_magic_mock.py
      def add(x, y):
          return x + y


      def test_magic_mock(mocker):
          mock_add = mocker.patch("test_magic_mock.add")

          assert isinstance(add, mocker.MagicMock)
          assert add(1, 1) != 2

          mock_add.assert_called_once_with(1, 1)

   Tyto mock objekty lze dále konfigurovat, aby vždy vracely stejnou či různé
   návratové hodnoty nebo také vyvolaly výjimku po zavolání::

      $ cat test_return.py
      import pytest


      def test_static_return(mocker):
          mocker.patch("builtins.abs", return_value=0)

          assert abs(1) == 0


      def test_dynamic_return(mocker):
          mocker.patch("builtins.abs", side_effect=range(3))

          assert abs(1) == 0
          assert abs(1) == 1
          assert abs(1) == 2


      def return_values(number):
          if number >= 1:
              return 1
          elif number <= -1:
              return -1
          else:
              return 0


      def test_dynamic_conditional_return(mocker):
          mocker.patch("builtins.abs", side_effect=return_values)

          assert abs(5) == 1
          assert abs(0) == 0
          assert abs(-5) == -1


      def test_exception(mocker):
          mocker.patch("builtins.abs", side_effect=ValueError("bad value"))

          with pytest.raises(ValueError) as err:
              abs(0)

          assert "bad value" in str(err)

Odbočka k Mock objektům
^^^^^^^^^^^^^^^^^^^^^^^

V zásadě existují dva hlavní mock objekty ``Mock`` a ``MagicMock``. přičemž
druhý jmenovaný má navíc od první možnosti implementované výchozí hodnoty v
magických metodách::

   $ cat test_mocks.py
   import pytest


   def test_mocks(mocker):
       mock = mocker.Mock()
       magic_mock = mocker.MagicMock()

       dir(mock) == dir(magic_mock)

       with pytest.raises(TypeError):
           int(mock)
           float(mock)
           bool(mock)
           len(mock)

       assert int(magic_mock) == 1
       assert float(magic_mock) == 1.0
       assert bool(mock)
       assert not len(magic_mock)

Oba mock objekty mají shodně následující atributy a metody k testovacím
účelům:

* ``assert_any_call(*args, **kwargs)``

  * ověř, že mock byl zavolán kdykoliv s danými ``args`` a ``kwargs`` argumenty

* ``assert_called_with(*args, **kwargs)``

  * ověř, že mock byl zavolán naposled s danými ``args`` a ``kwargs`` argumenty

* ``assert_called_once_with(*args, **kwargs)``

  * ověř, že mock byl zavolán jen jednou s danýmí ``args`` a ``kwargs``
    argumenty

* ``assert_not_called()``

  * ověř, že mock nebyl vůbec zavolán::

    $ cat test_assert_not_called(mocker):
    def test_called(mocker):
        mock = mocker.Mock()

        mock.assert_not_called()

* ``call_count``

  * počet volání na mocku::

    $ cat test_call_count(mocker):
    def test_called(mocker):
        mock = mocker.Mock()
        mock()

        assert mock.call_count == 1

* ``called``

  * zda byl mock zavolán nebo ne::

    $ cat test_called(mocker):
    def test_called(mocker):
        mock = mocker.Mock()
        mock()

        assert mock.called

* ``mock_calls``

  * seznam všech zavolaných metod včetně magických metod a řetězených metod::

    $ cat test_mock_calls(mocker):
    def test_asserts(mocker):
        mock_object = mocker.MagicMock()
        mock_object(0, y=1)
        mock_object.x.y.z()
        int(mock_object)

        assert [
            mocker.call(0, y=1),
            mocker.call.x.y.z(),
            mocker.call.__int__()
        ] == mock_object.mock_calls

        # or using mocker.ANY for whatever arguments

        assert [mocker.call(0, y=mocker.ANY), mocker.ANY, mocker.ANY] == mock_object.mock_calls

Další atributy a metody na mock objektech lze nalézt v
`dokumentaci <https://docs.python.org/3/library/unittest.mock.html#unittest.mock.Mock>`_.

.. note::

   Ačkoliv je ``MagicMock`` výchozím mock objektem v ``patch`` funkcích, tak je
   daleko bezpečnější použít základní ``Mock`` objekt a magické metody si
   definovat sám. Díky tomu lze předejít situacím, kdy testy procházejí díky
   výchozím hodnotám magického mocku, ačkoliv by měly selhávat.

.. tip::

   V případě property atributů a proměnných na tříde je třeba použít jiný mock
   objekt a to ``PropertyMock``::

      $ cat test_property_mock.py
      class Foo(object):
          @property
          def foo(self):
              return "foo"


      def test_property_mock(mocker):
          mock_foo = mocker.PropertyMock(return_value="bar")

          mocker.patch("test_property_mock.Foo.foo", mock_foo)

          assert Foo().foo == "bar"

          mock_foo.assert_called_once_with()

   Pokud chci ``PropertyMock`` přidat do ``MagicMock`` třídy, tak je třeba to
   provést pomocí ``ŧype`` funkce kvůli specifické povaze tohoto mocku::

      $ cat test_add_property_mock.py
      def test_add_property_mock(mocker):
          mock = mocker.MagicMock()
          prop = mocker.PropertyMock(return_value=0)

          type(mock).prop = prop

          assert mock.prop == 0

          prop.assert_called_once_with()

mocker.patch.dict
-----------------

Nahraď klíče ve slovníku::

   $ cat test_dict.py
   import os


   def test_dict(mocker):
       mocker.patch.dict("os.environ", {"FOO": "BAR"})

       assert os.environ["FOO"] == "BAR"

.. note::

   Místo cesty ke slovníku lze použít přímý objekt::

      $ test_dict_reference.py
      person = {}


      def test_dict_reference(mocker):
          mocker.patch.dict(person, name="Davie", age=23)

          assert person["name"] == "Davie"
          assert person["age"] == 23
          assert "status" not in person

.. tip::

   Klíče lze nahrazovat i v objektech, které se chovají jako slovník díky
   magickým metodám jako ``__getitem``, ``__setitem__`` aj.

mocker.patch.object
-------------------

Nahraď proměnnou na třídě::

   $ cat test_class_variable.py
   class Foo(object):
       x = 0
       y = 1


   def test_class_variable(mocker):
       mock_x = mocker.patch.object(Foo, "x", 1)
       mock_y = mocker.patch.object(Foo, "y", mocker.PropertyMock(return_value=0))

       assert Foo.x == 1
       assert Foo.y == 0

       assert isinstance(mock_x, int)
       assert isinstance(mock_y, mocker.PropertyMock)

Nahraď property atribut na třídě::

   $ cat test_class_property.py
   class Foo(object):
       @property
       def foo(self):
           return "foo"

       @property
       def bar(self):
           return "bar"


   def test_foo(mocker):
       mocker.patch.object(Foo, "foo", mocker.PropertyMock(return_value="bar"))
       mocker.patch.object(Foo, "bar", "foo")

       assert Foo.foo == "bar"
       assert Foo.bar == "foo"

Nahraď metodu na třídě::

   $ cat test_class_method.py
   class Foo(object):

       def foo(self):
           return "foo"

       def bar(self):
           return "bar"


   def test_foo(mocker):
       mocker.patch.object(Foo, "foo", return_value="bar")
       mocker.patch.object(Foo, "bar", lambda self: "foo")

       assert Foo().foo() == "bar"
       assert Foo().bar() == "foo"

.. note::

   Stejně jako u ``mocker.patch`` varianty, musí být nahrazované atributy
   a metody viditelné pri introspekci třídy pomocí zabudované ``dir`` funkce,
   tudíž instanční atributy lze upravit jen změnou ``__init__`` metody.

   Jakákoliv snaha mockovat objekty, které vůbec neexistují v daném modulu
   nebo na dané třídě, skončí vyvoláním erroru ``AttributeError``.

.. tip::

   Při patchování funkcí, metod a atributů lze zadat argument ``spec`` s
   hodnotou ``True``, kdy se vezme automaticky specifikace daného objektu a
   nastaví se debuggovací atributy na mock objektech, které budou vidět
   v diffu při failujících testech::

      $ cat test_spec.py
      class Foo(object):
          x = 0

          def foo(self):
              return "foo"


      def test_dict(mocker):
          # Use PropertyMock instead of default MagicMock to create a mock object

          mock_x = mocker.patch("test_spec.Foo.x", new_callable=mocker.PropertyMock, return_value=0, spec=True)
          mock_foo = mocker.patch.object(Foo, "foo", spec=True)

          assert repr(mock_x).startswith("<PropertyMock name='x' spec='int'")
          assert repr(mock_foo).startswith("<MagicMock name='foo' spec='function'")

   Mimo dosah patche, např. při vlastním definovaní mocku mimo **kwargs
   argumenty, je třeba zádavat explicitně referenci na mockovaný objekt
   a uvádat vlastní jméno::

      $ cat test_special_spec.py
      class Foo(object):
          x = 0


      def test_dict(mocker):
          mock_x = mocker.patch("test_spec.Foo.x", mocker.PropertyMock(return_value=1, name="x", spec=Foo.x))

          assert repr(mock_x).startswith("<PropertyMock name='x' spec='int'")

   V případě mockovaní celých tříd je vhodnější použít alternativní argument
   ``spec_set``, který zabrání nastavovat atributy a metody, které vubec
   neexistují na specifikovaném objektu::

      $ cat test_spec_set.py
      import pytest


      class Foo(object):
          x = 0

          def foo(self):
              return "foo"


      def test_dict(mocker):
          mock_foo = mocker.Mock(spec_set=Foo)
          mock_foo.foo = mocker.Mock(return_value="bar")

          # or shortcut
          #
          # mock_foo.foo.return_value = "bar"

          mocker.patch("test_spec_set.Foo", return_value=mock_foo)

          assert Foo().foo() == "bar"

          with pytest.raises(AttributeError):
              mock_foo.bar = mocker.Mock(return_value="foo")
