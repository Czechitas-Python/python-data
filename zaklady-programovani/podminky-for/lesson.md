Zatím všechny naše programy vypadaly jako sekvence příkazů vykonávané jeden za
druhým. Pro komplikovanější programy ale budeme potřebovat umožnit, aby se
některé části programu vykonaly jen za určitých _podmínek_ , nebo se
vykonávaly opakovaně v _cyklu_.

## Podmínky pro řízení běhu

V minulých kapitolách už jsme viděli podmínky při chroustání seznamů. Ty v
podstatě řídily, které hodnoty se dostanou do našeho výsledného seznamu.
Mnohem mocnější nástrojem jsem ovšem podmínky, které dokáží ovlivnit běh
samotného programu.

Představte si, že chceme napsat program, který určí, zda je hrací kostka
férová či falešná. Program načte experimentální data se souboru do proměnné
hody.. Ovšem k tomu, aby náš program fungoval, potřebujeme hodů dostatek. Ze
tří hodů kostkou těžko určíme, jestli je nebo není fér. Dejme tomu, že pro
spolehlivý výsledek požadujeme alespoň tisíc hodů kostkou. Pokud je hodů málo,
můžeme uživateli oznámit, že výsledek není spolehlivý.

    import statistics
    
    soubor = open('hody.txt')
    hody = [int(hod) for hod in soubor]
    soubor.close()
    
    if len(hody) < 1000:
      print('Nespolehlivý výsledek kvůli nedostatku dat.')
    
    print(statistics.mean(hody))

Pokud bychom při nedostatku dat vůbec nechtěli vypisovat výsledek, můžeme do
podmínky přidat další příkaz, který program ihned ukončí

    if len(hody) < 1000:
      print('Nespolehlivý výsledek kvůli nedostatku dat.')
      exit()

## Bloky

Všimněte si, že všechny příkazy, které jsou součástí naší podmínky, jsou
odsazené kousek doprava. Tímto poprvé narážíme na takzvané bloky kódu. Blok je
způsob jak seskupit posloupnost příkazů do jednoho celku. Takový celek pak
může být součástí podmínky nebo, jak později uvidíme, například cyklu. Blok
vždy začíná dvojtečkou na konci předchozího řádku. Tím říkáme k jaké
konstrukci (v našem případě `if`) náš blok příkazů patří.

Odsazování bloků se provádí buď pomocí několika mezer. Podobně jako v případě
jmen proměnných, zde opět přichází do hry různé programovací styly. Někteří
programátoři mají rádi pro odsazení dvě mezery, jiní čtyři, někteří dokonce
používají jeden tabulátor. Opět je to na jakémsi vašem estetickém cítění.

Pokud si zvolíte konkrétní styl, je velice důležité jej dodržovat. Pokud v
rámci jednoho bloku budete míchat různé počty mezer pro odsazení, Python
vašemu kódu nebude rozumět a bude si na vás stěžovat (rozuměj: vyhazovat
chyby).

### Podmínky se dvěma větvemi

Podmínky mohou být mnohem zajímavější a komplexnější, než jak jsme viděli před
chvíli. Například mohou mít jak pozitivní tak negativní větev. Negativní větev
se spouští, pokud výraz v podmínce vrátí `False`. Můžeme pak například psát:

    if len(hody) < 1000:
      print('Nespolehlivý výsledek kvůli nedostatku dat.')
      exit()
    else:
      print('Výsledek je dostatečně spolehlivý.')

## Cvičení

### Dělení

Napište program `deleni.py`, který na příkazové řádce obdrží dvě celá čísla a
vypíše jejich podíl zaokrouhlený na tři desetinná čísla. Pokud je druhé číslo
0, program vypíše hlášku, že nulou dělit nelze.

### Kontrola souboru

Napište program `zpracovani.py`, který na příkazové řádce obdrží název
souboru. Pokud soubor končí příponou `.csv`, program vypíše název tohoto
souboru na obrazovku. Pokud má soubor jinou příponu, programu zahlásí, že daný
soubor neumí zpracovat.

V tomto příkladu se vám může hodit metoda řetězců s názvem `endswith` ([viz
dokumentace](https://docs.python.org/3/library/stdtypes.html#str.endswith)).

Hotovo!

Hurá, pokud jste dorazili až sem, máte hotovo. Nalepte si lísteček a pokud
chcete, můžete pokračovat bonusovými příklady.

## Bonusy

### Maximum ze dvou čísel

Napište program `max2.py`, který dostane na vstupu dvě celá čísla a vrátí
větší z nich. Vyhněte se použití funkce `max()`.

### Maximum ze tří čísel

Opět bez použití funkce `max()` napište program `max3.py`, který dostane na
vstupu tři celá čísla a vrátí největší z nich.

## Cyklus FOR

Nyní už jsme připravení na pořádnou jízdu. V předchozí částí jsme si ukázali,
jak nějakou část kódu vynechat, pokud není splněna nějaká podmínka. Nyní si
ukážeme, jak nějakou část kódu opakovat vícekrát po sobě.

Cyklus FOR jste vlastně už ve zjednodušené formě viděli při chroustání
seznamů. Vezměme si například takovýto program:

    jmena = ['petr', 'pavel', 'jitka', 'jana']
    delky = [len(jmeno) for jmeno in jmena]

Se svými zkušenostmi jste jistě schopni popsat, co přesně takový program dělá.
Jednoduše chroustání projde jednotlivé prvky seznamu jmena a vyrobí nový
seznam, který pro každé jméno obsahuje jeho délku.

Co kdybychom ale chtěli projít nějaký seznam prvek po prvku, ale nechtěli
bychom vyrábět žádný nový seznam? Mohli bychom třeba chtít jen vypsat délky
jmen pod sebe na obrazovku. V takovém případě použijeme místo chroustání
seznamů skutečný FOR cyklus:

    jmena = ['petr', 'pavel', 'jitka', 'jana']
    for jmeno in jmena:
      print(len(jmeno))

Všimněte si, že cyklus FOR je v základu dost podobný chroustání seznamů. I
tady říkáme, že se má něco provést pro každý prvek seznamu. Jen teď máme
podstatně větší volnost v tom, co s jednotlivými prvky provedeme. Podobně jako
v případě podmínek můžeme cyklu FOR předat celý blok příkazů najednou:

    jmena = ['petr', 'pavel', 'jitka', 'jana']
    for jmeno in jmena:
      mail = jmeno + '@gmail.com'	
      print(mail)

Dokonce se můžeme opravdu odvázat a vložit do bloku v cyklu FOR i podmínku.

    jmena = ['petr', 'pavel', 'jitka', '', 'jana']
    for jmeno in jmena:
      if len(jmeno) < 1:
        mail = 'neplatný email'
      else:
        mail = jmeno + '@gmail.cz'
      print(mail)

Tímto jsme vlastně vysvětlili to hlavní a zásadní, co o cyklu FOR zatím
potřebujeme vědět. Možná se to na první pohled nezdá, ale přidáním cyklu do
našeho programátorského arzenálu jsme otevřeli pandořinu skříňku plnou
možností, co v našich programech můžeme dělat. Také jsme ovšem otevřeli bránu
do samotných pekel, neboť už si díky cyklům můžeme troufnout na mnohem
komplikovanější problémy. Na ty bude často potřeba pořádně roztočit mozkové
závity.

Ukažme si například, jak se pomocí cyklu spočítá součet všech čísel v seznamu.

    soucet = 0
    for cislo in cisla:
      soucet = soucet + cislo

Ne, že bychom zrovna takovýto kus kódu nutně potřebovali, když můžeme použít
funkci `sum()`. Tento příklad ale ukazuje, že s cykly můžeme dělat spoustu
zajímavých věcí.

## Cvičení

### Hrátky s cykly

Napište program, který dostane na příkazové řádce seznam celých čísel a

  1. vypíše všechna tato čísla pod sebe, každé na nový řádek,
  2. vypíše každé číslo spolu s jeho opačnou hodnotu (obrácené znaménko),
  3. vypíše pouze čísla větší než 0,
  4. čísla větší než 0 vypíše tak jak jsou, čísla menší než nula vypíše s obráceným znaménkem.

### Poznávačky

Popište vlídným, ale přesným slovem, co dělají následující cykly:

  1.     for x in cisla:
      if x % 2 == 0:
        print(x)

  2.     for jmeno in jmena:
      if jmeno[0] == 'p':
        print('pako')
      else:
        print(jmeno)

## Čtení na doma

Ještě než se přesuneme k hlavnímu tématu, ukážeme si, jak dělat hezčí import
funkcí z modulů. Do této chvíle, pokud jsme chtěli použít například funkci
`mean` z modulu `statistics`, psali jsme něco jako.

    import statistics
    prumer = statistics.mean(data)

Pokud funkce z tohoto modulu používáme v našem programu často, budeme název
`statistics` psát tolikrát, až se upíšeme k smrti. Abychom byli při psaní kódu
efektivnější, přejmenujeme si během importu název modulu na něco kratšího,
například takto

    import statistics as stat
    prumer = stat.mean(data)

Může se nám také stát, že z nějakého modulu potřebujeme jen některé funkce,
například funkce `randint()` a `uniform()` z modulu `random`. V takovém
případě můžeme funkce importovat takto

    from random import randint, uniform

Takto importované funkce pak můžeme používat **bez tečkové notace**

    from random import randint, uniform
    hod_kostkou = randint(1, 6)
    hod_desetinnou_kostkou = uniform(1, 6)

### Podmínky s více větvemi

V této lekci jsme si zatím představili pouze podmínky s jednou nebo dvěma
větvemi. Když chci něco provést jen v případě, že jsem z písemky dostal více
než 90 bodů, napíšu podmínku s jednou větví.

    if bodu > 90:
      print('Dobrá práce')

Pokud chci něco provést v případě, že podmínka nebyla splněna, použiju
podmínku s dvěma větvemi.

    if bodu > 90:
      print('Dobrá práce')
    else:
      print('Špatná práce')

Co kdybych ale například chtěl rozdělit známky podle počtů bodů? Tedy za více
než 90 by bylo A, za 80 až 90 B a tak dále. V takovém případě bych mohl použít
podmínku s více větvemi.

    if bodu >= 90:
      print('A')
    elif bodu >= 80:
      print('B')
    elif bodu >= 70:
      print('C')
    elif bodu >= 60:
      print('D')
    elif bodu >= 50:
      print('E')
    else:
      print('F')

Zde je dobré vědět, jakým způsobem Python takovou podmínku vyhodnocuje.
Nejdřív se podívá, jestli je splněna první větev. Pokud ano, vykoná příslušný
blok kódu a **zbytek větví přeskočí**. Pokud první větev není splněna, zkouší,
jestli je splněna druhá. Pokud ano, vykoná příslušný blok a opět zbytek
přeskočí. Takto pokračuje dokud nevyčerpá všechny větve nebo nenarazí na
`else`. Důležité je tedy zapamatovat si, že pokud výraz v nějaké větvi uspěje,
zbytek větví se přeskočí a Python se na ně ani nepodívá.

## Úložky na doma ‒ povinné

### Heslo

**Obtížnost: Pohodička**

Napište program `login.py`, který na příkazovém řádku obdrží uživatelské jméno
a heslo. Program bude mít v sobě uloženo správné heslo a pokud jej uživatel
zadá, program vypíše něco ve smyslu "přístup povolen". Zadá-li uživatel špatné
heslo, program odpoví "přístup odepřen".

### Převod na USD

**Obtížnost: To dáš**

Napište program `usd.py`, který bude umět převádět měnu na americké dolary.
Když program zavoláte takto

    $ python3 usd.py czk 550

převede 550 českých korun na americké dolary. Pokud jej zavoláte takto

    $ python3 usd.py eur 21

převede 21 euro na americké dolary.

Jako přídavek můžete do svého programu přidat tolik měn, kolik se vám líbí.

### Banka

**Obtížnost: To dáš**

Napište program, který z textového souboru přečte seznam zůstatků na spořících
účtech a vypíše tyto zůstatky navýšené o 2.5% úrok.

  1. Vypište každý navýšený zůstatek na samostatný řádek.
  2. Vypište jen ty zůstatky, které nejsou záporné.
  3. Zkuste jednotlivé řádky očíslovat. Každý řádek tedy bude obsahovat číslo řádku a výsledný zůstatek.

### Hádanky

**Obtížnost: To dáš**

Projděte si následující program a zkuste předpovědět co nejpřesněji, jaký bude
jeho výstup. Zkuste co nejvýstižněji (jednou dvěma větami) zformulovat, co
program dělá.

  1.     cisla = [3, 5, 8, 0, 4, 2, 0, 7, 6, 2, 0, 5]
    sum = 0
    for cislo in cisla:
      sum = sum + cislo
      if cislo == 0:
        print(sum)
        sum = 0

  2.     cisla = [3, 5, 8, 0, 4, 2, 0, 7, 6, 2, 0, 5]
    index = 0
    for cislo in cisla:
      if index % 2 == 0:
        print(cislo)
      index +=  1

### Vzestupný seznam

**Obtížnost: Zapni hlavu**

Napište program, který o zadaném seznamu celých čísel rozhodne, zda jsou čísla
v tomto seznamu vzestupně seřazena.

## Úložky na doma ‒ nepovinné

### Písemky

**Obtížnost: To dáš**

Napište program, který obdrží seznam známek z písemek a na výstup vypíše
souhrn toho, kolik bylo dohromady jedniček, kolik dvojek, kolik trojek a tak
dále.

### Maximum

**Obtížnost: Zapni hlavu**

Zkuste napsat program, který na vstupu obdrží seznam čísel a najde mezi nimi
nejvyšší číslo. Pozor, bez použití funkce `max()`.

### Druhé maximum

**Obtížnost: Zavařovačka**

Zkuste napsat program, který na vstupu obdrží seznam čísel a najde mezi nimi
druhé nejvyšší číslo. Opět bez použití funkce `max()`.

### K-té maximum

**Obtížnost: Smrt v přímém přenosu**

Napište program, který dostane na příkazové řádce posloupnost čísel. První
číslo udává, kolikáté největší číslo chceme ve zbytku zadaných čísel najít.
Můžeme tak chtít třeba páté největší číslo z 6, 1, 3, 8, 4, 7, 2

    $ python3 kmax.py 5 6 1 3 8 4 7 2
    3

Pokud je nějaké číslo v seznamu dvakrát, bere se jako dvě různá maxima.
Nepoužívejte žádné Python funkce typu `sorted` nebo `max`. Napište všechno
pěkně od píky.

Možností, jak tento úkol vyřešit, je více. Nebojte se zagooglit, nebojte se
být kreativní.

### Ruleta

**Obtížnost: Zapni hlavu**

Na obrázku vidíte rozložení čísel na klasické Francouzské ruletě. Ruleta
obsahuje čísla 0 - 36. Každé číslo s výjimkou nuly je buď sudé nebo liché a
zároveň červené nebo černé. Pro čísla 1 až 10 a 19 až 28 platí, že lichá čísla
jsou červená a sudá jsou černá. Pro zbytek platí obrácené pravidlo, tedy lichá
jsou černá a sudá červená. Nula není ani lichá ani sudá, ani černá ani
červená.

![](/czechitas/python-data/assets/zaklady-programovani/podminky-for/roulette.png)

Napište program, kterému uživatel zadá číslo a program odpoví jestli jde o
číslo sudé nebo liché, černé nebo červené, nebo je to nula.

### Přestupný rok

**Obtížnost: Zavařovačka**

Napište program, který po zadání kalendářního roku vypíše, zda jde o rok
přestupný, či nikoliv. Letopočet je přestupný, pokud je dělitelný čtyřmi.
Roky, které jsou dělitelné 100 jsou ovšem přestupné pouze tehdy, jsou-li
zároveň dělitelné 400.
