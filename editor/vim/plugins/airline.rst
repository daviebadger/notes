=========
 Airline
=========
------------------------
 Přehledný status řádek
------------------------

https://github.com/vim-airline/vim-airline

Konfigurace
===========

::

   let g:airline_powerline_fonts=1             " aktivuj powerline ikonky
   let g:airline#extensions#tabline#enabled=1  " zpřehlédni buffery a záložky

   set laststatus=2                            " vždy zobraz Airline řádek

Pokud font v terminálu neobsahuje powerline ikonky, je třeba nainstalovat
font, který je v sobě má, viz::

   https://github.com/powerline/fonts

Poté je třeba daný font nastavit v nastavení terminálu.
