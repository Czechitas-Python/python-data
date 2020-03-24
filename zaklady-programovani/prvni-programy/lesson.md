# První programy

Konzole jazyka Python už nám pomalu přestává stačit na větší a komplikovanější
problémy. Potřebovali bychom místo jednoho příkazu spustit příkazů více po
sobě a také být schopni si takovou sekvenci příkazů uložit, abychom ji mohli
spouštět vícekrát pro různá data. Začneme tedy psát první _programy_.

## Programy

Mějme následující zadání. Spočítejte průměrnou denní teplotu naměřenou za daný
týden podle následující tabulky a najděte den, ve který byla teplota nejblíže
průměru.

    mereni = [
      ['po', 17.3],
      ['út', 16.8],
      ['st', 15.1],
      ['čt', 13.2],
      ['pá', 14.0],
      ['so', 13.9],
      ['ne', 15.8]
    ]

Abychom se dostali k výsledku, budeme s touto tabulkou potřebovat provést
několik operací a místo toho, abychom je zadávali do Python konzole jednu po
druhé, napíšeme si příkazy jednoduše za sebe do obyčejného textového souboru s
příponou `.py`. Pojmenujme jej například `teplota.py`.

    mereni = [
      ['po', 17.3],
      ['út', 16.8],
      ['st', 15.1],
      ['čt', 13.2],
      ['pá', 14.0],
      ['so', 13.9],
      ['ne', 15.8]
    ]
    teploty = [radek[1] for radek in mereni]
    prumer = sum(teploty)/len(teploty)
    rozdily = [abs(t - prumer) for t in teploty]
    min_rozdil = min(rozdily)
    index = rozdily.index(min_rozdil)

Pokud chceme takovýto program spustit, musíme nejdříve náš terminál nasměrovat
na složku, ve které máme uložen náš soubor `teploty.py`. Poté napíšeme do
terminálu, **pozor, nikoliv do Python konzole** , následující příkaz.

    $ python3 teploty.py

Pozor, že na systému Windows příkaz vypadá takto:

    $ python teploty.py

Náš program se sice spustí, ale nevypíše žádný výsledek. To je proto, že když
spouštíme programy, Python žádné vysledky sám od sebe nevypisuje. Musíme to
provést sami pomocí funkce `print()`. Na konec našeho programu tedy přidáme
řádek

    print(index)

Pokud náš program spustíme znovu, vypíše nám index, na kterém se nachází den s
teplotou nejblíže k průměru.

Možná bychom ale chtěli, aby program místo indexu vypsal spíše název dne v
týdnu. To zařídíme tak, že poslední řádek změníme na

    print(mereni[index][0])

Ještě hezčí bude, pokud uživateli sdělíme výsledek nějak přívětivě, například
takto:

    print(
      'Den s teplotou nejblíž průměru je ' +
      str(mereni[index][0])
    )

## Cvičení

1

### Jméno a město

Napište program, který na obrazovku vypíše vaše jméno a na nový řádek město,
ze kterého pocházíte.

2

### Výplata jako program

Na první lekci jsme dělali [cvičení na výpočet výplaty](../hodnoty-promenne-
funkce#vyplata) pomocí proměnných. Udělejte toto cvičení znova, ale tentokrát
jako program. Nejdříve uložte nezbytné hodnoty do proměnných, spočítejte
výplatu a pak ji pomocí funkce `print()` vypište na obrazovku.

3

### Teploty jako program

Minulý týden jsme dělali [cvičení na zpracování teplot](../text-
chroustani#seznam-teplot). Udělejte toto cvičení znovu, tentokrát jako
program, který všechny požadované informace vypíše hezky přehledně na
obrazovku.

Hotovo!

Hurá, pokud jste dorazili až sem, máte hotovo. Nalepte si lísteček a pokud
chcete, můžete pokračovat bonusovými příklady.

## Moduly

Doposud jsme v našich programech měli k dispozici pouze několik základních
funkcí. Zatím jsme viděli tyto

`abs()`, `round()`, `len()`, `sum()`, `min()`, `max()`, `sorted()`, `int()`,
`float()`, `str()`, `print()`.

Později si ukážeme, že jich ještě několik přibude, ale o moc víc jich už k
dispozici není. S takto omezeným množstvím funkcí bychom si dlouho
nevystačili. Python naštěstí nabízí mnoho takzvaných _modulů_ , které obsahují
spousty dalších užitečných funkcí.

Moduly jsou v podstatě balíčky funkcí zaměřených na nějaké konkrétní téma,
například statistika, zpracování textu, práce se soubory na disku apod. Pokud
chceme používat funkce z nějakého modulu, musíme jej nejdřív takzvaně
_importovat_.

Prvním velmi užitečným balíčkem funkcí je modul `math`. Importujeme jej
příkazem

    import math

který napíšeme na začátek našeho programu. Pokud pracujeme v Python konzoli,
napíšeme tento příkaz prostě na konzoli a dokud ji nezavřeme, můžeme modul
používat.

Kromě mnoha jiných obsahuje modul `math` funkce `ceil()` a `floor()`, které
zaokrouhlují buď vždy jen dolů nebo jen nahoru. Abychom je mohli zavolat,
musíme použít tečkovou notaci.

    >>> math.ceil(3.1)
    4
    >>> math.floor(3.7)
    3

Mnozí z vás už si stěžovali, že Python neobsahuje funkci, která počítá průměr.
Nyní takovou funkci můžeme získat, pokud importujeme modul `statistics`. Tento
modul obsahuje mimo jiné funkci `mean()`, která počítá vytoužený průměr.

    >>> import statistics
    >>> statistics.mean([1, 2, 3, 4, 5, 6])
    3.5

Poslední avšak velmi důležitý modul, jenž si v tuto chvíli představíme, je
modul `sys`. Ten obsahuje funkce, které umožňují Pythonu komunikovat s
operačním systémem, ve kterém je spuštěný. Nás z tohoto modulu bude zajímat
především proměnná (ano, moduly mohou obsahovat kromě funkcí také proměnné) s
názvem `argv` Ta nám umožní přistupovat k takzvaným _parametrům příkazové
řádky_.

## Parametry příkazové řádky

Všechny programy, které jsme zatím společně vytvořili, obsahovaly všechna
nezbytná data jaksi natvrdo přímo uvnitř kódu programu. Možná vás napadne, že
například program, který má naměřené teploty z minulého týdne zadrátované
přímo uvnitř kódu, nám je jen pramálo k užitku. Nemůžeme mu předat nově
naměřené teploty jinak, než upravit jeho zdrojový kód. Do skutečně užitečného
programu musíme být schopni dostat data jaksi z venku. K tomu máme vícero
možností ‒ například nahrát data ze souboru na disku, což se naučíme v příští
lekci, můžeme je stáhnout z internetu (také se časem naučíme), ale také je
můžeme programu předat přímo na příkazové řádce, když jej spouštíme.

Představme si například program, kterému bychom chtěli předat počet minut a on
by nám vypsal v hezkém formátu kolik to dohromady dělá hodin a zbylých minut.
Pojmenujme náš program například `cas.py`. Pokud chceme zjistit, jaký čas
představuje 325 minut, zavoláme náš program takto:

    $ python3 cas.py 325

Číslo 325 v tomto příkazu je právě to, čemu říkáme _parametr_. Teď už jen
zbývá se k tomuto číslu nějak dostat zevnitř našeho programu.

    import sys
    celkem = int(sys.argv[1])
    hodin = celkem // 60
    minut = celkem % 60
    print(str(hodin) + ':' + str(minut))

To nejdůležitější se děje na druhém řádku, kde používáme hodnotu
`sys.argv[1]`. Proměnná `sys.argv` totiž obsahuje seznam všech parametrů,
které náš program dostal na příkazovém řádku. Zajímavé je, že tento seznam
jako první položku obsahuje samotný název programu. Tedy, pokud bychom si
nechali proměnnou `sys.argv` vytisknout na obrazovku, byl by její obsah po
spuštění našeho programu

    ['cas.py', '325']

Tedy na prvním místě je název programu a na druhém je náš parametr, který jsme
prve zadali na příkazové řádce. Všimněte si ovšem, že náš parametr je řetězec.
Python totiž všechny parametry na příkazové řádce bere jako řetězce, nehledě
na to, jestli jsou to čísla nebo cokoliv jiného. My chceme ale v našem
programu čas jako číslo, neboť s ním chceme provádět různá matematická
cvičení. Proto musíme náš parametr převést na číslo pomocí již známé funkce
`int()`, což právě provádíme na druhém řádku našeho programu.

### Nač se držet při zemi

Zatím jsme na příkazové řádce předali pouze jeden parametr. Nebuďme ale
troškaři. Na příkazové řádce si můžeme dovolit předávat zajímavější věci,
například celý seznam hodnot. Můžeme kupříkladu napsat program, který spočítá
součet všech zadaných hodnot. Pozor ovšem na to, že hodnoty na příkazové řádce
jsou vždy řetězce, takže pokud je to potřeba, musíme si je sami převést na
čísla.

    import sys
    cisla = [int(c) for c in sys.argv[1:]]
    print('Součet zadaných čísel: ' + str(sum(cisla)))

Program poté můžeme volat třeba takto:

    $ python3 soucet.py 57 41 37 22 12
    Součet zadaných čísel: 169

Všimněte si, že na druhém řádku našeho programu používáme `sys.argv[1:]`. Je
to proto, abychom se zbavili názvu programu, který vždy zabírá první prvek
seznamu parametrů. Naše čísla se tedy nacházejí až od prvního indexu nahoru.

## Cvičení

4

### Čas v minutách

Napište program `minuty.py`, která dělá obrácenou věc než program `cas.py` z
textu výše. Když mu na příkazové řádce předáme dva parametry ‒ počet hodin a
počet minut ‒ například takto

    $ python3 minuty.py 2 54

program nám vrátí délku tohoto času minutách. V tomto případě tedy číslo 174.

  1. Nejprve program napište tak, že si hodnoty 2 a 54 uložíte přímo natvrdo v programu do nějakých proměnných a z nich spočítáte a vytisknete výsledek.
  2. Až když váš program bude fungovat, zkuste tyto proměnné načíst z parametrů příkazové řádky. Nezapomeňte, že parametry jsou vždy řetězce a že první parametr je vždy název vašeho programu.

5

### Zaokrouhlování

Napište program, který dostane na vstupu desetinné číslo a na výstup napíše
toto číslo zakrouhlené nejdříve nahoru, potom dolů a potom běžným Pythonovským
zaokrouhlováním.

6

### Doména na URL

Napište program `url.py`, který jako parametr dostane název domény, například
`kodim.cz` a na výstup vypíše URL, kterou je třeba zadat do prohlížeče pro
přístup k webové stránce na této doméně, tedy `http://kodim.cz`.

7

### Průměr versus medián

Často se hovoří o tom, že průměr není pro některé veličiny (například platy)
vypovídající hodnota a lepší je dívat se na medián. Napište program, který s
použitím funkcí `statistics.mean()` a `statistics.median()` vypíše na výstup
průměr a medián zadaných hodnot. Hodnoty program obdrží na příkazovém řádku.
Příklad použití:

    $ python3 prumer-median.py 2 1 8 3 4 11 7 1512
    Průměr: 193.5
    Medián: 5.5

Hotovo!

Hurá, pokud jste dorazili až sem, máte hotovo. Nalepte si lísteček a pokud
chcete, můžete pokračovat bonusovými příklady.

## Bonusy

8

### Klasické zaokrouhlování

Překvapivě Python neobsahuje žádnou funkci, která by dělala klasické
zaokrouhlování, tedy takové, na které jsme všichni zvyklí ze školy. S něčím
takovým se nemůžeme spokojit.

Napište program, který dostane na vstupu číslo a zaokrouhlí jej klasickým
zaokrouhlováním. Zkuste vymyslet jak to udělat co nejúsporněji s použitím
zaokrouhlovacích funkcí, které už znáte.

## Čtení na doma

Opět je zde pro vás malá samovzdělávací lekce. Nejdříve se podíváme na to, jak
můžeme do chroustání seznamů zapojit podmínky, ukážeme si, jak se generují
náhodná čísla a potom si představíme další zajímavou hodnotu.

### Podmínky

Podmínky slouží k tomu, abychom nějaký kus kódu mohli vykonat jen v případě,
že je splněna nějaká podmínka. Nejjednodušší použití podmínek najdeme při
zpracování seznamů. Mějme například seznam uběhnutých kilometrů a chceme z něj
jen nenulové hodnoty.

    >>> ubehnuto = [12, 0, 4, 5, 0, 6]
    >>> [beh for beh in ubehnuto if beh != 0]
    [12, 4, 5, 6]

Nebo bychom mohli z následujícího seznamu měst chtít pouze názvy těch měst,
která mají nad 50 000 obyvatel.

    >>> mesta = [['Zlín', 76010], ['Jičín', 16792], ['Aš', 13093]]
    >>> [mesto[0] for mesto in mesta if mesto[1] > 50000]
    ['Zlín']

### Náhodná čísla

Jeden z velmi zajímavých a užitečných modulů v Pythonu, který jsme na hodině
nezmínili, je modul zvaný `random`. Slouží ke generování náhodných čísel a
jiných náhodných věcí. Podíváme se na funkce `randint()` a `uniform().`

Funkce `randint(a, b)` generuje náhodná celá čísla ze zadaného intervalu.
Můžeme tak simulovat například hody šestistěnnou hrací kostkou:

    >>> import random
    >>> random.randint(1, 6)
    4
    >>> random.randint(1, 6)
    6
    >>> random.randint(1, 6)
    1

Funkce `uniform(a, b)` funguje podobně jako `randint()`, generuje však náhodná
_desetinná_ čísla ze zadaného intervalu.

    >>> random.uniform(1, 6)
    3.0445222265782617
    >>> random.uniform(1, 6)
    3.655355475003799
    >>> random.uniform(1, 6)
    4.435795489936791

Tyto funkce se nám mohou hodit pro generování náhodných dat nebo pro psaní
různých her a hříček.

### Rozsahy

Za posledních pár lekcí už jsme se naučili používat pěknou řádku typů hodnot:

  * celá čísla,
  * desetinná čísla,
  * řetězce,
  * pravdivostní hodnoty,
  * seznamy.

Nyní nám přibude jedna navíc, která se jmenuje _rozsah_. Rozsahy slouží k
tomu, abychom v Pythonu uměli říct, že chceme všechna čísla z nějakého rozmezí
hodnot. Pokud bychom například chtěli všechna čísla mezi 1 a 10, mohli bychom
vyrobit seznam

    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

To vypadá přímočaře a jednoduše. Ovšem to pouze do chvíle, kdy po vás budu
chtít seznam od 1 do 10 000. Pokud byste chtěli takový seznam vyrobit, upíšete
se k smrti. Navíc si Python bude muset všechna tato čísla v takovém seznamu
pamatovat a to je trochu zbytečné. Když víme, že v seznamu jsou opravdu
všechna čísla v zadaném rozmezí, stačí si pamatovat jen krajní hodnoty, tedy 1
a 10 000. A přesně k tomu slouží hodnota typu _rozsah_ , anglicky _range_.

Chceme-li všechna čísla od 1 do 10, napíšeme prostě

    range(1, 11)

Pozor na to, že funkce `range()` chápe druhý parametr jako **vyjma** , nikoliv
včetně.

Pojďme vyzkoušet, co se stane, když takovýto výraz napíšeme do Python konzole

    >>> range(1, 11)
    range(1, 11)

Python nám prostě odpověděl totéž, co jsme napsali, úplně stejně jako
kdybychom napsali prostě číslo 50 nebo řetězec `'ahoj'`. Rozsah je prostě
hodnota, ve které si Python pamatuje dolní a horní mez a to je všechno.
Výhodou rozsahů však je, že je můžeme používat všude tam, kde bychom normálně
použili seznam. Pokud nás například zajímá součet hodnot od 1 do 20, můžeme
prostě napsat

    >>> sum(range(1, 21))
    210

Všimněte si, že jsme takto spočítali součet aniž bychom museli vypisovat
všechny hodnoty mezi 1 a 20. Náš nejsilnější kanón je teď samozřejmě
chroustání seznamů a ano, i tam můžeme s výhodou použít rozsahy. Pokud bychom
například chtěli všechny násobky trojky mezi 1 a 100, stačí napsat

    >>> [x for x in range(1, 101) if x % 3 == 0]

Pokud bychom mermomocí chtěli opravdu všechny hodnoty z rozsahu jako seznam,
můžeme jej převést na seznam pomocí funkce `list()`

    >>> list(range(1, 10))
    [1, 2, 3, 4, 5, 6, 7, 8, 9]

## Domácí úložky ‒ povinné

9

### Minuty

**Obtížnost: To dáš**

Vytvořte program `casy.py`, který bude zpracovávat seznam naměřených časů v
minutách. Nejprve přímo do programu zadrátujte konkrétní hodnoty například
takto:

    casy = [12, 25, 64, 27, 15, 66, 128, 44]

  1. Vyfiltrujte z tohoto seznamu pouze ty časy, které se vejdou do jedné hodiny.
  2. Vyfiltrujte z tohoto seznamu pouze ty časy, které překračují jednu hodinu a to tak, že výsledkem bude seznam minut, udávajících o kolik jsme jednu hodinu překročili.
  3. Upravte program tak, aby seznam naměřených hodnot obdržel na příkazové řádce.

10

### Fahrnheit vs. Celsius

**Obtížnost: To dáš**

Pokud pečete podle anglických receptů, často se po váš požaduje rozehřát
troubu na uvedenou teplotu. Pokud si ovšem neuvědomíte, že Američané používají
pro měření teploty stupně Fahrenheita namísto Celsia, bude vás na konci pečení
čekat nemilé překvapení.

Nastudujte si na [České
Wikipedii](https://cs.wikipedia.org/wiki/Stupe%C5%88_Fahrenheita) jak se
převádějí stupně Fahrenheita na stupně Celsia a napište program, který takový
převod provede. Váš program dostane na příkazové řádce teplotu ve stupních
Fahrenheita a vypíše její ekvivalent ve stupních Celsia.

11

### Cesta k souboru

**Obtížnost: To dáš**

Ve Windows se cesty k souborům zapisují pomocí zpětných lomítek, tedy
například takto

    cesta\do\rise\smazenych\krevet

Na Unixu (Macu nebo Linux) se naopak cesty píší pomocí dopředných lomítek,
tedy takto

    cesta/do/rise/smazenych/krevet

Napište program, který dostane jako parametr cestu ve Windows stylu a převede
ji na Unix styl.

12

### Házení kostkou

**Obtížnost: Zapni hlavu**

  1. Napište program, který při každém spustění hodí šestistěnnou kostkou ‒ tedy vypíše náhodné číslo mezi 1 až 6.
  2. Upravte program tak, aby jako parametr dostal počet stěn kostky. Bude tedy umět házet třeba sedmistěnnou nebo devítistěnnou kostkou podle toho, jaké číslo dostane na vstupu.
  3. Předejte programu další parametr, který bude udávat kolik hodů má program provést. Program pak na výstup vytiskne seznam tolika hodů, kolik jste zadali na vstupu. Cílem je tedy vymyslet, jak vyrobit seznam náhodných čísel. Jistě se nám k tomu bude hodit chroustání seznamů.

13

### Karty 1

**Obtížnost: Zapni hlavu**

Napište program, který vylosuje náhodnou hrací kartu z klasické whistové sady
obsahující 52 karet, rozdělených do čtyř barev (kříže, srdce, piky, káry), s
hodnotami 2, 3, 4, 5, 6, 7, 8, 9, 10, J (kluk), Q (dáma), K (král), A (eso).

Výstup programu může vypadat například takto:

    Karta: kluk kříže

## Domácí úložky ‒ nepovinné

14

### Jak proměnit hada na velblouda

**Obtížnost: To dáš**

Napište program, který dostane na příkazovém řádku název proměnné v hadí
notaci a vrátí tentýž název zapsaný ve velbloudí notaci.

Příklad:

    $ python3 had-velbloud.py had_honi_velblouda
    hadHoniVelblouda

15

### Jak proměnit velblouda na hada

**Obtížnost: Smrt v přímém přenosu**

Napište program, který dostane na příkazovém řádku název proměnné ve velbloudí
notaci a vrátí tentýž název zapsaný v hadí notaci.

Příklad:

    $ python3 velbloud-had.py velbloudHoniHada
    velbloud_honi_hada

Ano, tohle už není procházka růžovým sadem a jde o úložku spíše pro
fajnšmekry, Python gurmány a lidi s neutišitelnou touhou nenechat žádný
příklad nevyřešený. Vězte, že skutečně existuje řešení, které používá výhradně
probrané techniky. Vyplatí se mrknout na to, jaké všechny metody nabízí Python
řetězce, jinak ale není potřeba žádné googlení, jen se nesmíte bát věci, které
už tak dobře znáte, opravdu použít, a nemít je ve své programátorské dílně jen
vystavené za sklem.

Některé pasáže programu si lze mírně ulehčit použítím funkce `enumerate()`,
která vám při chroustání seznamů vrací nejen prvek seznamu, ale i jeho index.
Vyzkoušejte například následující příkaz

    [[i, jmeno] for i, jmeno in enumerate(['petr', 'jana', 'vlasta', 'onyx'])]

Úlohu lze však vyřešit i bez `enumerate()`!

