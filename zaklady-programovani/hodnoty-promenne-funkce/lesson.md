# Hodnoty, proměnné, funkce

V této kapitole si představíme úplné základy programování v Pythonu. Ještě
nebudeme psát celé programy, ale budeme zatím Pythonu posílat jednotlivé
příkazy a uvidíme, co nám odpoví.

Abychom si mohli s Pythonem povídat, musíme spustit takzvanou _Python
konzoli_. To je prostředí, ve kterém můžeme s Pythonem komunikovat a posílat
mu příkazy.

Pokud pracujete pod Windows, Python konzoli spustíte tak, že do termínálu
napíšete příkaz

    
    
    $ python

Pokud pracujete na Macu nebo Linuxu, správný příkaz je

    
    
    $ python3

**POZOR!** Symbol dolaru na začátku příkazu se do terminálu napíše. Slouží
pouze k tomu, abychom odlišili, že příkaz se píše do terminálu a ne někam
jinam.

**POZOR!** Pokud v Linuxu nebo na Macu spustíte příkaz jako ve Windows,
pravděpodobně se vám spustí jiná verze Pythonu, se kterou vám následující
lekce nebudou fungovat.

## Hodnoty

_Hodnoty_ představují všechny možné druhy dat, se kterými můžou naše programy
pracovat. Hodnoty se dle způsobu použití dělí do různých kategorií zvaných
_datové typy_. Datových typů existuje velké množství. V tuto chvíli si
představíme ty nejzákladnější - celá čísla a desetinná čísla.

### Celá čísla

Nejjednodušší datový typ jsou _celá čísla_. Pod tento typ patří hodnoty jako
12, 1321500, -5, 0 a podobně.

Pokud do Python konzole napíšete hodnotu, Python vám ji vypíše zpátky, což
znamená, že vám rozumí :-)

    
    
    >>> 127
    127

### Desetinná čísla

S celými čísly bychom si dlouho nevystačili. Dalším datovým typem tedy budou
_desetinná čísla_ , např. 13.4, 6.0, -0.0001, 0.0 apod. Pozor, že programátoři
vždycky píší desetinná čísla s tečkou, nikoliv s čárkou.

## Aritmetické operátory

Nyní už máme prostředky k tomu, abychom mohli pomocí Pythonu něco spočítat. V
Pythonu máme k dispozici běžné aritmetické operátory:

  * sčítání: **+**
  * odčítání: **-**
  * násobení: *****
  * dělení: **/**

Díky těmto operátorům můžeme Python použít jako kalkulačku a psát _aritmetické
výrazy_ jako ve škole.

    
    
    >>> 12 * 13 + 10
    
    
    >>> (13.4 - 1.4) / 4

Všimněte si, že můžeme používat kulaté závorky, pokud potřebujeme změnit
prioritu operací.

## Proměnné

Při komplikovanějších výpočtech se nám často stane, že si potřebujeme nějaký
mezivýpočet uložit pro pozdější použití. K tomu nám slouží takzvané
_proměnné_.

Proměnná je jakási pojmenovaná krabička nebo šuplík, do kterého si můžeme
uložit nějakou hodnotu, abychom ji neztratili a mohli ji používat v dalších
výpočtech.

Můžeme například v rámci dietního programu spočítat, kolik vanilkových věnečků
denně jsme spořádali za posledních 5 dní.

    
    
    >>> celkem = 1 + 2 + 4 + 1 + 6
    >>> prumer = celkem / 5

### Jména proměnných

Už od úplných začátků s programováním je dobré učit se dobrým návykům, které
budou později prospěšné nejen vám, ale hlavně lidem ve vašem okolí. Jedním z
takových návyků je správné pojmenovávání proměnných.

  * Název proměnné by neměl začínat velkým písmenem, např. Pocet. Takové názvy jsou rezervované pro speciální typy proměnných, ke kterým se v tomto kurzu nedostaneme. 
  * Název proměnné by neměl obsahovat diakritiku, např. počet. Programovací jazyky vznikaly v anglickém prostředí, kde se diakritika nepoužívá, takže si s ní většina jazyků neporadí. 
  * Víceslovné proměnné nesmí obsahovat mezeru, např. pocet hodin. To by si Python myslel, že to jsou dvě proměnné za sebou a nevěděl by co s tím. Pokud chcete proměnnou s více slovy, použijte takzvanou velbloudí notaci pocetHodin nebo hadí notaci pocet_hodin.
  * Vždy proměnnou pojmenujte tak, aby její název jasně napovídal, co se uvnitř ní nachází. Například proměnná pocet_hodin jasně říká, že v ní bude uložen asi nějaký počet hodin. Můžeme podlehnout touze název proměnné zkrátit například na pcthdn, aby se nám lépe psala. Až ovšem někdo další bude takový program číst, bude mlátit hlavou do stolu, cože proboha znamená zkratka `pcthdn`.
  * Naposledy je dobré si uvědomit, že programy i programátoři se téměř vždy pohybují v mezinárodním prostředí. Takže je vždycky lepší pojmenovávat proměnné anglicky. V tomto kurzu ještě tohle pravidlo trošku rozvolníme, ale i tak si můžete začít zvykat na proměnné s názvem number_of_hours.

## Nástrahy

Dejte pozor na to, že do proměnné se jako do šuplíku ukládá pouze hodnota a
nikoliv celý výpočet. Pokud tedy napíšeme například

    
    
    >>> sazba = 350
    >>> vyplata = 8 * sazba

bude v proměnné vyplata uložena hodnota 2800. Jestliže potom změníme hodnotu v
proměnné sazba na něco jiného, například

    
    
    >>> sazba = 420

v proměnné vyplata bude nadále uložena hodnota 2800. Pokud chceme výsledek
výpočtu aktualizovat, musíme jej spustit znova.

    
    
    >>> vyplata = 8 * sazba

## Cvičení

1

### Výplata

  1. Spočítejte svůj měsíční příjem víte-li, že pracujete 7 hodin denně se mzdou 450 Kč na hodinu. Řekněme, že měsíc má 21 pracovních dní.
  2. Uložte si počet pracovních hodin za den do proměnné hodin, hodinovou mzdu do proměnné mzda a počet pracovních dní do proměnné dni. Spočítejte svou výplatu s použitím těchto proměnných.
  3. Pokud pracujete na živnostenský list, můžete si odečíst 60 % příjmů jako paušál a ze zbytku zaplatíte 15% daň. Uložte si tyto hodnoty do proměnných paušál a dan a spočítejte svůj příjem po zdanění.

Hotovo!

Hurá, pokud jste dorazili až sem, máte hotovo. Nalepte si lísteček a pokud
chcete, můžete pokračovat bonusovými příklady.

## Bonusy

2

### Králičí farma

Králičí farma si objednala sestavení modelu množení králičí populace, aby
dokázala odhadnout své zisky. Model funguje takto.

Počet králičích párů na farmě v aktuálním roce (např. 2005) získáme tak, že
sečteme počet králíků na farmě v roce minulém (2004) a roce předminulém
(2003). Pokud tedy například v roce 2003 žilo na farmě 13 párů a v roce 2004
zde žilo 21 párů, model předpovídá, že v roce 2005 zde bude žít 13 + 21 tedy
34 králičích párů.

Králičí farma započala svůj chov v předminulém roce (2017) s nulovým počtem
králíků a v minulém roce 2018 pořídili svůj první králičí pár. Uložte si tyto
počty do proměnných predminuly a minuly. V aktuálním roce 2019 tak máme stále
jeden pár (`predminuly + minuly`). Uložte tuto hodnotu do proměnné aktualni.

Zodpovězte následující otázky:

  1. Kolik králičích párů bude mít farma za deset let, tedy v roce 2029?
  2. Kdy bude mít farma alespoň 300 králičích párů?

## Funkce

S čísly jsme zatím byli schopní pracovat pouze pomocí aritmetických operátorů.
To nám ale brzy nebude stačit a budeme potřebovat složitejší operace, kterým
říkáme _funkce_.

Funkce je nějaký komplikovanější výpočet zabalený do jakési krabičky. Této
krabičce dáme nějaké jméno, abychom jej mohli používat na různých místech v
našem programu.

Dobrým příkladem je funkce `round()`, která pro nás dělá zaokrouhlování.
Můžeme tedy psát

    
    
    >>> round(3.4)
    3

Tomuto zápisu se říká _volání funkce_. Když funkci voláme, předáváme jí
takzvaný _argument_ , v našem případě číslo 3.4. Když funkci zavoláme s
nějakým argumentem, funkce takzvaně _vrátí_ výsledek.

Funkci si můžeme představit například jako topinkovač. Topinkovač pro nás dělá
nějakou užitečnou činnost, kterou chceme často opakovat (opéká topinky). Má
svoje jméno (topinkovač). Do topinkovače dáme cheba (argument) a spustíme je
(zavoláme). Topinkovač chvíli pracuje a pak nám vrátí výsledek - topinky.
Důležité je, že nemusíme řešit jak to topinkovač vlastné dělá, že dokáže opéct
chleba. Důležité pro nás je, že to umí a že jej můžeme kdykoliv použít.

![Toaster](/czechitas/python-data/assets/zaklady-programovani/hodnoty-promenne-funkce/toaster.jpg)

## Seznamy

Zatím jsme byli schopní do jedné proměnné uložit pouze jednu hodnotu. Pro
práci s daty ale budeme potřebovat pracovat s větším množstvím hodnot než
pouze s jednou. K tomu nám poslouží takzvané _seznamy_

Představme si, že si chci zaznamenat počet vanilkových věnečků snězených za
posledních 7 dní. V Pythonu si můžu pro tento účel vytvořit seznam, který si
uložím do vhodně pojmenované proměnné.

    
    
    >>> venecky = [1, 2, 4, 1, 6, 0, 1]

**POZOR!** Programátoři jsou podivné bytosti, které vždy počítají od nuly,
nikoliv od jedničky. Proto také první hodnota v našem seznamu má index 0.

Chceme-li přistoupit k jednotlivým hodnotám uvnitř seznamu, použijeme k tomu
hranaté závorky.

    
    
    >>> venecky[0]
    1
    >>> venecky[4]
    6

Snadno také můžeme některou hodnotu v seznamu změnit. Například když si
vzpomeneme, že jsme trošku zalhali ohledně konzumace věnečků v sobotu:

    
    
    >>> venecky[5] = 12

Z jednoho seznamu můžeme také získat menší kusy podle zadaných mezí

    
    
    >>> venecky[2:5]
    [4, 1, 6]
    >>> venecky[:3]
    [1, 2, 4]
    >>> venecky[3:]
    [1, 6, 12, 1]

### Vnořené seznamy

Seznam může obsahovat jakékoliv hodnoty, tedy nejen celá čísla. Nezapomeňte,
že seznamy jsou také hodnoty, takže jeden seznam může obsahovat jiný seznam
jako svůj prvek. Například takto:

    
    
    >>> seznam = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

Rozmyslete si, co vypíšou následující výrazy:

    
    
    >>> seznam[0][1]
    
    
    >>> seznam[2][0]
    
    
    >>> seznam[1:][1]
    
    
    >>> seznam[:1][2]

### Užitečné funkce nad seznamy

Pro práci se seznamy se nám může hodit několik funkcí:

`len()`

    Vrátí délku seznamu
`sum()`

    Vrátí součet všech prvků v seznamu
`min()`

    Vrátí nejmenší prvek seznamu
`max()`

    Vrátí největší prvek seznamu
`sorted()`

    Vrátí setříděný seznam

## Cvičení

3

### Pohyby na účtu

Mějme seznam pohybů na nějakém bankovním účtu:

    
    
    pohyby = [1200, -250, -800, 540, 721, -613, -222]

  1. Vypište v pořadí třetí pohyb z uvedeného seznamu. 
  2. Vypište všechny pohyby kromě prvních dvou. 
  3. Vypište kolik je všech pohybů dohromady 
  4. Pomocí volání vhodných funkcí vypište nejvyšší a nejnižší pohyb. 
  5. Spočítejte celkový přírustek na účtu za dané období. Pozor, že přírůstek může vyjít i záporný. 

4

### Známky z písemek

Představme si kurz, v jehož průběhu se píšou čtyři písemky. Kurzu se účastní
šest účastníků.

  1. Vytvořte seznam známek ze všech písemek pro jednoho účastníka. 
  2. Vytvořte seznam, který bude pro každého účastníka obsahovat seznam jeho známek. 
  3. Zjistěte průměrnou známku ze všech písemek pro druhého účastníka v seznamu. 

## Povinné čtení na doma

Přečtěte si povídání o dalších vymoženostech Pythonu, které se nám nevešly do
živé lekce. Cílem je, abyste se postupně učili rozumět textům o programování
bez cizí pomoci.

### Další hezké operátory

Během přednášky jsme neprobrali úplně všechny aritmetické operátory, které
můžeme v Pythonu použít. Kromě sčítání, odčítání, násobení a dělení máme ještě
tyto:

  * Mocnění: ******
  * Celočíselné dělení: **//**
  * Zbytek po dělení: **%**

Mocnění nás zachrání od zdlouhavého opakovného násobení, tedy místo abychom
psali

    
    
    >>> 2*2*2*2*2

můžeme prostě napsat

    
    
    >>> 2**5

Pokud si na chvíli vybavíte kruté hodiny matematiky na střední škole, možná si
vzpomenete, že mocnění lze použít i k zajímavějším výpočtům. Můžeme například
spočítat druhou odmocninu.

    
    
    >>> 16**0.5
    4

Dalším užitečným operátorem je celočíselné dělení. Dejme tomu, že jsme si
dopřáli dlouhou dovolenou, která trvala 33 dní, a chceme spočítat, kolik to
bylo celých týdnů. Normální dělení nám vrátí desetinné číslo, takže místo toho
použijeme dělení celočíselné.

    
    
    >>> 33 // 7
    4

Všimněte si, že nám po čtyřech týdnech zbude ještě pár dní. Pokud chceme
přesně vědět, kolik dní nám bylo po dělení sedmi, použijeme operátor _zbytek
po dělení_.

    
    
    >>> 33 % 7
    5

## Domácí úložky - povinné

Povinné v tomto případě znamená, že budu na další hodině přepokládat, že jste
tyto úkoly alespoň zkusili, ne že se budu na vás zle mračit, když je neuděláte
:-)

5

### Úroky

**Obtížnost: To dáš**

Fíha banka a.s. nabízí na svých stránkách spořící účet s úrokem 2,4 %. Když si
na takový účet uložíte 1 000 000 kč, kolik peněz nastřádáte za 10 let?

6

### Délka filmu

**Obtížnost: Pohodička**

V programu kin se často uvádí délka filmu v minutách. Například rozšířená
verze filmu _Pán prstenů: Dvě věže_ trvá 223 minut. My bychom ovšem délku
filmu raději věděli v hodinách a minutách. Použijte operátory celočíselného
dělení a dělení se zbytkem, abyste spočetli, kolik hodin a minut trvá film
_Pán prstenů: Dvě věže._

7

### Průměrné teploty

**Obtížnost: To dáš**

Následující tabulka obsahuje průměrné roční teploty v České republice za roky
2001 až 2010 (zdroj: Český hydrometeorologický ústav).

rok | teplota °C | 2001 | 7.8  
---|---  
2002 | 8.7  
2003 | 8.2  
2004 | 7.8  
2005 | 7.7  
2006 | 8.2  
2007 | 9.1  
2008 | 8.9  
2009 | 8.4  
2010 | 7.2  
  
Vytvořte reprezentaci této tabulky pomocí seznamu seznamů. Zde existují dvě
možnosti. Nejprve vytvořte seznam, který obsahuje řádky tabulky jako
dvouprvkové seznamy a uložte jej do proměnné radky. Poté vytvořte seznam,
který obsahuje sloupce tabulky, tedy dva seznamy po deseti prvcích. Uložte jej
do proměnné sloupce.

Pro obě tyto reprezentace vyřešte následující úkoly

  1. Získejte teplotu na třetím řádku tabulky. 
  2. Získejte rok na pátém řádku tabulky. 
  3. Získejte poslední řádek tabulky jako seznam. 
  4. Vytvořte tabulku bez prvních dvou řádků. 
  5. Vytvořte tabulku pouze z prvních dvou řádků. 
  6. Vytvořte tabulku obsahující jen řádky 5, 6, 7, 8. 
  7. Použitím proměnné sloupce vypište seznam teplot setřízený vzestupně podle velikosti. Šlo by to i pomocí proměnné radky, ale to ještě neumíme. 

8

### Průměr

**Obtížnost: To dáš**

Mějme proměnnou s, ve které předpokládáme uložený nějaký seznam. Sestavte v
Python konzoli výraz (vzoreček), který spočítá průměrnou hodnotu v takovém
seznamu. Otestujte jej na seznamech různých délek.

## Domácí úložky - nepovinné

Konzumujte, pokud si chcete dál procvičovat Python.

9

### Nový koberec

**Obtížnost: To dáš**

Do místnosti tvaru čtverce o rozloze 30 m2 potřebujeme koupit nový koberec.
Jakou délku má mít strana koberce? Vejde se nám srolovaný do dodávky s
nákladovým prostorem dlouhým 5 m?

10

### Rozpětí

**Obtížnost: To dáš**

Postupujte obdobně jako v úložce **Průměr** , ale tentokrát sestavte výraz pro
výpočet _rozpětí_ , tedy rozdílu mezi minimální a maximální hodnotou.

11

### Vlastní minimum a maximum

**Obtížnost: Zapni hlavu**

Prohlédněte si funkce pro práci se seznamy uvedené dříve v obsahu lekce.
Představte si, že bychom neměli k dispozici funkce `min()` a `max()`. Dokázali
byste vytvořit výraz, který zjistí minimální resp. maximální hodnotu v seznamu
s? Můžete v tomto vzorečku použít cokoliv, co jsme probrali na lekci kromě
samotných funkcí `min()` a `max()`.

12

### Střed seznamu

**Obtížnost: Zavařovačka**

Sestavte výraz, který vrátí číslo nacházející se přesně uprostřed v zadaném
seznamu s. U seznamů liché délky je střed jasně definovaný, ovšem u seznamů
sudé délky nám padne mezi dvě čísla. V takovém případě vyberte jako střed
číslo blíž ke konci seznamu.

13

### Střed seznamu podruhé

**Obtížnost: Smrt v přímém přenosu**

Sestavte vzoreček, který vrátí číslo nacházející se přesně uprostřed v zadaném
seznamu s. Tentokrát však u seznamů sudé délky vyberte jako střed číslo blíž k
_začátku_ seznamu.
