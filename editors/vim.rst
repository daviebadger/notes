=====
 Vim
=====
---------------------------------------
 Textový editor zabudovaný v terminálu
---------------------------------------

:Abstract:

   Vi IMproved, zkráceně `Vim`_, vznikl v roce 1991 klonem původního `Vi`_
   editoru určeného pro operační systém Unix. Vytvořil ho Bram Moonlenaar.

   Vim je zdarma a lze ho spustit na jakémkoliv operačním systému (pokud je
   nainstalovaný). Jeho zdrojové kódy lze najít na `GitHubu`_. Poslední
   hlavní verze je č. 8 (od října 2016).

   Oficiální dokumentaci lze najít:

   1. uvnitř Vimu spuštěním příkazu pro nápovědu v normal módu::

      :help

   2. online na stránce http://vimhelp.appspot.com/

   Kromě toho má Vim i oficiální interaktivní tutoriál v terminálu, ve kterém
   se lze prakticky naučit ovládat základy Vimu během 25 - 30 minut. Tento
   tutoriál se spouští pomocí::

      $ vimtutor

   Na závěr doporučuji i přehledný `Vim tahák`_ (v angličtině).

.. contents:: Obsah

Instalace
=========

Defaultně v Ubuntu je už Vim nainstalovaný, avšak ve své omezené podobě kvůli
kompatibilitě s původním Vi editorem. Spouští se příkazem::

   $ vi

Jestliže však chci používat Vim se všemi možnostmi, které nabízí, tak jej
musím nainstalovat pomocí::

   $ sudo apt install vim

Základní ovládání
=================

Spuštění a ukončení
-------------------

Editor Vim se spuští svým stejnojmenným příkazem::

   $ vim

Bez uvedení cesty k nějakému souboru se otevře prázdný editor s výchozím
textem o Vimu (jeho aktuální verze, jméno autora atd.). Pro "zavření" Vimu
(respektive okna, ve kterém se nacházím) se nápíše uvnitř editoru příkaz::

   :q

.. note::

   Jestliže jste nechtěně vstoupili do "Insert" módu (začali jste psát text),
   tak je třeba zmáčknout klávescu ESC (vypne "Insert" mód) a příkaz pro
   násilné ukončení Vimu bez uložení textu do souboru::

      :q!

Když pro příkaz "vim" uvedu ještě cestu k souboru, tak zde záleží, zdá se
jedná o:

a) existující soubor

   * zobrazí se jeho obsah
   * např.::

        $ vim ~/.profile

b) neexistující soubor

   * otevře se opět prázdný editor, ale pokud se změní jeho obsah (přibude
     nějaký text) a ten se uloží, tak již není třeba uvádět jméno souboru.

Soubor lze samozřejme ještě otevřít uvnitř Vimu a to příkazem::

   :o název_souboru

Tento postup platí jen pro lokální a vnořené soubory. Pro otevření souboru
někde v jiném nadřazeném adresáři, kde je třeba použít absolutní cestu se
použíje příkaz::

   :e /cesta/k/souboru

Módy
----

Aby Vim věděl, kdy chce uživatel editovat / navigovat se v textu, tak jsou
zavedené tzv. módy. Pro začátek postačí znát tyto tři základní:

1. Normal

   * výchozí stav po spuštení Vimu, který slouží pro navigaci v textu a jeho
     editaci pomoci
   * některé písmenka (znaky) a klávesové zkratky jsou vyhrazena pro
     jednotlivé úkony, např. pohyb kurzoru doprava o 1 znak
   * při přepnutí z jiného módu na Normal se použije klávesa ESC

2. Insert

   * mód, ve kterém přestanou fungovat speciální písmena (znaky), ty se
     budou nyní zapisovat do textu
   * spustí se z Normal módu stisknutím písmenka "i" (v levém dolním rohu
     bude vidět tučným písmem "-- INSERT --")
   * do Insert módu lze vstupovat i jinými písmenkami, ale o tom až v
     kapitole `Další vstupy do Insert módu`_

3. Command-line

   * pro ovládání Vimu jako takového pomocí příkazů jako je např. otevírání a
     zavírání souborů nebo jeho nastavení (přízpůsobení)
   * zapíná se převážně stiskem ":", za který následuje název daného příkazu
   * tento mód se pozná tak, že se dole ve Vimu objeví příkazový řádek
   * pokud si nejsem jistý, jestli píšu příkaz správně, mohu stisknout
     klávesovou zkratku CTRL + d, která mi ukáže všechny možné možnosti
   * klávesa TAB slouží klasicky pro automatické doplnění příkazů

Ukládání do souboru
-------------------

Jestliže došlo k požadované změně obsahu a tu chci uložit, tak se přepnu z
Insert do Normal a spustím::

   :w

Pokud jsem otevřel prázdný Vim (bez uvedení cesty k souboru), tak musím uvést,
kam chci obsah uložit::

   :w ~/Documents/test.txt

Pro uložení obsahu existujícího souboru do jiného souboru (uložit jako) je
příkaz::

   :sav /cesta/k/souboru

Když chci uložit a dál nepokračovat v práci (zavřít Vim)::

   :wq

Pohyb kurzoru
-------------

Aby bylo na čem procvičovat, je dobré mít nějaký pracovní text.

1. zkopírujte text níže (tři odstavce latinského textu)
2. otevřete si prázdný Vim
3. změnte mód na Insert
4. vložte do Vimu pomocí kombinace kláves CTRL + SHIFT + v
5. vratťe se zpět do Normal módu
6. v případě potřeby uložte pro budoucí použití

Lorem ipsum dolor sit amet, eos eu aperiri moderatius. Eam utamur nostrud
quaeque eu, an his hendrerit prodesset, nonumes oportere gloriatur qui
ut. Cu malis summo saperet nec, eam ei purto fastidii sententiae. Graece
detracto reformidans ex mel. At oportere moderatius ius, sea at scripta
regione dissentiunt.

Vel no ferri aeterno deleniti. Ne eam nisl dissentiunt comprehensam, ea
accusata vulputate mea. Ne duo assum meliore tincidunt, ius option
molestiae et. Magna porro lucilius ea mea. Tota malorum ut vis, vim id
posse civibus praesent.

Quot cibo eloquentiam eum id, tation mentitum consectetuer pri ad. Ei mel
exerci explicari, equidem aliquando nec et, an sed assum hendrerit. Id
vel modus philosophia. Ea quo dicant minimum, choro scaevola ex mel. Tale
vide nostrum ei usu, his illum scriptorem te. Ex legere cotidieque pro,
quo nisl dolor assentior an, et iriure scripta blandit per.

Základní pohyb po znacích
^^^^^^^^^^^^^^^^^^^^^^^^^

Klasický pohyb kurzoru doleva, dolu, nahoru, doprava tvoří písmenka::

         ^
         k
   < h       l >
         j
         v

.. note::

   Samozřejmě lze použít i šipky (pokud fungují), nicméně se tím ztrácí
   výhoda mít umístěnou pravou ruku ve výchozi poloze pro psaní všemi deseti
   (ukazováček je na pozici písmenka "j").

Klávesy h / j / k / l jde samožejmě podržet, kdy dojde k opakování jejich
stisku. Pokud však vím, o kolik se chci posunout na jiné misto, můžů před
jejich stiskem uvést číslo. Např. pohyb o 10 řádku dolu::

   10j

Skákání na konkrétní znak na řádku
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pokud chci skočit na konkrétní znak místo počítání počtu znaků doleva či
doprava, stisknu následující písmenka:

1. f + znak

   * hledá vpravo od kurzoru po konec řádku výskyt daného znaku
   * příklad::

        # Mějme následující řádek:

        Lorem ipum dolor sit amet, eos eu aperiri moderatius. Eam

        # Chci skočit na začátek další věty, tak stisknu

        fE

        # a kurzor skutečně skočí na onen začátek, neboť jinde velké písmeno E
        # není.

   * jestliže se daný znak vyskutuje vícekrát na řádku, tak mohu skočit až na
     Ntý výskut pomocí::

        2fe

2. F + znak

   * to samé jako malé "f", akorát hledá nalevo po začátek řádku

Skákání na konkrétní sloupec
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sloupcem se myslí pořadí (místo) znaků na řádku.

* |

  * skočí na první sloupec (znak) na řádku

* 80|

  * skočí na 80. sloupec (znak) na řádku
  * platí jen pro takové řádky, které jsou takhle dlouhé. Když bude řádek
    obsahovat méně znaků než 80, tak kurzor skočí na ten poslední znak

Skákání po slovech
^^^^^^^^^^^^^^^^^^

Pohyb mezi slovy zajišťují tyto písmenka:

* w

  * skočí na začátek dalšího slova (může jej tvořit i číslo), ale i
    interpunkčního znaménka
  * příklad::

       # Mějme následující větu:

       Lorem ipsum dolor sit amet, eos eu aperiri moderatius.

       # Pokud bychom skákali od začátku věty pomocí písmenka "w" a aktuálně
       # by se kurzor nacházel na začátku slova "amet":

       Lorem ipsum dolor sit |a|met, eos eu aperiri moderatius.

       # Tak při dalším skoku kurzor neskočí na začátek slova "eos", ale na
       # čárku:

       Lorem ipsum dolor sit amet|,| eos eu aperiri moderatius.

  * pro ignorování interpunkčních znamének je třeba stisknout velké "W"

* e

  * skočí na konec aktuální slova (pokud se kurzor nachází kdekoliv od
    prvního po předposlední znak slova) nebo konec dalšího slova
  * taky respektuje interpunkční znaménka, pro jejich ignoraci je třeba
    stisk "E"

* ge

  * skočí na začátek předchozí slova (opak "e")
  * pro ignoraci interpunkčních znamének se stiskne "gE"

* b

  * skočí na začátek aktuálního nebo předchozího slova (opak "w")
  * pro ignoranci interpunkčních znamének se stiskne "B"

Stejně jako u znacích mohu skákat po více slovech, např. o tři slova dopředu::

   3w

Skákání na konkrétní slova
^^^^^^^^^^^^^^^^^^^^^^^^^^

Pokud je kurzor v místě nějakého slova a já hledám zrovna další / předchozí
výskyt tohoto slova, tak mohu stisknout tyto znaky:

* \*

  * skočí dopředu na další výskyt slova (pokud je v souboru)

* #

  * skočí dozadu na předchozí výskyt slova

Když nemám v daném slově kurzor, mohu si vypomoct příkazy (Command-line mód),
které jsou spíše typické při vyhledávání slov(a) v textu:

* /pattern

  * hledá výskyt daného patternu napravo od kurzoru až po poslední řádek v
    souboru
  * pokud se pattern najde, tak je třeba stisknout ENTER, aby se na něho
    přemístil kurzor
  * kdyby se na stejném řádku vyskytoval daný vzor vícekrát, tak na další
    pozici patternu skáče stisknutím písmene "n" po ESC
  * na předchozí výskyt se místo malého "n" bude klikat velké "N"

* ?pattern

  * zde naopak se bude hledat pattern nalevo od kurzoru až po začátek
    souboru
  * lze taktéž použít "n" a "N" pro skákání na předchozí / další výskytu

Oba způsoby jsou defaultně citlivé na rozdíl velkých a malých písmen. Pro
dočasné vypnutí tohoto chování lze na konec napsat suffix "\c"::

   /pattern\c
   ?pattern\c

.. tip::

   Pro náročnější uživatele by se mohly hodit i regulární výrazy, více o nich
   `ZDE <http://vimhelp.appspot.com/pattern.txt.html>` dole ve 4. sekci o
   patternech.

Skákání na kraje řádku
^^^^^^^^^^^^^^^^^^^^^^

* 0 (nula)

  * na začátek řádku

* $

  * na konec řádku

Jestliže řádek začíná odsazením a já nechci skočit do tohoto prázdného
prostoru, ale na první slovo, tak zmáčknu "^".

Skákání na konkrétní řádky
^^^^^^^^^^^^^^^^^^^^^^^^^^

* gg (nebo 1G)

  * na začátek souboru (první řádek)

* 3G

  * na 3. řádek v souboru

* G

  * na konec souboru (poslední řádek)

.. note::

   Kurzor po skoku bude vždy na začátku řádku, i když jsem ho předtím měl
   třeba někde uprostřed řádku.

Skákání na začátky a konce závorek
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pokud jsem uvnitř libovolné závorky (kulatá, složená, hranatá), tak znakem "%"
mohu skočit na pozici otevřené / zavřené závorky. První skok je vždy na tu
otevírající.

Skákání po větách a odstavcích
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* )

  * na začátek další věty
  * příklad::

       # Mějme text:

       Toto je věta A. Toto je věta B.

       # a kurzor na začátku řádku. Stiskem ")" se kurzor přesune na znak "T"
       # v druhé větě:

       Toto je věta A. |T|oto je věta B.

* (

  * na začátek předchozí věty

* }

  * na další odstavec (taktéž blok kódu)

* {

  * na předchozí odstavec

Skákání na kraje a doprostřed obrazovky
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* L

  * škočí na poslední řádek, který vidím v okně terminálu

* H

  * skočí na první řádek, který vidím v okně

* M

  * škočí doprostřed obrazovky

Skákání po stránkách
^^^^^^^^^^^^^^^^^^^^

Abych nemusel skákat po X řádcích, ale rovnou podle velikosti okna terminálu.

* CTRL + f

  * skočí na další "okno" (přesně o tolik řádků, kolik vidím celkem v
    terminálu)

* CTRL + b

  * na předchozí okno

Pro poloviční velikost to pak je:

* CTRL + d

  * o půlku okna dolu

* CTRL + u

  * o půlku okna nahoru

Další vstupy do Insert módu
---------------------------

Teď, když umíme se pohybovat v textu, je dobré vědět o dalších možnostech,
jak si usnadnit vstup do Insert módu (kromě klasického "i"):

* a

  * na rozdíl od "i" nezačně Insert mód v místě, kde je kurzor, ale o
    jeden znak napravo
  * rozdíl bude patrný z následujícího příkladu::

       # Mějme v editoru pouze text "Vim", ke kterému chci dopsat text
       # " je super."

       Vim

       # Navigujeme kurzorem na konec řádku. Pokud bychom do Insert módu
       # vstoupili pomocí "i" a začali psát dovětek, vypadalo by to takhle:

       Vi je super.m

       # Naopak při stisku "a" se kurzor posune o jeden znak doprava za
       # písmenko "m" (vznikne mezera, která zanikne po stisku ESC,
       # jestliže nic nenapíšeme), pak lze v pořádku dopsat zbytek:

       Vim je super.

* A

  * kurzor skočí na konec řádku a interně stiskne "a", abychom mohli
    pokračovat v psaní nové věty či odentrovat na jiný řádek

* I

  * relativně opak stisku "A", kdy se kurzor přemístí na úplný začátek
    souboru

.. tip::

   Když před zmáčknutím "a" / "A" / "i" / "I" stisknu ještě nějaké číslo,
   tak to, co napíšu v Insert módu se tolikrát vloží do textu, když se vrátím
   zpět do Normal módu.

   Např. chci třikrát vložit písmenko "X"::

      3iX + ESC

Pokud chci při vstupu rovnou vložit i prázdný řádek, tak mám na výběr, zda
ho chci vložit:

a) o řádek výše, než je kurzor

   * stisknu "O" (velké o)
   * příklad::

        # Mám kurzor na prvním řádku souboru, který obsahuje větu:

        |U|čím se Vim.

        # Pokud stisknu "O", tak se celá věta posune na druhý řádek a první
        # řádek bude prázdný, kam se přesune i kurzor a mód bude klasiky
        # Insert.

        | |
        Učím se Vim.

b) o řádek níž

   * stisknu "o" (malé o), opak k předchozí variantě

Editace textu
=============

Občas se může stát, že provedete nějakou akci, které lituje a chtěli byste se
vrátít v čase zpátky nebo naopak vrátit z minulosti dopředu:

* u

  * odstraní poslední akci (může se jednat o příkaz či vložený text)
  * lze několikrát stisknout za sebou (přesne o tolik stisknutí se vrátí
    do minulosti)

* CTRL + r

  * vrátí se o jednu akci z minulosti dopředu (taktéž lze opakovat)

Co se týče jednotlivých editačních akcí (mazání, kopírování aj.) uvedených
níže v textu, tak ve většině případů lze skloubit speciální znaky pro danou
akci spolu s čísly a pohybovými znaky.

Syntaxe tedy bude vypadat následovně:

1. speciální_znak
2. číslo + speciální_znak
3. speciální_znak + pohybový_znak
4. speciální_znak + číslo + pohybový_znak

.. tip::

   Kdyby se náhodou stálo, že potřebuji několikrát zopakovat předchozí
   událost, tak stačí tolikrát stisknout ".". Např. místo trojíte stisku
   "u" mohu taktéž třikrát stisknout tečku.

Mazání textu
------------

Lze samozřejmě použít klasické klávesy pro mazání (backspace a delete), ale
je to zdlouhavý proces, pokud potřebuji mazat např. více znaků / slov / řádku
najednou.

Při použítí následujícíh způsobu mazání je třeba být klasicky v Normal módu.

Mazání po znacích
^^^^^^^^^^^^^^^^^

* x

  * smaže znak, který se nachází v místě kurzoru
  * když uvedu i číslo, tak smažu X znaků doprava::

       5x

Pro mazání více znaků doleva mimo klasické způsoby lze následovně::

   3dj

Toto smaže od aktuálního kurzoru 3 znaky nalevo. Pro smazání všech znaků až
na začátek / konec řádku to bude::

   d0
   d$

.. tip::

   Bylo by dobré vědět do budoucna, že písmenko "d" nejenom, že maže určitý
   úsek textu, ale taky tuto smaznou část si ještě zapamatuje. Toto se bude
   hodit do situaci, kdy je třeba vystřihnout text a přemístit ho jinam.

Mazání po slovech
^^^^^^^^^^^^^^^^^

Kombinace písmenka "d" spolu s písmenky "w" / "e" / "b" a případně i čísly
uprostřed mezi nimi.

Co se týče mazání slova, tak lze použít zkratku namísto skoku na nějaký kraj
a až pak smazat znaky na druhý kraj. Jde o::

   daw

.. tip::

   Kromě mazání slova (aw = a word) lze mazat i věty (as = a sentence) nebo
   celé odstavce (ap = a paragraph)::

      das
      dap

   Tyto zkratky se budou hodit i v kapitolce `Přepisování textu`_-

Mazání po řádcích
^^^^^^^^^^^^^^^^^

a) aktuální řádek

   * dd

     * smaže řádek, na kterém se nachází kurzor

b) od aktuálního řádku dolu

   * dj

     * smaže aktuální řádek a řádek pod ním

   * 3dd

     * smaže aktuální řádek a dva řádky pod ním

   * d + číslo_řádku + G

     * pokud je číslo_řádku větší než číslo řádku, na kterém se nacházím,
       tak maže řádky až po dané číslo_řádku

   * dG

     * až na konec souboru

c) od aktuálního řádku nahoru

   * dk

     * smaže aktuální řádek a řádek nad ním

   * d + číslo_řádku + G

     * pokud je číslo_řádku menší, než číslo aktuálního řádku, tak se maže
       až po daný řádek nahoru

   * dgg

     * až na začátek souboru

.. tip::

   Pokud bych měl nějaký zalomený text, např::

      Dnes je
      pondělí.

   a chtěl tuto větu spojit na jeden řádek spolu s přidáním mezery za slovo
   "je", tak mohu stisknout "J" kdekoliv na prvním řádku pro sjednocení
   s následujícím řádkem. Výsledek pak bude::

      Dnes je pondělí.

Mazání vymezené části textu
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Zde bude k zapotřebí si představit další mód a to Visual. Ten slouží pro
označení textu, se kterým chci dál pracovat. Mám na výběr ze dvou znaků:

* v

  * chci označovat po znacích
  * lze opět kombinovat s pohybovými znaky "h", "e", "$" atd.

* V

  * chci označovat po celých řadcích

Pokud potřebuji upravit začátek výběru textu a naopak konec, tak můžu mezi
těmito dvěmi místy skákat pomocí "o" (malé o).

.. note::

   Ve Visual módu má "o" jiný význam, než v Normal módu (jeden ze vstupů
   do Insert módu).

Dále ještě existuje speciální varianta označení textu a to pomocí CTRL + v,
kde se jedná o takový sloupcový výběr. Příklad::

   # Mějme následující text, ve kterém chci změnit najednou mezery na
   # dvojtečky.

   01 45
   05 00
   08 24

   # Kurzorem najedu na místo první mezery, stisknu CTRL + v a dvojitým
   # kliknutím "j" označím i dva řádky pod tím.

   01| |45
   05| |00
   08| |24

   # Stisknu "r" pro náhrazení znaku (bude probráno za chvíli) a zmáčknu ":".
   # Text nyní bude vypadát následovně:

   01:45
   05:00
   08:24

Nyní zpět k mazání. Pro smazání označeného textu stisknu klasicky "d" nebo i
"x".

.. tip::

   Pro práci s označeným textem se může hodit do budoucnosti vědět i o
   dalších speciálních znacích, které jdou stisknout ve Visual módu:

   * >

     * posune (odsadí) text doprava o jeden tabulátor.

   * <

     * posune text doleva o jeden tabulátor

   * ~

     * změní označení text na opačnou velikost písma. např. pokud nějaké
       písmenko  bylo malé, tak se změní na velké a naopak

Přepisování textu
-----------------

Zkrácená varianta, která kombinuje najednou mazání nevhodného textu a
okamžitý vstup do Insert módu.

.. note::

   Existuje ještě Replace mód, do kterého se vstoupuje velkým písmenem "R",
   který začne jakoby přepisovat vše, co mu stojí v cestě.

   Příklad::

      # Mějme klasickou větu:

      Lorem ipsum dolor sit amet, eos eu aperiri moderatius.

      # Pokud bych vstoupil do Replace módu na začátku řádku a začal psát,
      # tak tento nový text překryje ten starý:

      Přepisuji tuto větu.t amet, eos eu aperiri moderatius.

      # Kdybych ještě zůstal v Replace módu, neodcházel do Normalu a začal
      # mazat to, co jsem nově napsal, tak uvidím zpět původní text, který
      # byl překryt:

      Lorem ipsum dolor sit amet, eos eu aperiri moderatius.

Přepisování po znacích
^^^^^^^^^^^^^^^^^^^^^^

* r

  * hned po stisknutí písmenka "r" stisknu nový znak, který nahradí ten
    starý
  * při použití této varianty není žádný vstup do Insert módu, vše probíhá
    v Normal módu

* s

  * smaže daný znak a stále zůstává v Insert módu pro přepisování

Přepisování po slovech
^^^^^^^^^^^^^^^^^^^^^^

* c

  * kombinace písmena "c" s "w" / "e" / "b" a potažmo i čísly (počtem)

Co se týče kombinace "c" s objekty pro slova (aw) / věty (as) / odstavce (ap),
tak zde je naopak nevýhoda, že zmizí i mezery za / před daný objekt, viz
následující příklad::

   # Mějme větu:

   Dnes je pondělí.

   # ve které chci změnit "pondělí" na "úterý". Pokud použiju kombinaci
   # "caw", tak vstup do Insert módu bude vypadat následovně:

   Dnes je|.|

   # tzn. že první musím vložit mezeru a až pak slovo "úterý". Proto, abych
   # si ušetřil čas, tak budu chtít zanechat při přepisování mezeru (v tomto
   # případě před slovem) pomocí "ciw":

   Dnes je |.|

   # Pro větu to bude "cis" a odstavec "cip".

Přepisování po řádcích
^^^^^^^^^^^^^^^^^^^^^^

* cc (nebo i přes "S")

  * smaže celý řádek, kde je kurzor a přepnutí na Insert mód

Pro více řádku pak platí stejné kombinace, jako jsou uvedené v sekcí "Mazání
po řádcích", kde akorát místo písmenka "d" se bude použít "c".

Přepisování ve vymezené části textu
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Opět přes označení textu a pak stisknutím "c". Pokud by se stisklo "r", tak se
na daném řádku bude tolikrát opakovat nový znak, kolik bylo předtím znaků na
něm.

Nahrazování textu
-----------------

Alias přepisování na několika místech najednou.

Nahrazování na řádku
^^^^^^^^^^^^^^^^^^^

* :s/starý_text/nový_text + ENTER

  * pokud se na daném řadku, kde je kurzor, nachází "starý_text" vícekrát,
    tak bude nahrazen novým textem jen jednou

* :s/starý_text/nový_text/g + ENTER

  * nahradí všechen "starý_text" na řádku

Nahrazování na více řádcích
^^^^^^^^^^^^^^^^^^^^^^^^^^^

* :%s/starý_text/nový_text + ENTER

  * nahradí "starý_text" jen jednou na každém řádku v souboru

* :%s/starý_text/nový_text/g + ENTER

  * nahradí "starý_text" všude v celém souboru

Pokud chci nahrazovat jen ve vymezeném území, např. jen od prvního po pátý
řádek včetně, tak použiju::

   :1,5s/starý_text/nový_text + ENTER

   # nebo

   :1,5s/starý_text/nový_text/g + ENTER

Přesouvání textu
----------------

Alias vyjmutí (smazání) části textu a jeho přesunutí na jiné místo.

Při mazání (přes "d", případně i "x") se obsah smazaného textu ještě ukládá do
paměti. Jednak je to kvůli historii (procházení zpět a vpřed) a druhak pro
opětovné vkládání na stejném / jiném místě, což je nyní náš případ.

* p

  * vloží smazaný text za kurzorem (napravo)

* P

  * vloží smazný text před kurzorem (nalevo)

Kopirování textu
----------------

* y

  * hlavní písmenko pro kopírování, které lze použít samostatně jen ve
    Visual módu

* yy

  * zkopíruje celý řádek, na kterém se nacházím

Pří použití "y" s jakýmkoliv dalším pohybovým znakem lze kopírovat ještě v
Normal módu (netřeba přepínat na Visual). Pro vkládání tohoto zkopírovaného
textu se používají opět písmenka "p" / "P".

Pokročilé ovládání
==================

Práce s více soubory
--------------------

Bez záložek
^^^^^^^^^^^

Soubor, se kterým chci aktuálně pracovat, tak ho uvidím na popředí a ostatní
budou čekat na pozadí, dokud se na ně nepřepnu. Nevýhodou je, že nemám
přehled, jaké soubory jsou otevřené v pozadí, pokud nepoužiju příkaz / plugin.

Otevírání souborů nad sebe a jejich zavírání
""""""""""""""""""""""""""""""""""""""""""""

* :e cesta_k_souboru

  * otevře daný soubor a ostatní otevřené soubory schová

* :bd (:bd!)

  * zavře daný soubor
  * pokud je to jediný soubor, který mám otevřevený, tak na rozdíl od ":q"
    se Vim nezavře, jen zůstané prázdný

Zobrazení přehledu otevřených souborů
"""""""""""""""""""""""""""""""""""""

* :ls

  * zobrazení všech souborů, které jsou otevřeny a pod jakým pořadovým
    číslem (bude se hodit pro přepínání)
  * číslování je od jedničky

Přepínání mezi soubory
""""""""""""""""""""""

* :bn

  * přepne se další soubor v pořadí

* :bp

  * přepne se na předchozí soubor v pořadí

* :b2

  * přepne se na soubor s pořadovým číslem 2

V oknech
^^^^^^^^

Alias zobrazení několika souborů (stejných či různých) do oken tak, abych je
všechny viděl najednou a v případě potřeby mohl mezi nimi přepínat. Okna mohou
být jak vedle sebe (vertikálně), tak i nad / pod sebou (horizontálně).

.. note::

   V každé záložce mohou být jinak rozvrstveny okna.

Vytvoření a zavření oken
""""""""""""""""""""""""

a) stejný soubor ve více oknech

   * CTRL + ws (:sp)

     * vytvořii kopii aktuálního souboru včetně změn a otevře jej v dalším
       okně horizontálním způsobem (pod aktuálním oknem)

   * CTRL + wv (:vsp)

     * to samé, ale nové okno vznikne vpravo vedle aktuálního okna
       (vertikální způsob)

b) různé soubory v oknech

   * :sp cesta_k_souboru

     * načte obsah daného souboru a zobrazí ho v okně pod aktuálním oknem

   * :vsp cesta_k_souboru

     * to samé, ale zobrazí ho ve vedlejším okne napravo

Okno, ve kterém je kurzor se zavírá pomocí::

   CTRL + wq

   # nebo taktéž klasicky

   :q
   :q!
   :qa
   :qa!
   :wq

Zavření všechn ostatních oken kromě aktuálního okna::

   :on

Přepínání mezi okny
"""""""""""""""""""

* CTRL + w + pohybový_směrový_znak

  * tím pohybovým směrovým znakem mám na mysli klasické "h" / "j" / "k" a
    "l", pomocí kterých se lze přepínat mezi okny

Přesouvání oken
"""""""""""""""

* CTRL + w + r

  * přesune okno dolů / doprava, avšak zaleží na typech oknech (nelze
    kombinovat horizontální okno s vertikálním)

* CTRL + w + R

  * přesune okno nahoru / doleva (platá stejná podmína, jako před chvíli)

* CTRL + w + H / J / K / L

  * přesune dané okno na úplně vlevo / dolu / nahoru / doprava, přičemž se
    může změnit i typ okna, např. z vertikálního na horizontálního

Úprava velikosti oken
"""""""""""""""""""""

a) na výšku

   * CTRL + w + +

     * zvětší okno na výšku o jeden řádek

   * 5 + CTRL + w + +

     * zvětší okno o 5 řádků

   * CTRL + w + -

     * zmenší okno o jeden řádek

   * 5 + CTRL + w + -

     * zmenší okno o 5 řádků

   * :res 20

     * nastaví fixní výšku na 20 řádků

b) na šířku

   * CTRL + w + >

     * zvětší okno na šířku o jeden sloupec

   * 5 + CTRL + w + >

     * zvětší okno o 5 sloupců

   * CTRL + w + <

     * zmenší okno o jeden sloupec

   * 5 + CTRL + w + -

     * zmenší okno o 5 sloupců

   * :vert res 80

     * nastaví fixní šířku na 80 znaků

.. tip::

   Pokud bych chtěl mít 2 okna vedle / pod sebe stejně velká, stisknu::

      CTRL + w + =

Se záložkami
^^^^^^^^^^^^

Na rozdíl od varianty bez záložek jednak uvidím ve výchozím stavu nahoře ve
Vimu přehledně záložky se jmény souborů, které v nich mám otevřeny a druhak
mohu mít v nich jinak rozvrstevny okna, což by ve variantě bez záložek nešlo.

Otevírání a zavírání záložek
""""""""""""""""""""""""""""

Novou záložku mohu otevřít jak prázdnou, tak i načtenou s obsahem nějakého
souboru:

a) prázná záložka

   * :tabnew

     * otevře prázdnou záložku (nahoře v terminálu bych měl vidět
       rozdělení na záložky)
     * aktuální záložku poznám jednak podle tučného písmena a druhak podle
       barvy pozadí (je stejné, jako u řádků pod záložkami)
     * pokud bych načíst do této prázdné záložky obsah nějakého souboru,
       tak použiju syntaxi::

          :o cesta_k_souboru

b) záložka se souborem

   * :tabnew cesta_k_souboru

     * načte do záložky rovnou obsah daného souboru

Zavřít záložku/y mohu několika způsoby:

1. :tabc

   * zavře záložku, na které se nacházím, nicméne soubor bude stále otevřený
     v paměti
   * jestliže jsou v daném souboru na dané záložce nějaké změny, které nejsou
     uložené, tak Vim odmítne exekuci tohoto příkazu
   * pro zavření záložky bez uložení je třeba používat ještě vykričník::

        :tabc!

   * pro zavření záložky s uložením změn se použije standardně::

        :wq

   * pro za

2. :tabo (:tabo!)

   * zavře všechny ostatní záložky, ale aktuální ne
   * taktéž Vim zařve, pokud nějaká změna v nějaké záložce není uložena

3. :qa (:qa!)

   * zavření všech záložek a ukončení Vimu

Přecházení mezi záložkami
"""""""""""""""""""""""""

* qt (:tabn)

  * přepne se na další záložku (vpravo)

* qT (:tabp)

  * přepne se na předchozí záložku (vlevo)

* 3gt

  * přene se na třetí záložku v pořadí (počítá se od jedničky)

.. tip::

   Pokud bych chtěl najednou ve všech záložkách spustit stejný příkaz,
   použiju následující syntaxi::

      :tabd příkaz

   U příkazu není třeba na začátku používat dvojtečku.

Přesouvání záložek
""""""""""""""""""

Jestli se mi nelíbí pořádí záložek, tak si ho můžu upravit pomocí syntaxe::

   :tabm nová_pozice_záložky

.. note::

   Zde se naopak čísluje od nuly. Tudíž, pokud chci přesunout aktuální
   záložku na úplný začátek, použiju právě nulu::

      :tabm 0

Exekuce externích příkazů
-------------------------

S dočasným opuštěním Vimu
^^^^^^^^^^^^^^^^^^^^^^^^^

Externí terminálové příkazy se z Vimu spouštějí pomocí vykřičníku za klasickou
dvoutečkou a názvem daného příkazu::

   :!ls -l

Vim bude dočasně schovaný, neboť se zobrazí klasický terminál s výsledkem
příkazu. Pro návrat do editoru se pak stiskne ENTER.

Další možností je:

1. přesunout editor na pozadí klávesovou zkratkou::

      CTRL + z

2. spustit příkaz a do editoru se vrátit příkazem::

      fg

Bez opuštění Vimu
^^^^^^^^^^^^^^^^^

* :w !příkaz

  * výstup příkazu se zobrazí v přikazovém řádku dole

* :r !příkaz

  * výstup se zapíše na aktuální místo kurzoru v souboru
  * pro jiné místo v souboru je nutné uvést i číslo řádku (počítá se od
    nuly, takže vždy 1 dílek ubrat), např. pro 5 řádek v souboru to bude::

       :4r !ls

.. tip::

   Pro vložení obsahu je jiného souboru lze zkratka:

      :r cesta/k/souboru

Pracovní prostředí
------------------

Rozvržení oken a záložek si mohu uložit a zpětně zobrazit při dalším spuštění
Vimu. Stačí aktuální nastavení uložit pomocí příkazu::

   :mks cesta/pro/uložení/souboru.vim

   # Doporučuji vytvořit adresář "~/.vim/sessions/" a ukládat tam

   :mks ~/.vim/sessions/název_uloženého_pracovního_prostředí.vim

Poté stačí při dalším otevření editoru použít příkaz::

   $ vim ~/.vim/sessions/název_pracovního_prostředí.vim

   # nebo taktéž uvnitř Vimu pomocí:

   :source ~/.vim/sessions/název_pracovního_prostředí.vim

.. note::

   Pokud budete používat plugin NERDTree, tak při otevření pracovního
   prostředí nebude strom vidět (BUG). Stačí si otevřít další a hned ho opět
   zavřít (budou vidět dva najednou).

Obnovení souborů
----------------

Vim defaultně nedělá zálohy souborů (soubory s koncovkou "~"). Nicméně i
přesto si uchavává dost informací o poslední editaci souboru pro případ
obnovení (např. se vypnul z ničeho nic počítač).

Při editaci souborů se v daném adresáři objeví skrytý soubor se stejným
názvem editovaného souboru a koncovkou ".swp". Soubor ze zálohy se spustí
pomocí příkazu::

   $ vim -r název_souboru

Objeví se hláška o obnově a doporučení uložit obnovený soubor pod jiným
názvem. Hláška se vypne stisknutím ENTER klávesy. Po editaci v obnoveném
souboru je pak potřeba smazat již starý ".swp" soubor.

Seznam souboru k obnově lze zobrazit příkazem::

   $ vim -r

Přízpůsobení Vimu
=================

Aneb nastavení vlastního vzhledu, zvýrazňování syntaxe, zobrazení řádku s
čísly atd.

Konfigurační soubor
-------------------

Slouží pro ukládání nastavení pro každé budoucí spuštení Vimu. Je třeba jej
vytvořit v domovském adresáři se jménem::

   .vimrc

Rovnou si můžeme napsat i nějaké to základní nastavení::

   set number          " zobraz čísla řádků
   set colorcolumn=80  " ukáž vodorovnou čáru na 80. znaku (lze překročit)

   " Globální nastavení tabulátorů

   set tabstop=4       " velikost tabulátoru podle znaků
   set softtabstop=4  " v souboru nechá původní velikost tabu, ale já
                       " uvidím ve Vimu jen 4 mezery
   set shiftwidth=4    " velikost odsazení (např. ve Visual módu přes ">")
   set expandtab       " zkonvertuje tabulátory na mezery
   set smarttab        " pokud mám nastavený expandtab, tak při mazání se
                       " smažou 4 mezery najednou a ne jen po jedné

   " Nastavení pro jednotlivé soubory

   autocmd Filetype html setlocal ts=2 sw=2 sts=2
   autocmd Filetype css setlocal ts=2 sw=2 sts=2
   autocmd Filetype js setlocal ts=2 sw=2 sts=2

.. note::

   Dvojitá otevírací uvozovka slouží pro komentáře (nutno bez zavírací).

Pluginy
-------

Aneb zásuvné moduly, které rozšířují funkčnost Vimu. Mohu si je vytvořit sám
nebo použít už nějaký hotový od někoho.

Plug
^^^^

https://github.com/junegunn/vim-plug

Vim Plug je z mnoha nástrojů pro správu modulů. Umí klasicky stáhnout
externí moduly, nainstalovat je a aktivovat je pro každou instanci Vimu.

Lze ho stáhnout příkazem::

   curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

DÁle není třeba nic instalovat. Stačí jen ve Vimu vyjmenovat moduly (externí),
které chci použivat::

   call plug#begin('~/.vim/plugged')

   Plug 'název_uživatele/název_repozitáře_na_githubu'
   Plug 'https://adresa.doména/cesta/k/git/repozitáři.git'

   call plug#end()

Nyní je třeba znovu načíst konfigurační soubor (lze rovnou z Vimu)::

   :source ~/.vimrc

Pak stačí spustit příkaz pro instalaci vyjmenovaných modulů::

   :PlugInstall

Kdybych přestal nějaký plugin používat, tak jej odstraním z konfiguráku a
odintaluji pomocí::

   :PlugClean

   # nebo bez potvrzení

   :PlugClean!

Colorschemes
^^^^^^^^^^^^

https://github.com/flazz/vim-colorschemes

Kompletní balík s několika barevnými schématy pro vzhled Vimu včetně
zvýrazňování syntaxe::

   Plug 'flazz/vim-colorschemes'

   colorscheme název_schématu " např. colorscheme badwolf

Seznam všech schémat lze najít ve složce "colors", viz odkaz nahoře na
GitHub repozitář. Ve Vimu si je lze všechy po jednom dočasně prohlížet
pomocí příkazu::

   :colorscheme název_schématu

Polyglot
^^^^^^^^

https://github.com/sheerun/vim-polyglot

Kompletní balík s podporou pro několik programovacích jazyků a speciálních
typů souborů, který vylepší zvýraznění (zbarvení) syntaxe (pro komentáře,
funkce aj. budou použity barvy z námi vybraného barevného schématu)::

   Plug 'vim-polyglot'

Airline
^^^^^^^

https://github.com/vim-airline/vim-airline

Barevná a přehledná statusová lišta, která je přilepena na konci editoru.
Ukazuje informace o aktuálním módu, čísla řádku / sloupečku aj.

Instalace a nastavení::

   Plug 'vim-airline/vim-airline'

   set laststatus=2                           " vždy zobraz Airline lištu
   let g:airline_powerline_fonts=1            " včetně ikonek
   let g:airline#extensions#tabline#enabled=1 " nastyluj i záložky nahoře

Aby Airline správně fungoval (správné zobrazení šipek a ikonek), tak je třeba
použít takový font, který obsahuje speciální znaky. Pro Ubuntu existuje
stejnojmenný rozšiřující font. Stačí je stáhnout následujícími příkazy::

   wget -P ~/.local/share/fonts/ https://github.com/powerline/fonts/raw/master/UbuntuMono/Ubuntu%20Mono%20derivative%20Powerline.ttf
   wget -P ~/.local/share/fonts/ https://github.com/powerline/fonts/raw/master/UbuntuMono/Ubuntu%20Mono%20derivative%20Powerline%20Bold.ttf
   wget -P ~/.local/share/fonts/ https://github.com/powerline/fonts/raw/master/UbuntuMono/Ubuntu%20Mono%20derivative%20Powerline%20Italic.ttf
   wget -P ~/.local/share/fonts/ https://github.com/powerline/fonts/raw/master/UbuntuMono/Ubuntu%20Mono%20derivative%20Powerline%20Bold%20Italic.ttf

Posléze je načíst pomocí::

   fc-cache -vf ~/.local/share/fonts/

a v neposlední řádě změnit font pro terminál v grafickém rozhraní na::

   Ubuntu Mono derivative Powerline Regular

Pro Airline taky existují barevná schémeta, mě nicméně vyhovuje výchozí
vzhled.

NERDTree
^^^^^^^^

https://github.com/scrooloose/nerdtree

Zobrazovač stromu se souborami a adresářemi (složkami) uvnitř Vimu, díky
kterému lze klasicky procházet adresářovou strukturou a otevírat soubory.

Instalace::

   Plug 'scrooloose/nerdtree'

Defaultně není strom po spuštění Vimu vidět, tak si ho musím otevřít
příkazem::

   :NERDTree

   # nebo stačí jen ":N", stisknout tabulátor pro automatické dokončení a
   # ENTER.

Strom se různými písmenky a klávesovými zkratkami. Jejich přehled lze najít
v nápovědě. Je nutné být kurzorem v okně stromu a stisknout "?". Po zavření
nápovedy se taktéž stiskne otázník.

Popis stromu
""""""""""""

Ukázkový strom::

   " Press ? for help

   .. (up a dir)
   /home/jméno_uživatele/
   > název_složky/
     název_souboru

Význam posledních dvou řádku je více než zřejmý, nicméně pro jistotu
vysvětlím i dva nadřazenější:

* .. (up a dir)

  * pro vstupování do nadřazeného adresáře

* /home/jméno_uživatele/

  * cesta (místo na disku), kde se nacházejí adresáře a složky, které vidím
    ve stromu pod tímto řádkem

Navigace ve stromu
""""""""""""""""""

Abych nemusel zdlouhavě jezdit / skákat klasickými kurzorovými pohyby, tak
mohu použít i speciální pro navigaci ve stromu.

* P

  * skočí kurzorem pod řádek ".. (up a dir)", kde vidím cestu na místo, kde
    se nacházejí adresáře a soubory, které právě vidím

* p

  * pokud mám rozbalené vnořené adresáře, tak kurzor skočí na řádek s
    nadřazeným adresářem

* J

  * skočí na poslední řádek obsahu daného adresáře

* K

  * skočí na první řádek obsahu daného adresáře

* CTRL + J

  * skočí na vedlejší adresář dolu, pokud je kurzor u nějakého adresáře

* CTRL + K

  * to samé, akorát na vedlejší adresář nahoru

Práce s adresářemí
""""""""""""""""""

**Rozbalování a zabalování adresářů:**

* o

  * rozbalí / zabalí obsah daného adresáře

* x

  * zabalí adresář, ve kterém se nachází kurzor (ten může být klidně u
    souboru) a ten se posune na nadřazený adresář

**Vstupování do adresářů a vystupování z nich:**

Je nutné rozlišit, zda vstupuji / vystupuji jen vizuálně nebo i reálně. U
vizuální varianta uvidím jiný obsah adresáře, kdežto u reálně se virtuálně
nastaví cesta na daný adresář (vhodné pro exekuci externích příkazů odsud).

* C

  * vstoupí dovnitř daného adresáře a zobrazí jeho obsah
  * pozor, může nastat i menší prodleva, neboť NERDTree musí rozhodnout, zda
    jsem zmáčknul jen "C" nebo "CD" (viz níže)

* u

  * vstoupí do nadřazeného adresáře

* U

  * taktéž vstoupí do nadřazeného adresáře, ale nechá rozbalený adresář, ve
    kterém jsem byl předtím

* cd

  * nastaví reálnou cestu na daný adresář

* CD

  * vrátí se zpátky do adresáře, na kterou mám nastavenou cestu přes "cd" a
    zobrazí jeho obsah

**Aktualizace obsahu adresáře:**

Pokud vznikne v daném adresáři nová adresář / soubor, tak ho ve stromu
neuvidím, dokud se neaktualizuje.

* r

  * aktualizuje obsah daného adresáře

* R

  * aktualizuje obsah ve všech adresářích, které právě vidím ve stromu

**Tvoření / přejmenování / přesouvání / kopírování / mazání adresářů:**

Tyto akce se provádí až v menu, které je třeba otevřít v okně stromu pomocí
písmenka::

   m

Dole v příkazovém řádku pak uvidím, jaké akce mám na výběr a pomocí jakých
písmenek je vyvolám. Pro zavření menu bez žádné akce se stiskne ESC.

* m + a + název_podadresáře/ + ENTER

  * přidá jeden nebo více vnořených podadresářů najednou
    (nezapomenout na lomítko na konci, jinak se vytvoří soubor)

* m + m + nový_název_adresáře + ENTER

  * přejmenuje daný adresář (netřeba lomítko na konci)

* m + m + upravená_cesta_do_adresáře + ENTER

  * přesune daný adresář na jiné místo

* m + c + cesta_pro_vložení_zkopírovaného_adresáře + ENTER

  * zkopíruje daný adresář a jeho kopii vloží na vybrané místo

* m + d + potvrzení_či_odmínutí

  * smaže daný adresář, pokud ho potvrdím ještě stiskem "y"

Práce se soubory
""""""""""""""""

**Otevírání souborů:**

* o

  * otevře daný sobor na další okno (při opětovném stisku se nic nebude dít)

* s

  * otevře soubor do dalšího okna vedle sebe (lze opakovat)

* i

  * otevře soubor do dalšího okna pod sebe (lze opakovat)

* t

  * otevře soubor na další záložku a hned se na ní přepne

* T

  * otevře soubor tiše na další záložku (nepřepne se na ní)

Poslední čtyři písmenka lze uplatnit i na adresáře, pokud by to bylo někdy k
zapotřebí.

**Tvoření / přejmenování / přesouvání / kopírování / mazání souborů:**

Platí úplně stejný princip jako u adresářů, tj. v okně stromu stisknout "m"
pro zobrazení menu a v něm si vybrat, jakou akci chci provést.

* m + a + název_souboru + ENTER

  * vytvoří soubor v daném adresáři (u jeho názvu nemusí být kurzor)

* m + m + nový_název_souboru + ENTER

  * přejmenuje daný soubor

* m + m + upravená_cesta_do_adresáře + ENTER

  * přesune soubor na jiné místo

* m + c + cesta_pro_zkopírovaný_soubor + ENTER

  * vytvoří kopii daného souboru a vloží na požadovaném místě

* m + d + potvrzení_či_odmínutí

  * smaže daný soubor, pokud to potvrdím ještě stiskem písmenka "y"

Konfigurace NERDTree
""""""""""""""""""""

Pokud někdo chce, aby pokaždé při startu viděl NERDTree strom, tak nechť
napíše do konfiguračního souboru následující řádek::

   autocmd vimenter * NERDTree

Já nicméně preferuji následující dvě varianty:

1. ukaž strom, když není uveden soubor

   * když v terminálu při otevření Vimu neuvedu žádný soubor::

        $ vim

   * nastavení::

        autocmd StdinReadPre * let s:std_in=1
        autocmd VimEnter * if argc() == 0 && !exists("s:std_in") | NERDTree | endif

2. ukaž strom, pokud otevírám adresář

   * když v terminálu místo názvu souboru odkažu na název adresáře::

        $ vim název_adresáře/

   * nastavení::

        autocmd StdinReadPre * let s:std_in=1
        autocmd VimEnter * if argc() == 1 && isdirectory(argv()[0]) && !exists("s:std_in") | exe 'NERDTree' argv()[0] | wincmd p | ene |

.. _Vim: https://en.wikipedia.org/wiki/Vim_(text_editor)
.. _Vi: https://en.wikipedia.org/wiki/Vi
.. _GitHubu: https://github.com/vim/vim
.. _Vim tahák: https://vim.rtorr.com/
