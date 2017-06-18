=============
 Easy Motion
=============
------------------------------
 Snadnější pohyhování v textu
------------------------------

https://github.com/easymotion/vim-easymotion

.. contents:: Obsah:

.. sectnum::
   :depth: 3
   :suffix: .

Ovládání
========

* ``\\f`` + znak

  * najdi v textu další výskyty daného znaku a označ je písmeny, pomocí kterých
    lze na dané místo rovnou skočit::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.

       \\fo

       L{a}rem ipsum d{s}l{d} sit amet, e{g}s eu aperiri m{h}deratius.

* ``\\F`` + znak

  * najdi v textu předchozí výskyty daného znaku a označ je písmeny

* ``\\w`` (\W)

  * označ v textu začátky všech slov, na které lze skočit

* ``\\e`` (\E)

  * označ v textu konce všech slov, na které lze skočit

* ``\\b`` (\B)

  * označ v textu předchozí začátky všech slov, na které lze skočit

* ``\\ge`` (\gE)

  * označ v textu předchozí konce všech slov, na které lze skočit

* ``\\j``

  * označ v textu začátky dalších řádků včetně prázdných řádků a řádků s
    odsazením::

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur
       nostrud quaeque eu, an his hendrerit prodesset, nonumes oportere
       gloriatur qui ut.

       \\j

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur
       {a}ostrud quaeque eu, an his hendrerit prodesset, nonumes oportere
       {s}loriatur qui ut.

* ``\\k``

.. note::

   Označená oblast závísí na velikosti (výšce) okna.

Konfigurace
===========

::

   " aktivuj Easy Motion pří stisknutí \ namísto \\

   map <Leader> <Plug>(easymotion-prefix)
