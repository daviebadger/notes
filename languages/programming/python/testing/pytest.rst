========
 Pytest
========
---------------------
 Testovací framework
---------------------

:Author: Davie Badger
:Contact: davie.badger@gmail.com
:License: CC BY-SA 4.0

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Instalace
=========

::

   $ pip install --user pytest

Testování
=========

Tvorba a spuštění testů
-----------------------

Vytvoř a spusť konkrétní testovací soubor::

   $ ls
   add.py  test_add.py
   $ cat add.py
   def add(x, y):
       return x + y
   $ cat test_add.py
   from add import add


   def test_add_with_valid_arguments():
       assert add(1, 1) == 2


   def test_add_with_invalid_arguments():
       with pytest.raises(TypeError):
           assert add(1, "1") == "2"
   $ pytest test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test/, inifile:
   collected 2 items

   test_add.py ..                                                  [100%]

   ======================= 2 passed in 0.01 seconds ========================

Spusť konkrétní test z testovacího souboru::

   $ pytest test_add.py::test_add_with_valid_arguments
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test/, inifile:
   collected 1 item

   test_add.py .                                                   [100%]

   ======================= 1 passed in 0.01 seconds ========================

Spusť všechny testy v daném adresáři::

   $ pytest
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test/, inifile:
   collected 2 items

   test_add.py ..                                                  [100%]

   ======================= 2 passed in 0.01 seconds ========================
   $ pytest .
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test/, inifile:
   collected 2 items

   test_add.py ..                                                  [100%]

   ======================= 2 passed in 0.01 seconds ========================

Spusť znova všechny nefunkční testy z minulého běhu::

   $ cat test_add.py
   from add import add


   def test_add():
       assert add(1, 1) == 2


   def test_another_add():
       assert add(0, "0") == 0
   $ pytest
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 2 items

   test_add.py .F                                                    [100%]

   =============================== FAILURES ================================
   ___________________________ test_another_add ____________________________

       def test_another_add():
   >       assert add(0, "0") == 0

   test_add.py:9:
   _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _

   x = 0, y = '0'

       def add(x, y):
   >       return x + y
   E       TypeError: unsupported operand type(s) for +: 'int' and 'str'

   add.py:2: TypeError
   ================== 1 failed, 1 passed in 0.04 seconds ===================
   $ cat test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 2 items
   run-last-failure: rerun previous 1 failure

   test_add.py .                                                     [100%]

   ========================== 1 tests deselected ===========================
   ================ 1 passed, 1 deselected in 0.02 seconds =================

.. note::

   Jako testovací soubory jsou považovany ty soubory, který mají název
   ``test_*.py`` nebo ``*_test.py``. Zpravidla se používá první varianta.
   Tyto testy se pak většinou nacházejí v separátním adresáři ``tests``::

      docs/
      project/
        __init__.py
        add.py
      tests/
        test_add.py
      setup.py

   Aby byly testy v separátní adresáři funkční, musí být projekt ``project``
   nainstalován pomocí ``setup.py`` souboru nebo bez lokální instalace projektu
   lze testy spouštět skrze Python interpreter::

      $ ls
      docs  projects  setup.py  tests
      $ python3 -m pytest

   Výhoda interpreteru spočívá v přidání aktuálního pracovního adresáře do
   ``sys.path``, aby bylo možné naimportovat projekt v testech.

.. tip::

   V rámci adresáře ``tests`` je možné ještě testy dále třídit podle jejich
   typů, např::

      tests/
        functional/
        integration/
        performance/
        system/
        unit/
          test_add.py

Fixtury
-------

Vlastní fixtury
^^^^^^^^^^^^^^^

Vytvoř a použij fixturu, která spustí kód před testem::

   $ cat test_add.py
   import pytest

   from add import add


   @pytest.fixture
   def echo():
       print("before", end="")


   @pytest.mark.usefixtures("echo")  # usefixtures accept multiple string args
   def test_add():
       assert add(1, 1) == 2
   $ pytest -s test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_add.py before.

   ======================= 1 passed in 0.01 seconds ========================

Vytvoř a použij fixturu, jejíž návratovou hodnotu lze dále použít v testech::

   $ cat test_add.py
   import pytest

   from add import add


   @pytest.fixture
   def echo():
       print("before", end="")
       return "value"


   def test_add(echo):
       assert add(1, 1) == 2
       assert echo == "value"
   $ pytest -s test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_add.py before.

   ======================= 1 passed in 0.01 seconds ========================

Vytvoř a použij fixturu, která poskytne hodnotu pro test a po testu spustí
dodatečný kód::

   $ cat test_add.py
   import pytest

   from add import add


   @pytest.fixture
   def echo():
       print("before", end="")
       yield "value"
       print("after", end="")


   def test_add(echo):
       assert add(1, 1) == 2
       assert echo == "value"
   $ pytest -s test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_add.py before.after

   ======================= 1 passed in 0.01 seconds ========================

Vytvoř a použij fixturu, která spustí kód před a po testu bez poskytnutí
hodnoty::

   $ cat test_add.py
   import pytest

   from add import add


   @pytest.fixture
   def echo():
       print("before", end="")
       yield
       print("after", end="")


   @pytest.mark.usefixtures("echo")
   def test_add():
       assert add(1, 1) == 2
   $ pytest -s test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_add.py before.after

   ======================= 1 passed in 0.01 seconds ========================

.. note::

   Díky volbě ``-s`` lze vidět standardní výstup i při testech, které jsou
   funkční. Defaultně lze vidět stdout jen při nefunkčních testech::

      $ cat test_add.py
      import pytest

      from add import add


      @pytest.fixture
      def echo():
          print("before", end="")


      @pytest.mark.usefixtures("echo")
      def test_add():
          assert add(1, 1) == 3
      $ pytest test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 1 item

      test_add.py F                                                    [100%]

      ============================== FAILURES ===============================
      ______________________________ test_add _______________________________

          @pytest.mark.usefixtures("echo")
          def test_add():
      >       assert add(1, 1) == 3
      E       assert 2 == 3
      E        +  where 2 = add(1, 1)

      test_add.py:13: AssertionError
      ------------------------ Captured stdout setup ------------------------
      before
      ====================== 1 failed in 0.03 seconds =======================

.. tip::

   Fixtury lze centralizovat do speciálního souboru ``conftest.py``, který
   se nachází v kořeni ``tests`` adresáře nebo taky ve vnořených adresářích,
   kde májí přednost před centrálním conftestem::

      $ cat conftest.py
      import pytest


      @pytest.fixture()
      def echo():
          print("before", end="")
          yield
          print("after", end="")

   Fixtury lze zavolat explicitně pomocí ``pytest.mark.usefixtures`` dekorátoru
   nebo uvedením fixtury jako parametr ve funkci. Alternativně lze spustit
   fixtury automaticky pomocí ``autouse`` argumentu::

      $ cat conftest.py
      import pytest


      @pytest.fixture(autouse=True)  # default scope is function
      def echo_function():
          """
          Before and after each test functions or class methods
          """
          print(" before-function ", end="")
          yield
          print(" after-function ", end="")


      @pytest.fixture(scope="class", autouse=True)
      def echo_class():
          """
          Before and after each test class even if it does not exist in module (bug?)
          """
          print(" before-class ", end="")
          yield
          print(" after-class ", end="")


      @pytest.fixture(scope="module", autouse=True)
      def echo_module():
          """
          Before and after each test module
          """
          print(" before-module ", end="")
          yield
          print(" after-module ", end="")


      @pytest.fixture(scope="session", autouse=True)
      def echo_session():
          """
          Before and after each test session
          """
          print("before-session ", end="")
          yield
          print(" after-session", end="")
      $ cat test_add.py
      from add import add


      def test_add():
          assert add(1, 1) == 2
      $ cat test_another_add.py
      from add import add


      def test_another_add():
          assert add(0, 0) == 0
      $ pytest -sv
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0 -- /usr/bin/python3
      cachedir: .pytest_cache
      rootdir: /home/davie/test, inifile:
      collected 2 items

      test_add.py::test_add before-session  before-module  before-class  before-function PASSED after-function  after-class  after-module
      test_another_add.py::test_another_add  before-module  before-class  before-function PASSED after-function  after-class  after-module  after-session

      ====================== 2 passed in 0.02 seconds =======================

   V neposlední řádě lze explitně nastavit na úrovni testovacího souboru,
   jaké fixtury se mají automaticky použít::

      $ cat conftest.py
      import pytest


      @pytest.fixture()
      def echo_function():
          """
          Before and after each test functions or class methods
          """
          print(" before-function ", end="")
          yield
          print(" after-function ", end="")


      @pytest.fixture(scope="module")
      def echo_module():
          """
          Before and after each test module
          """
          print(" before-module ", end="")
          yield
          print(" after-module", end="")
      $ cat test_add.py
      import pytest

      from add import add

      pytestmark = pytest.mark.usefixtures("echo_module", "echo_function")


      def test_add():
          assert add(1, 1) == 2
      $ pytest -sv test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0 -- /usr/bin/python3
      cachedir: .pytest_cache
      rootdir: /home/davie/test, inifile:
      collected 1 item

      test_add.py::test_add  before-module  before-function PASSED after-function  after-module

      ====================== 1 passed in 0.01 seconds =======================

   Volba ``-v`` zobrazí ukecanější výsledky pytestu.

Odbočka ke klasickému setupu a teardownu
""""""""""""""""""""""""""""""""""""""""

Spusť kód před a po testech klasickým způsobem, avšak s možností posílat
hodnoty dovnitř testů jen uvnitř tříd::

   $ cat test_add.py
   from add import add


   def setup_module(module):  # module parameter is not required
       print("before-module ", end="")


   def teardown_module(module):
       print(" after-module", end="")


   def setup_function(function):  # function parameter is not required
       print(" before-function ", end="")


   def teardown_function(function):
       print(" after-function ", end="")


   class TestAdd(object):
       @classmethod
       def setup_class(cls):
           print(" before-class ", end="")

           cls.value = "echo"

       @classmethod
       def teardown_class(cls):
           print(" after-class", end="")

       def setup_method(self):
           print(" before-method ", end="")

       def teardown_method(self):
           print(" after-method ", end="")

       def test_add(self):
           assert add(0, 0) == 0


   def test_add():
       assert add(1, 1) == 2
   $ pytest -sv test_add.py
   ========================= test session starts =========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0 -- /usr/bin/python3
   cachedir: .pytest_cache
   rootdir: /home/davie/test, inifile:
   collected 2 items

   test_add.py::TestAdd::test_add before-module  before-class  before-method PASSED after-method  after-class
   test_add.py::test_add  before-function PASSED after-function  after-module

   ======================= 2 passed in 0.02 seconds ======================
   ========================== test session starts ==========================

.. note::

   Fixtury na rozdíl od klasického postupu mají výhodu ve znovupoužitelnosti
   napříč testy, možnosti posílat hodnoty dovnitř testů nebo tyto fixtury
   nakešovat. Nicméně obě možnosti lze dohromady kombinovat.

.. tip::

   Fixtury lze parametrizovat, pokud je třeba vytvořit různé objekty a ty pak
   posílat do testů::

      $ cat test_add.py
      import smtplib

      import pytest


      @pytest.fixture(scope="session",
                      params=["smtp.gmail.com", "smtp.office365.com"])
      def smtp(request):
          smtp = smtplib.SMTP(host=request.param, port=587, timeout=10)
          yield smtp
          smtp.close()


      def test_smtp(smtp):
          assert smtp.noop()[0] == 250
      $ pytest test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items

      test_smtp.py ..                                                 [100%]

      ====================== 2 passed in 5.38 seconds =======================

   Dané testy se budou volat tolikrát, kolik existuje parametrů pro danou
   fixturu. Vedle parametrizovaných fixtur lze parametrizovat i samotné testy.

Zabudované fixtury
^^^^^^^^^^^^^^^^^^

Zobraz seznam fixtur::

   $ pytest --fixtures
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 2 items
   cache
       Return a cache object that can persist state between testing sessions.

       cache.get(key, default)
       cache.set(key, value)

       Keys must be a ``/`` separated value, where the first part is usually the
       name of your plugin or application to avoid clashes with other cache users.

       Values can be any object handled by the json stdlib module.
   capsys
       Enable capturing of writes to sys.stdout/sys.stderr and make
       captured output available via ``capsys.readouterr()`` method calls
       which return a ``(out, err)`` tuple.  ``out`` and ``err`` will be ``text``
       objects.
   capsysbinary
       Enable capturing of writes to sys.stdout/sys.stderr and make
       captured output available via ``capsys.readouterr()`` method calls
       which return a ``(out, err)`` tuple.  ``out`` and ``err`` will be ``bytes``
       objects.
   capfd
       Enable capturing of writes to file descriptors 1 and 2 and make
       captured output available via ``capfd.readouterr()`` method calls
       which return a ``(out, err)`` tuple.  ``out`` and ``err`` will be ``text``
       objects.
   capfdbinary
       Enable capturing of write to file descriptors 1 and 2 and make
       captured output available via ``capfdbinary.readouterr`` method calls
       which return a ``(out, err)`` tuple.  ``out`` and ``err`` will be
       ``bytes`` objects.
   doctest_namespace
       Inject names into the doctest namespace.
   pytestconfig
       the pytest config object with access to command line opts.
   record_xml_property
       Add extra xml properties to the tag for the calling test.
       The fixture is callable with ``(name, value)``, with value being automatically
       xml-encoded.
   record_xml_attribute
       Add extra xml attributes to the tag for the calling test.
       The fixture is callable with ``(name, value)``, with value being automatically
       xml-encoded
   caplog
       Access and control log capturing.

       Captured logs are available through the following methods::

       + caplog.text()          -> string containing formatted log output
       + caplog.records()       -> list of logging.LogRecord instances
       + caplog.record_tuples() -> list of (logger_name, level, message) tuples
   monkeypatch
       The returned ``monkeypatch`` fixture provides these
       helper methods to modify objects, dictionaries or os.environ::

           monkeypatch.setattr(obj, name, value, raising=True)
           monkeypatch.delattr(obj, name, raising=True)
           monkeypatch.setitem(mapping, name, value)
           monkeypatch.delitem(obj, name, raising=True)
           monkeypatch.setenv(name, value, prepend=False)
           monkeypatch.delenv(name, value, raising=True)
           monkeypatch.syspath_prepend(path)
           monkeypatch.chdir(path)

       All modifications will be undone after the requesting
       test function or fixture has finished. The ``raising``
       parameter determines if a KeyError or AttributeError
       will be raised if the set/deletion operation has no target.
   recwarn
       Return a WarningsRecorder instance that provides these methods:

       + ``pop(category=None)``: return last warning matching the category.
       + ``clear()``: clear list of warnings

       See http://docs.python.org/library/warnings.html for information
       on warning categories.
   tmpdir_factory
       Return a TempdirFactory instance for the test session.
   tmpdir
       Return a temporary directory path object
       which is unique to each test function invocation,
       created as a sub directory of the base temporary
       directory.  The returned object is a `py.path.local`_
       path object.

   ===================== no tests ran in 0.02 seconds ======================

.. note::

   V seznamu se mohou objevit i fixtury z pluginů, pokud jsou nějaké
   nainstalované.

caplog
""""""

Otestuj zachycené logy::

   $ cat test_logs.py
   import logging

   logger = logging.getLogger()


   def log():
       logger.warning("log")


   def test_logs(caplog):
       log()

       for record in caplog.records:  # instances of logging.LogRecord class
           assert record.levelname == "WARNING"
           assert record.msg == "log"
   $ pytest test_logs.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_logs.py .                                                    [100%]

   ======================= 1 passed in 0.01 seconds ========================

.. note::

   Zachycovaný jsou logy s úrovní ``WARNING`` a výš, tudíž logy s úrovni
   ``INFO`` a ``DEBUG`` jsou ignorovaný, není-li nastaveno jinak::

      $ cat test_info_logs.py
      import logging

      logger = logging.getLogger()
      logger.setLevel(logging.INFO)


      def log():
          logger.info("log")


      def test_log_in_context_manager(caplog):
          with caplog.at_level(logging.INFO):  # or with logger="name"
              log()

              assert "log" in caplog.text


      def test_log_out_of_context_manager(caplog):
          caplog.set_level(logging.INFO)  # or with logger="name"

          log()

          assert "log" in caplog.text
      $ pytest test_info_logs.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items

      test_info_logs.py ..                                            [100%]

      ====================== 2 passed in 0.01 seconds =======================

capsys
""""""

Otestuj zachycené printy::

   $ cat test_echo.py
   def echo():
       print("echo")


   def test_echo(capsys):
       echo()

       captured = capsys.readouterr()  # .out for stdout and .err for stderr

       assert "echo" in captured.out
       assert "echo\n" == captured.out
   $ pytest test_echo.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_echo.py .                                                    [100%]

   ======================= 1 passed in 0.01 seconds ========================

monkeypatch
"""""""""""

Otestuj podvržení návratové hodnoty objekty::

   $ cat test_setattr.py
   import os


   def test_setattr(monkeypatch):
       monkeypatch.setattr(os, "getcwd", lambda: "/")

       # or in a short way
       #
       # monkeypatch.setattr("os.getcwd", lambda: "/")

       assert os.getcwd() == "/"
   $ pytest test_setattr.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_setattr.py .                                                 [100%]

   ======================= 1 passed in 0.01 seconds ========================

Otestuj podvržení klíče ve slovníku::

   $ cat test_setitem.py
   config = {
       "USER": "davie",
   }


   def test_setitem(monkeypatch):
       monkeypatch.setitem(config, "USER", "badger")

       assert config["USER"] == "badger"
   $ pytest test_setitem.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_setitem.py .                                                 [100%]

   ======================= 1 passed in 0.01 seconds ========================

Otestuj podvržení environmentální proměnné v shellu::

   $ echo $LANG
   en_US.UTF-8
   $ cat test_setenv.py
   import os


   def test_setenv(monkeypatch):
       lang = "cs_CZ.UTF-8"

       monkeypatch.setenv("LANG", lang)

       assert os.environ["LANG"] == lang
   $ pytest test_setenv.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_setenv.py .                                                  [100%]

   ======================= 1 passed in 0.01 seconds ========================

.. note::

   Fixtura ``monkeypatch`` nabízí i analogii k ``set`` metodám a to ``del``
   metody, které po podvržení vyvolájí výjimku, pokud je původní metoda v
   kódu použita, není-li nastaveno jinak::

      $ cat test_delattr.py
      import os


      def test_setattr(monkeypatch):
          # monkeypatch.delattr(os, "getcwd")
          #
          # or

          monkeypatch.delattr("os.getcwd")

          assert os.getcwd() == "/"
      $ pytest test_delattr.py
      ================================================= test session starts =================================================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 1 item

      test_delattr.py
      INTERNALERROR> Traceback (most recent call last):
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/main.py", line 107, in wrap_session
      INTERNALERROR>     session.exitstatus = doit(config, session) or 0
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/main.py", line 145, in _main
      INTERNALERROR>     config.hook.pytest_runtestloop(session=session)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 617, in __call__
      INTERNALERROR>     return self._hookexec(self, self._nonwrappers + self._wrappers, kwargs)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 222, in _hookexec
      INTERNALERROR>     return self._inner_hookexec(hook, methods, kwargs)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 216, in <lambda>
      INTERNALERROR>     firstresult=hook.spec_opts.get('firstresult'),
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 201, in _multicall
      INTERNALERROR>     return outcome.get_result()
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 76, in get_result
      INTERNALERROR>     raise ex[1].with_traceback(ex[2])
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 180, in _multicall
      INTERNALERROR>     res = hook_impl.function(*args)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/main.py", line 168, in pytest_runtestloop
      INTERNALERROR>     item.config.hook.pytest_runtest_protocol(item=item, nextitem=nextitem)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 617, in __call__
      INTERNALERROR>     return self._hookexec(self, self._nonwrappers + self._wrappers, kwargs)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 222, in _hookexec
      INTERNALERROR>     return self._inner_hookexec(hook, methods, kwargs)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 216, in <lambda>
      INTERNALERROR>     firstresult=hook.spec_opts.get('firstresult'),
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 201, in _multicall
      INTERNALERROR>     return outcome.get_result()
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 76, in get_result
      INTERNALERROR>     raise ex[1].with_traceback(ex[2])
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 180, in _multicall
      INTERNALERROR>     res = hook_impl.function(*args)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/runner.py", line 62, in pytest_runtest_protocol
      INTERNALERROR>     runtestprotocol(item, nextitem=nextitem)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/runner.py", line 79, in runtestprotocol
      INTERNALERROR>     reports.append(call_and_report(item, "call", log))
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/runner.py", line 160, in call_and_report
      INTERNALERROR>     report = hook.pytest_runtest_makereport(item=item, call=call)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 617, in __call__
      INTERNALERROR>     return self._hookexec(self, self._nonwrappers + self._wrappers, kwargs)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 222, in _hookexec
      INTERNALERROR>     return self._inner_hookexec(hook, methods, kwargs)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 216, in <lambda>
      INTERNALERROR>     firstresult=hook.spec_opts.get('firstresult'),
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 196, in _multicall
      INTERNALERROR>     gen.send(outcome)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/skipping.py", line 117, in pytest_runtest_makereport
      INTERNALERROR>     rep = outcome.get_result()
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 76, in get_result
      INTERNALERROR>     raise ex[1].with_traceback(ex[2])
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 180, in _multicall
      INTERNALERROR>     res = hook_impl.function(*args)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/runner.py", line 312, in pytest_runtest_makereport
      INTERNALERROR>     longrepr = item.repr_failure(excinfo)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/python.py", line 598, in repr_failure
      INTERNALERROR>     return self._repr_failure_py(excinfo, style=style)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/python.py", line 591, in _repr_failure_py
      INTERNALERROR>     style=style)
      INTERNALERROR>   File "/home/davie/.local/lib/python3.6/site-packages/_pytest/nodes.py", line 243, in _repr_failure_py
      INTERNALERROR>     os.getcwd()
      INTERNALERROR> AttributeError: module 'os' has no attribute 'getcwd'
      Traceback (most recent call last):
        File "/home/davie/.local/bin/pytest", line 11, in <module>
          sys.exit(main())
        File "/home/davie/.local/lib/python3.6/site-packages/_pytest/config.py", line 61, in main
          return config.hook.pytest_cmdline_main(config=config)
        File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 617, in __call__
          return self._hookexec(self, self._nonwrappers + self._wrappers, kwargs)
        File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 222, in _hookexec
          return self._inner_hookexec(hook, methods, kwargs)
        File "/home/davie/.local/lib/python3.6/site-packages/pluggy/__init__.py", line 216, in <lambda>
          firstresult=hook.spec_opts.get('firstresult'),
        File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 201, in _multicall
          return outcome.get_result()
        File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 76, in get_result
          raise ex[1].with_traceback(ex[2])
        File "/home/davie/.local/lib/python3.6/site-packages/pluggy/callers.py", line 180, in _multicall
          res = hook_impl.function(*args)
        File "/home/davie/.local/lib/python3.6/site-packages/_pytest/main.py", line 138, in pytest_cmdline_main
          return wrap_session(config, _main)
        File "/home/davie/.local/lib/python3.6/site-packages/_pytest/main.py", line 128, in wrap_session
          session.startdir.chdir()
        File "/home/davie/.local/lib/python3.6/site-packages/py/_path/local.py", line 568, in chdir
          old = self.__class__()
        File "/home/davie/.local/lib/python3.6/site-packages/py/_path/local.py", line 149, in __init__
          self.strpath = py.error.checked_call(os.getcwd)
      AttributeError: module 'os' has no attribute 'getcwd'

.. tip::

   Pro pokročilejší podvrhování objektů je vhodnější použít plugin
   ``pytest-mock``, který je vylepšenou abstrakcí nad zabudovaných modulem
   ``unittest.mock``.

recwarn
"""""""

Otestuj zachycené varování pomocí fixtury::

   $ cat test_warning.py
   import warnings


   def warn():
       warnings.warn("warn", UserWarning)


   def test_warn(recwarn):
       warn()

       assert len(recwarn) == 1

       for warning in recwarn:
           assert str(warning.message) == "warn"
           assert issubclass(warning.category, UserWarning)
   $ pytest test_warning.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_warning.py .                                                 [100%]

   ======================= 1 passed in 0.01 seconds ========================

Otestuj zachycené varování bez fixtury::

   $ cat test_warning.py
   import warnings

   import pytest


   def warn():
       warnings.warn("warn", UserWarning)


   def test_warn(recwarn):
       with pytest.warns(UserWarning) as warning:
           warn()

           assert str(warning[0].message) == "warn"
   $ pytest test_warning.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_warning.py .                                                 [100%]

   ======================= 1 passed in 0.01 seconds ========================

.. note::

   Várování ``DeprecationWarning`` a ``PendingDeprecationWarning`` nejsou
   zobrazeny v přehledu, neboť i Python samotný je defaultně nezobrazuje::

      $ cat add.py
      import warnings


      def add(x, y):
          warnings.warn("use rather '+' operator", DeprecationWarning)

          return x + y
      $ test_add.py
      import pytest

      from add import add


      def test_add():
          assert add(1, 1) == 2


      def test_add_warning():
          with pytest.warns(DeprecationWarning):
              add(1, 1)
      $ pytest test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items

      test_add.py ..                                                  [100%]

      ====================== 2 passed in 0.01 seconds =======================

   Zobraz všechny varování klasickou volbou ``-W``, kterou zná i Python
   interpret::

      $ pytest -W always test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items

      test_add.py ..                                                  [100%]

      ========================== warnings summary ===========================
      test_add.py::test_add
        /home/davie/test/add.py:5: DeprecationWarning: use rather '+' operator
          warnings.warn("use rather '+' operator", DeprecationWarning)

      -- Docs: http://doc.pytest.org/en/latest/warnings.html
      ================ 2 passed, 1 warnings in 0.01 seconds =================

   Zobraz všechny varování pomocí globální fixtury::

      $ cat conftest.py
      import warnings

      import pytest


      @pytest.fixture(scope="session", autouse=True)
      def inject_x():
          warnings.filterwarnings("always")
      $ pytest test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items

      test_add.py ..                                                  [100%]

      ========================== warnings summary ===========================
      test_add.py::test_add
        /home/davie/test/add.py:5: DeprecationWarning: use rather '+' operator
          warnings.warn("use rather '+' operator", DeprecationWarning)

      -- Docs: http://doc.pytest.org/en/latest/warnings.html
      ================ 2 passed, 1 warnings in 0.01 seconds =================

   Zobraz všechny varování pomocí lokálního dekorátoru::

      $ cat test_add.py
      import pytest

      from add import add


      @pytest.mark.filterwarnings("always")
      def test_add():
          assert add(1, 1) == 2


      def test_add_warning():
          with pytest.warns(DeprecationWarning):
              add(1, 1)
      $ pytest test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items

      test_add.py ..                                                  [100%]

      ========================== warnings summary ===========================
      test_add.py::test_add
        /home/davie/test/add.py:5: DeprecationWarning: use rather '+' operator
          warnings.warn("use rather '+' operator", DeprecationWarning)

      -- Docs: http://doc.pytest.org/en/latest/warnings.html
      ================ 2 passed, 1 warnings in 0.01 seconds =================

.. tip::

   Viditelné varování se vždy zobrazí na konci testu::

      $ cat add.py
      import warnings


      def add(x, y):
          warnings.warn("test")

          return x + y
      $ pytest test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 1 item

      test_add.py .                                                   [100%]

      ========================== warnings summary ===========================
      test_add.py::test_add
        /home/davie/test/add.py:5: UserWarning: test
          warnings.warn("test")

      -- Docs: http://doc.pytest.org/en/latest/warnings.html
      ================ 1 passed, 1 warnings in 0.01 seconds =================

   Toto chování lze vypnout::

      $ pytest -p no:warnings test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 1 item

      test_add.py .                                                   [100%]

      ======================= 1 passed in 0.01 seconds ======================

tmpdir
""""""

Otestuj soubory a adresáře v dočasném adresáři::

   $ cat test_tmpdir.py
   def test_tmpdir(tmpdir):
       tmpdir.mkdir("test")

       assert len(tmpdir.listdir()) == 1
   $ pytest test_tmpdir.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   test_tmpdir.py .                                                  [100%]

   ======================= 1 passed in 0.01 seconds ========================

.. note::

   Fixtura ``tmpdir`` je objekt z externího balíčku ``py``, konkrétně
   ``py.path.local``, viz https://py.readthedocs.io/en/latest/path.html. Jde
   o vylepšení API nad zabudovaným ``os.path`` objektem.

.. tip::

   Defaultně má každý test svůj vlastní dočasný adresář. Pokud je třeba
   napříč testy sdílet tentýž adresář, je třeba místo ``tmpdir`` použít
   ``tmp_factory`` fixturu::

      $ cat test_tmpdir_factory.py
      import pytest


      @pytest.fixture(scope="module", autouse=True)
      def testdir(tmpdir_factory):
          testdir = tmpdir_factory.mktemp("test")
          testdir.mkdir("one")
          testdir.mkdir("two")

          yield testdir


      def test_dir_one(testdir):
          assert [True for tdir in testdir.listdir() if tdir.basename.endswith("one")]


      def test_dir_two(testdir):
          assert [True for tdir in testdir.listdir() if tdir.basename.endswith("two")]
      $ pytest test_tmpdir_factory.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items

      test_tmpdir_factory.py ..                                       [100%]

      ====================== 2 passed in 0.01 seconds =======================

tmp_path
""""""""

Otestuj dočasný adresář pro každou testovací funkci::

   $ cat test_tmp_path.py
   from pathlib import Path

   def test_tmp_path(tmp_path):
       assert isinstance(tmp_path, Path)
       assert tmp_path.exists()
   $ pytest test_tmp_path.py
   =========================== test session starts ==========================
   platform linux -- Python 3.6.6, pytest-4.0.1, py-1.7.0, pluggy-0.8.0
   rootdir: /home/davie/gitlab/trainer, inifile:
   plugins: mock-1.10.0, cov-2.6.0
   collected 1 item

   test_tmp_path.py .                                                 [100%]

   ======================== 1 passed in 0.02 seconds ========================

.. note::

   Fixtura ``tmp_path`` na rozdíl od ``tmpdir`` fixtury vrací ``Path`` objekt
   ze zabudované knihovny ``Pathlib``.

.. tip::

   Stejně jako u ``tmpdir_factory`` fixtury, lze i pomocí ``tmp_path_factory``
   fixtury sdílet stejný dočasný adresář pro vícero testů.

Modifikace testů
----------------

Parametrizace
^^^^^^^^^^^^^

Spusť test N-krát s různýmy argumenty::

   $ cat test_add.py
   import pytest

   from add import add


   @pytest.mark.parametrize("number", [-1, 0, 1])
   def test_add(number):
       if number < 0:
           assert add(0, number) < 0
       elif number == 0:
           assert add(0, number) == 0
       else:
           assert add(0, number) > 0
   $ pytest -v test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0 -- /usr/bin/python3
   cachedir: .pytest_cache
   rootdir: /home/davie/test, inifile:
   collected 3 items

   test_add.py::test_add[-1] PASSED                                  [ 33%]
   test_add.py::test_add[0] PASSED                                   [ 66%]
   test_add.py::test_add[1] PASSED                                   [100%]

   ======================= 3 passed in 0.01 seconds ========================

Spusť test N-krát s vícero různými argumenty::

   $ cat test_add.py
   import pytest

   from add import add


   @pytest.mark.parametrize("x,y", [  # or also ["x", "y"]
       (0, 1),
       (1, 2),
       (2, 3),
   ])
   def test_add(x, y):
       assert add(x, y) == sum([x, y])
   $ pytest test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0 -- /usr/bin/python3
   cachedir: .pytest_cache
   rootdir: /home/davie/test, inifile:
   collected 3 items

   test_add.py::test_add[0-1] PASSED                                 [ 33%]
   test_add.py::test_add[1-2] PASSED                                 [ 66%]
   test_add.py::test_add[2-3] PASSED                                 [100%]

   ======================= 3 passed in 0.02 seconds ========================

.. note::

   Pomocí parametrizace lze přepsat hodnotu fixtury a tím i její celé chování::

      $ cat test_add.py
      import pytest

      from add import add


      def echo():
          print("before function ")
          yield "echo"
          print(" after function")


      @pytest.mark.parametrize("echo", ["no echo"])
      def test_add(echo):
          assert add(1, 1) == 2
          assert echo == "no echo"
      $ pytest -s test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 1 item

      test_add.py .

      ====================== 1 passed in 0.01 seconds =======================

   Alternativně lze chování fixtury změnit pomocí vytvoření stejnojmenné
   fixturu v souboru, která přepíše fixturu z lokálního či globálního
   conftestu.

.. tip::

   Při použítí vícero parametrizovaných dekorátorů dojde ke kombinaci těchto
   argumentů::

      $ cat test_add.py
      import pytest

      from add import add


      @pytest.mark.parametrize("x", [1, 2, 3])
      @pytest.mark.parametrize("y", [4, 5, 6])
      def test_add(x, y):
          assert add(x, y) == sum([x, y])
      $ test -v test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0 -- /usr/bin/python3
      cachedir: .pytest_cache
      rootdir: /home/davie/test, inifile:
      collected 9 items

      test_add.py::test_add[4-1] PASSED                               [ 11%]
      test_add.py::test_add[4-2] PASSED                               [ 22%]
      test_add.py::test_add[4-3] PASSED                               [ 33%]
      test_add.py::test_add[5-1] PASSED                               [ 44%]
      test_add.py::test_add[5-2] PASSED                               [ 55%]
      test_add.py::test_add[5-3] PASSED                               [ 66%]
      test_add.py::test_add[6-1] PASSED                               [ 77%]
      test_add.py::test_add[6-2] PASSED                               [ 88%]
      test_add.py::test_add[6-3] PASSED                               [100%]

      ====================== 9 passed in 0.03 seconds =======================

Přeskakování
^^^^^^^^^^^^

Přeskoč test bez udání důvodu::

   $ cat test_add.py
   import pytest

   from add import add


   def test_add():
       assert add(1, 1) == 2


   @pytest.mark.skip
   def test_another_add():
       assert add(0, 0) == 0
   $ pytest test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 2 items

   test_add.py .s                                                                                                  [100%]

   ================== 1 passed, 1 skipped in 0.01 seconds ==================

Přeskoč všechny testy v souboru::

   $ cat test_add.py
   import pytest

   from add import add


   pytestmark = pytest.mark.skip  # or [pytest.mark.skip]


   def test_add():
       assert add(1, 1) == 2


   def test_another_add():
       assert add(0, 0) == 0
   $ pytest test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 2 items

   test_add.py ss                                                                                                  [100%]

   ================== 2 passed, 2 skipped in 0.01 seconds ==================

Přeskoč test s udáním důvodu::

   $ cat test_add.py
   import pytest

   from add import add


   def test_add():
       assert add(1, 1) == 2


   @pytest.mark.skip(reason="bla bla bla")
   def test_another_add():
       assert add(0, 0) == 0
   $ pytest test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 2 items

   test_add.py .s                                                                                                  [100%]

   ================== 1 passed, 1 skipped in 0.01 seconds ==================

.. note::

   Pokud jsou testy nefunkční a je třeba je z nějakého důvodu dočasně
   ignorovat, je daleko lepší je explicitně přeskočit než je všechny nechat
   zakomentovat.

   Navíc pomocí volby ``-`` lze vidět podrobněji, proč jsou testy přeskočony,
   je-li udán důvod::

      $ cat test_add.py
      import pytest

      from add import add


      @pytest.mark.skip
      def test_add():
          assert add(1, 1) == 2


      @pytest.mark.skip(reason="bla bla bla")
      def test_another_add():
          assert add(0, 0) == 0
      $ pytest -r test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items

      test_add.py ss                                                                                                  [100%]
      ======================= short test summary info =======================
      SKIP [1] test_add.py:6: unconditional skip
      SKIP [1] test_add.py:12: bla bla bla

      ====================== 2 skipped in 0.02 seconds ======================

.. tip::

   Preskoč test jen v případě pravdivé podmínky::

      $ cat test_add.py
      import sys

      import pytest

      from add import add


      def test_add():
          assert add(1, 1) == 2


      @pytest.mark.skipif(sys.version_info < (3, 7),
                          reason="Requires Python >= 3.7.0")
      def test_another_add():
          assert add(0, 0) == 0
      $ pytest -r test_add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.4.2, py-1.5.2, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items

      test_add.py .s                                                                                                  [100%]
      ======================= short test summary info =======================
      SKIP [1] test_add.py:12: Requires Python >= 3.7.0
      PASSED test_add.py::test_add

      ================= 1 passed, 1 skipped in 0.02 seconds =================

   U podmíněného přeskakování nelze vynechat důvodový argument ``reason``.

Značkování
^^^^^^^^^^

Označ test vlastní značkou::

   $ cat test_add.py
   import pytest

   from add import add


   @pytest.mark.one
   def test_add():
       assert add(1, 1) == 2


   @pytest.mark.two
   def test_another_add():
       assert add(0, 0) == 0

.. note::

   Označkované testy lze vyselektovat, zda se mají spusti nebo ignorovat::

      $ pytest -m one
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items / 1 deselected

      test_add.py .                                                                                                   [100%]

      =============== 1 passed, 1 deselected in 0.01 seconds ================
      $ pytest -m 'not one'
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 2 items / 1 deselected

      test_add.py .                                                                                                   [100%]

      =============== 1 passed, 1 deselected in 0.01 seconds ================

.. tip::

   Značky je vhodné zaregistrovat do konfiguračního souboru, aby pak mohly
   být zobrazny v přehledy pomocí volby ``--marks``::

      $ cat setup.cfg
      [tool:pytest]
      markers =
          one: description of this tag
          two: description of this tag
      $ pytest --markers
      @pytest.mark.one: description of this tag

      @pytest.mark.two: description of this tag

      @pytest.mark.skip(reason=None): skip the given test function with an optional reason. Example: skip(reason="no way of currently testing this") skips the test.

      @pytest.mark.skipif(condition): skip the given test function if eval(condition) results in a True value.  Evaluation happens within the module global context. Example: skipif('sys.platform == "win32"') skips the test if we are on the win32 platform. see http://pytest.org/latest/skipping.html

      @pytest.mark.xfail(condition, reason=None, run=True, raises=None, strict=False): mark the test function as an expected failure if eval(condition) has a True value. Optionally specify a reason for better reporting and run=False if you don't even want to execute the test function. If only specific exception(s) are expected, you can list them in raises, and if the test fails in other ways, it will be reported as a true failure. See http://pytest.org/latest/skipping.html

      @pytest.mark.parametrize(argnames, argvalues): call a test function multiple times passing in different arguments in turn. argvalues generally needs to be a list of values if argnames specifies only one name or a list of tuples of values if argnames specifies multiple names. Example: @parametrize('arg1', [1,2]) would lead to two calls of the decorated test function, one with arg1=1 and another with arg1=2.see http://pytest.org/latest/parametrize.html for more info and examples.

      @pytest.mark.usefixtures(fixturename1, fixturename2, ...): mark tests as needing all of the specified fixtures. see http://pytest.org/latest/fixture.html#usefixtures

      @pytest.mark.tryfirst: mark a hook implementation function such that the plugin machinery will try to call it first/as early as possible.

      @pytest.mark.trylast: mark a hook implementation function such that the plugin machinery will try to call it last/as late as possible.

   Aby nedocházelo k překlepům v názvech značek, je vhodné ještě použít
   volbu ``--strict`` při spuštění testů::

      $ pytest --strict

Pluginy
=======

Nainstaluj a použij plugin ``pytest-cov`` pro zobrazení informace o pokrytí
kódu testy::

   $ pip install --user pytest-cov
   $ pytest --cov=.
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   plugins: cov-2.5.1
   collected 2 items

   test_add.py ..                                                    [100%]

   ----------- coverage: platform linux, python 3.6.3-final-0 -----------
   Name          Stmts   Miss  Cover
   ---------------------------------
   add.py            2      0   100%
   test_add.py       5      0   100%
   ---------------------------------
   TOTAL             7      0   100%


   ======================= 2 passed in 0.03 seconds ========================

.. note::

   Pluginy lze ignorovat při testech pomocí volby ``-p``::

      $ pytest -p no:cov --cov=.
      usage: pytest [options] [file_or_dir] [file_or_dir] [...]
      pytest: error: unrecognized arguments: --cov=.
        inifile: None
        rootdir: /home/davie/test
      $ pytest -p no:cov --cov=.

   Skrze volbu ``--trace--config`` lze vidět aktivované pluginy::

      $ pytest --trace-config | grep '^plugins:'
      plugins: cov-2.5.1

.. tip::

   Seznam pluginů lze najít na http://plugincompat.herokuapp.com/.

Konfigurace
===========

Konfigurační soubor
-------------------

Ulož volby příkazu do konfiguračního souboru ``setup.cfg``::

   $ cat setup.cfg
   [tool:pytest]
   addopts = -v
   $ pytest test_add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0 -- /usr/bin/python3
   cachedir: .pytest_cache
   rootdir: /home/davie/test, inifile: setup.cfg
   collected 2 items

   test_add.py::test_add PASSED                                      [ 50%]
   test_add.py::test_another_add PASSED                              [100%]

   ======================= 2 passed in 0.01 seconds ========================

.. note::

   Další konfigurační možnosti lze zobrazit v nápovědě pomocí ``--help`` volby
   v sekci ``ini-options``::

      $ pytest --help

   Např. v klíčí ``norecursedirs`` lze specifikovat adresáře, které se mají
   ignorovat nebo v klíčí ``testpaths`` nastavit adresáře, kde se mají hledat
   testy::

      $ cat setup.cfg
      [tool:pytest]
      norecursedirs = build dist
      testpaths = docs tests

.. tip::

   Pokud je použíta volba ``--lf`` pro spuštění posledních nepovedených testů,
   tak v případě žádných nepovedených testů se spustí všechny testy. Tomu lze
   zabránit pomocí volby ``--last-failed-no-failures none``::

      $ cat setup.cfg
      [tool:pytest]
      addopts = -v --last-failed-no-failures none
      $ pytest --lf
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0 -- /usr/bin/python3
      cachedir: .pytest_cache
      rootdir: /home/davie/test, inifile: setup.cfg
      collected 2 items / 2 deselected
      run-last-failure: run none (no recorded failures)

      ==================== 2 deselected in 0.01 seconds =====================

Integrace s doctesty
--------------------

Spusť v rámci testů i doctesty v dokumentačních řetězcích::

   $ cat add.py
   def add(x, y):
       """
       >>> add(1, 1)
       2
       """
       return x + y
   $ pytest add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 0 items

   ===================== no tests ran in 0.00 seconds ======================
   $ pytest --doctest-modules add.py
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   add.py .                                                          [100%]

   ======================= 1 passed in 0.01 seconds ========================

Spusť doctesty v textových souborech::

   $ cat add.rst
   >>> 1 + 1
   2

   .. code::

      >>> 2 + 2
      4
   $ pytest --doctest-modules --doctest-glob='*.rst' add.rst
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 1 item

   add.rst .                                                         [100%]

   ======================= 1 passed in 0.01 seconds ========================

.. note::

   Obsahuje-li docstring více příkladu, tak po prvním neúspěchu se další
   testy nespustí, pokud není nastaveno jinak::

      $  cat add.py
      def add(x, y):
          """
          Examples
          --------

          Addition with integers:

          >>> add(1, 1)
          3

          Addition with floats:

          >>> add(2.0, 2.0)
          5.0

          Addition with incompatible types:

          >>> add(3, "3")
          Traceback (most recent call last):
              ...
          TypeError: unsupported operand type(s) for +: 'int' and 'str'
          """
          return x + y
      $ pytest --doctest-modules add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 1 item

      add.py F                                                        [100%]

      ============================== FAILURES ===============================
      __________________________ [doctest] add.add __________________________
      002
      003     Examples
      004     --------
      005
      006     Addition with integers:
      007
      008     >>> add(1, 1)
      Expected:
          3
      Got:
          2

      /home/davie/test/add.py:8: DocTestFailure
      ====================== 1 failed in 0.01 seconds =======================
      $ pytest --doctest-modules add.py --doctest-continue-on-failure
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 1 item

      add.py F                                                        [100%]

      ============================== FAILURES ===============================
      __________________________ [doctest] add.add __________________________
      002
      003     Examples
      004     --------
      005
      006     Addition with integers:
      007
      008     >>> add(1, 1)
      Expected:
          3
      Got:
          2

      /home/davie/test/add.py:8: DocTestFailure
      004     --------
      005
      006     Addition with integers:
      007
      008     >>> add(1, 1)
      009     3
      010
      011     Addition with floats:
      012
      013     >>> add(2.0, 2.0)
      Expected:
          5.0
      Got:
          4.0

      /home/davie/test/add.py:13: DocTestFailure
      ====================== 1 failed in 0.01 seconds =======================

.. tip::

   Pomocí fixtur lze upravit jmenný prostor v doctestech::

      $ cat conftest.py
      import pytest


      @pytest.fixture(scope="session", autouse=True)
      def inject_x(doctest_namespace):
          doctest_namespace["x"] = 0
      $ cat add.py
      def add(x, y):
          """
          >>> assert x == 0
          >>> add(x, x)
          0
          """
          return x + y
      $ pytest --doctest-modules add.py
      ========================= test session starts =========================
      platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
      rootdir: /home/davie/test, inifile:
      collected 1 item

      add.py .                                                        [100%]

      ====================== 1 passed in 0.01 seconds =======================

Integrace se setup.py
---------------------

Přepiš zabudovaný spoušteč testů v ``setuptools`` projektu na ``pytest``::

   $ cat setup.py
   from setuptools import setup

   setup(
       name="add",
       version="0.1.0",
       py_modules=["add"],
       setup_requires=["pytest-runner"],
       tests_require=["pytest"],
   )
   $ cat setup.cfg
   [aliases]
   test = pytest
   $ python setup.py test
   running pytest
   Searching for pytest
   Best match: pytest 3.5.0
   Processing pytest-3.5.0-py3.6.egg

   Using /home/davie/test/.eggs/pytest-3.5.0-py3.6.egg
   running egg_info
   writing add.egg-info/PKG-INFO
   writing dependency_links to add.egg-info/dependency_links.txt
   writing top-level names to add.egg-info/top_level.txt
   reading manifest file 'add.egg-info/SOURCES.txt'
   writing manifest file 'add.egg-info/SOURCES.txt'
   running build_ext
   ========================== test session starts ==========================
   platform linux -- Python 3.6.3, pytest-3.5.0, py-1.5.3, pluggy-0.6.0
   rootdir: /home/davie/test, inifile:
   collected 2 items

   test_add.py ..                                                    [100%]

   ======================== 2 passed in 0.01 seconds =======================

.. note::

   Pokud chcí poslat pro ``test`` příkaz volby z ``pytest`` příkazu, je nutné
   je uvést ve volbě ``--adopts``::

      $ python3 setup.py test --addopts '-v'
