===================
 ComfortableMotion
===================
-------------------------------
 Příjemnější scrollování textu
-------------------------------

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

   Plug 'yuttie/comfortable-motion.vim'

Konfigurace
===========

::

   " Příjemnější scrollování i pro klávesy 'j' a 'k'

   let g:comfortable_motion_scroll_down_key = "j"
   let g:comfortable_motion_scroll_up_key = "k"

.. note::

   Skoky o půl stránky nebo celou stránku jsou automaticky upraveny na
   scrollování o určitém počtu řádku.
