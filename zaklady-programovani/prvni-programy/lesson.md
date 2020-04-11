Konzole jazyka Python už nám pomalu přestává stačit na větší a komplikovanější problémy. Potřebovali bychom místo jednoho příkazu spustit příkazů více po sobě a také být schopni si takovou sekvenci příkazů uložit, abychom ji mohli spouštět vícekrát pro různá data. Začneme tedy psát první _programy_.

## Programy

Mějme následující zadání. Spočítejte průměrnou denní teplotu naměřenou za daný týden podle následující tabulky a najděte den, ve který byla teplota nejblíže průměru.

```py
mereni = [
  ['po', 17.3],
  ['út', 16.8],
  ['st', 15.1],
  ['čt', 13.2],
  ['pá', 14.0],
  ['so', 13.9],
  ['ne', 15.8]
]
```

Abychom se dostali k výsledku, budeme s touto tabulkou potřebovat provést několik operací a místo toho, abychom je zadávali do Python konzole jednu po druhé, napíšeme si příkazy jednoduše za sebe do obyčejného textového souboru s příponou `.py`. Pojmenujme jej například `teplota.py`.

```py
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
```

Pokud chceme takovýto program spustit, musíme nejdříve náš terminál nasměrovat na složku, ve které máme uložen náš soubor `teploty.py`. Poté napíšeme do terminálu, **pozor, nikoliv do Python konzole** , následující příkaz.

```shell
$ python3 teploty.py
```

Pozor, že na systému Windows příkaz vypadá takto:

```shell
$ python teploty.py
```

Náš program se sice spustí, ale nevypíše žádný výsledek. To je proto, že když spouštíme programy, Python žádné vysledky sám od sebe nevypisuje. Musíme to provést sami pomocí funkce `print()`. Na konec našeho programu tedy přidáme řádek

```py
print(index)
```

Pokud náš program spustíme znovu, vypíše nám index, na kterém se nachází den s teplotou nejblíže k průměru.

Možná bychom ale chtěli, aby program místo indexu vypsal spíše název dne v týdnu. To zařídíme tak, že poslední řádek změníme na

```py
print(mereni[index][0])
```

Ještě hezčí bude, pokud uživateli sdělíme výsledek nějak přívětivě, například takto:

```py
print(
  'Den s teplotou nejblíž průměru je ' +
  str(mereni[index][0])
)
```

@exercises ## Cvičení [

- jmeno-a-mesto
- vyplata-jako-program
- teploty-jako-program
  ]@

Hotovo!

Hurá, pokud jste dorazili až sem, máte hotovo. Nalepte si lísteček a pokud chcete, můžete pokračovat bonusovými příklady.

## Moduly

Doposud jsme v našich programech měli k dispozici pouze několik základních funkcí. Zatím jsme viděli tyto

`abs`, `round`, `len`, `sum`, `min`, `max`, `sorted`, `int`,
`float`, `str`, `print`.

Později si ukážeme, že jich ještě několik přibude, ale o moc víc jich už k dispozici není. S takto omezeným množstvím funkcí bychom si dlouho nevystačili. Python naštěstí nabízí mnoho takzvaných _modulů_ , které obsahují spousty dalších užitečných funkcí.

Moduly jsou v podstatě balíčky funkcí zaměřených na nějaké konkrétní téma, například statistika, zpracování textu, práce se soubory na disku apod. Pokud chceme používat funkce z nějakého modulu, musíme jej nejdřív takzvaně _importovat_.

Prvním velmi užitečným balíčkem funkcí je modul `math`. Importujeme jej příkazem

```py
import math
```

který napíšeme na začátek našeho programu. Pokud pracujeme v Python konzoli, napíšeme tento příkaz prostě na konzoli a dokud ji nezavřeme, můžeme modul používat.

Kromě mnoha jiných obsahuje modul `math` funkce `ceil()` a `floor()`, které zaokrouhlují buď vždy jen dolů nebo jen nahoru. Abychom je mohli zavolat, musíme použít tečkovou notaci.

```pycon
>>> math.ceil(3.1)
4
>>> math.floor(3.7)
3
```

Mnozí z vás už si stěžovali, že Python neobsahuje funkci, která počítá průměr. Nyní takovou funkci můžeme získat, pokud importujeme modul `statistics`. Tento modul obsahuje mimo jiné funkci `mean()`, která počítá vytoužený průměr.

```pycon
>>> import statistics
>>> statistics.mean([1, 2, 3, 4, 5, 6])
3.5
```

Poslední avšak velmi důležitý modul, jenž si v tuto chvíli představíme, je modul `sys`. Ten obsahuje funkce, které umožňují Pythonu komunikovat s operačním systémem, ve kterém je spuštěný. Nás z tohoto modulu bude zajímat především proměnná (ano, moduly mohou obsahovat kromě funkcí také proměnné) s názvem `argv` Ta nám umožní přistupovat k takzvaným _parametrům příkazové řádky_.

## Parametry příkazové řádky

Všechny programy, které jsme zatím společně vytvořili, obsahovaly všechna nezbytná data jaksi natvrdo přímo uvnitř kódu programu. Možná vás napadne, že například program, který má naměřené teploty z minulého týdne zadrátované přímo uvnitř kódu, nám je jen pramálo k užitku. Nemůžeme mu předat nově naměřené teploty jinak, než upravit jeho zdrojový kód. Do skutečně užitečného programu musíme být schopni dostat data jaksi z venku. K tomu máme vícero možností ‒ například nahrát data ze souboru na disku, což se naučíme v příští lekci, můžeme je stáhnout z internetu (také se časem naučíme), ale také je můžeme programu předat přímo na příkazové řádce, když jej spouštíme.

Představme si například program, kterému bychom chtěli předat počet minut a on by nám vypsal v hezkém formátu kolik to dohromady dělá hodin a zbylých minut. Pojmenujme náš program například `cas.py`. Pokud chceme zjistit, jaký čas představuje 325 minut, zavoláme náš program takto:

```pycon
$ python3 cas.py 325
```

Číslo 325 v tomto příkazu je právě to, čemu říkáme _parametr_. Teď už jen
zbývá se k tomuto číslu nějak dostat zevnitř našeho programu.

```py
import sys
celkem = int(sys.argv[1])
hodin = celkem // 60
minut = celkem % 60
print(str(hodin) + ':' + str(minut))
```

To nejdůležitější se děje na druhém řádku, kde používáme hodnotu
`sys.argv[1]`. Proměnná `sys.argv` totiž obsahuje seznam všech parametrů,
které náš program dostal na příkazovém řádku. Zajímavé je, že tento seznam
jako první položku obsahuje samotný název programu. Tedy, pokud bychom si
nechali proměnnou `sys.argv` vytisknout na obrazovku, byl by její obsah po
spuštění našeho programu

```
['cas.py', '325']
```

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

```py
import sys
cisla = [int(c) for c in sys.argv[1:]]
print('Součet zadaných čísel: ' + str(sum(cisla)))
```

Program poté můžeme volat třeba takto:

```shell
$ python3 soucet.py 57 41 37 22 12
Součet zadaných čísel: 169
```

Všimněte si, že na druhém řádku našeho programu používáme `sys.argv[1:]`. Je
to proto, abychom se zbavili názvu programu, který vždy zabírá první prvek
seznamu parametrů. Naše čísla se tedy nacházejí až od prvního indexu nahoru.

@exercises ## Cvičení [

- cas-v-minutach
- zaokrouhlovani
- domena-a-url
- prumer-versus-median
  ]@

Hotovo!

Hurá, pokud jste dorazili až sem, máte hotovo. Nalepte si lísteček a pokud
chcete, můžete pokračovat bonusovými příklady.

@exercises bonuses [
- klasicke-zaokrouhlovani
  ]@

## Čtení na doma

Opět je zde pro vás malá samovzdělávací lekce. Nejdříve se podíváme na to, jak
můžeme do chroustání seznamů zapojit podmínky, ukážeme si, jak se generují
náhodná čísla a potom si představíme další zajímavou hodnotu.

### Podmínky

Podmínky slouží k tomu, abychom nějaký kus kódu mohli vykonat jen v případě,
že je splněna nějaká podmínka. Nejjednodušší použití podmínek najdeme při
zpracování seznamů. Mějme například seznam uběhnutých kilometrů a chceme z něj
jen nenulové hodnoty.

```pycon
>>> ubehnuto = [12, 0, 4, 5, 0, 6]
>>> [beh for beh in ubehnuto if beh != 0]
[12, 4, 5, 6]
```

Nebo bychom mohli z následujícího seznamu měst chtít pouze názvy těch měst,
která mají nad 50 000 obyvatel.

```pycon
>>> mesta = [['Zlín', 76010], ['Jičín', 16792], ['Aš', 13093]]
>>> [mesto[0] for mesto in mesta if mesto[1] > 50000]
['Zlín']
```

### Náhodná čísla

Jeden z velmi zajímavých a užitečných modulů v Pythonu, který jsme na hodině
nezmínili, je modul zvaný `random`. Slouží ke generování náhodných čísel a
jiných náhodných věcí. Podíváme se na funkce `randint()` a `uniform().`

Funkce `randint(a, b)` generuje náhodná celá čísla ze zadaného intervalu.
Můžeme tak simulovat například hody šestistěnnou hrací kostkou:

```pycon
>>> import random
>>> random.randint(1, 6)
4
>>> random.randint(1, 6)
6
>>> random.randint(1, 6)
1
```

Funkce `uniform(a, b)` funguje podobně jako `randint()`, generuje však náhodná
<i>desetinná</i> čísla ze zadaného intervalu.

```pycon
>>> random.uniform(1, 6)
3.0445222265782617
>>> random.uniform(1, 6)
3.655355475003799
>>> random.uniform(1, 6)
4.435795489936791
```

Tyto funkce se nám mohou hodit pro generování náhodných dat nebo pro psaní
různých her a hříček.

### Rozsahy

Za posledních pár lekcí už jsme se naučili používat pěknou řádku typů hodnot:

- celá čísla,
- desetinná čísla,
- řetězce,
- pravdivostní hodnoty,
- seznamy.

Nyní nám přibude jedna navíc, která se jmenuje <term cs="rozsah" en="range">.
Rozsahy slouží k tomu, abychom v Pythonu uměli říct, že chceme všechna čísla z
nějakého rozmezí hodnot. Pokud bychom například chtěli všechna čísla mezi 1 a
10, mohli bychom vyrobit seznam

```py
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

To vypadá přímočaře a jednoduše. Ovšem to pouze do chvíle, kdy po vás budu
chtít seznam od 1 do 10 000. Pokud byste chtěli takový seznam vyrobit, upíšete
se k smrti. Navíc si Python bude muset všechna tato čísla v takovém seznamu
pamatovat a to je trochu zbytečné. Když víme, že v seznamu jsou opravdu
všechna čísla v zadaném rozmezí, stačí si pamatovat jen krajní hodnoty, tedy 1
a 10 000. A přesně k tomu slouží hodnota typu rozsah.

Chceme-li všechna čísla od 1 do 10, napíšeme prostě

```py
range(1, 11)
```

Pozor na to, že funkce `range()` chápe druhý parametr jako **vyjma** , nikoliv
včetně.

Pojďme vyzkoušet, co se stane, když takovýto výraz napíšeme do Python konzole

```pycon
>>> range(1, 11)
range(1, 11)
```

Python nám prostě odpověděl totéž, co jsme napsali, úplně stejně jako
kdybychom napsali prostě číslo 50 nebo řetězec `'ahoj'`. Rozsah je prostě
hodnota, ve které si Python pamatuje dolní a horní mez a to je všechno.
Výhodou rozsahů však je, že je můžeme používat všude tam, kde bychom normálně
použili seznam. Pokud nás například zajímá součet hodnot od 1 do 20, můžeme
prostě napsat

```pycon
>>> sum(range(1, 21))
210
```

Všimněte si, že jsme takto spočítali součet aniž bychom museli vypisovat
všechny hodnoty mezi 1 a 20. Náš nejsilnější kanón je teď samozřejmě
chroustání seznamů a ano, i tam můžeme s výhodou použít rozsahy. Pokud bychom
například chtěli všechny násobky trojky mezi 1 a 100, stačí napsat

```pycon
>>> [x for x in range(1, 101) if x % 3 == 0]
```

Pokud bychom mermomocí chtěli opravdu všechny hodnoty z rozsahu jako seznam,
můžeme jej převést na seznam pomocí funkce `list()`

```pycon
>>> list(range(1, 10))
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

@exercises ## Doporučené úložky na doma [

- minuty
- fahrnheit-vs-celsius
- cesta-k-souboru
- hazeni-kostkou
- karty-1
  ]@

@exercises ## Volitelné úložky na doma [

- hada-na-velblouda
- velblouda-na-hada
  ]@
