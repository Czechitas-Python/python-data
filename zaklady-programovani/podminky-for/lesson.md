Zatím všechny naše programy vypadaly jako sekvence příkazů vykonávané jeden za druhým. Pro komplikovanější programy ale budeme potřebovat umožnit, aby se některé části programu vykonaly jen za určitých _podmínek_ , nebo se vykonávaly opakovaně v _cyklu_.

## Podmínky pro řízení běhu

V minulých kapitolách už jsme viděli podmínky při chroustání seznamů. Ty v podstatě řídily, které hodnoty se dostanou do našeho výsledného seznamu. Mnohem mocnější nástrojem jsem ovšem podmínky, které dokáží ovlivnit běh samotného programu.

Představte si, že chceme napsat program, který určí, zda je hrací kostka férová či falešná. Program načte experimentální data se souboru do proměnné hody.. Ovšem k tomu, aby náš program fungoval, potřebujeme hodů dostatek. Ze tří hodů kostkou těžko určíme, jestli je nebo není fér. Dejme tomu, že pro spolehlivý výsledek požadujeme alespoň tisíc hodů kostkou. Pokud je hodů málo, můžeme uživateli oznámit, že výsledek není spolehlivý.

```py
import statistics

soubor = open('hody.txt')
hody = [int(hod) for hod in soubor]
soubor.close()

if len(hody) < 1000:
  print('Nespolehlivý výsledek kvůli nedostatku dat.')

print(statistics.mean(hody))
```

Pokud bychom při nedostatku dat vůbec nechtěli vypisovat výsledek, můžeme do podmínky přidat další příkaz, který program ihned ukončí

```py
if len(hody) < 1000:
  print('Nespolehlivý výsledek kvůli nedostatku dat.')
  exit()
```

## Bloky

Všimněte si, že všechny příkazy, které jsou součástí naší podmínky, jsou odsazené kousek doprava. Tímto poprvé narážíme na takzvané bloky kódu. Blok je způsob jak seskupit posloupnost příkazů do jednoho celku. Takový celek pak může být součástí podmínky nebo, jak později uvidíme, například cyklu. Blok vždy začíná dvojtečkou na konci předchozího řádku. Tím říkáme k jaké konstrukci (v našem případě `if`) náš blok příkazů patří.

Odsazování bloků se provádí buď pomocí několika mezer. Podobně jako v případě jmen proměnných, zde opět přichází do hry různé programovací styly. Někteří programátoři mají rádi pro odsazení dvě mezery, jiní čtyři, někteří dokonce používají jeden tabulátor. Opět je to na jakémsi vašem estetickém cítění.

Pokud si zvolíte konkrétní styl, je velice důležité jej dodržovat. Pokud v rámci jednoho bloku budete míchat různé počty mezer pro odsazení, Python vašemu kódu nebude rozumět a bude si na vás stěžovat (rozuměj: vyhazovat chyby).

### Podmínky se dvěma větvemi

Podmínky mohou být mnohem zajímavější a komplexnější, než jak jsme viděli před chvíli. Například mohou mít jak pozitivní tak negativní větev. Negativní větev se spouští, pokud výraz v podmínce vrátí `False`. Můžeme pak například psát:

```py
if len(hody) < 1000:
  print('Nespolehlivý výsledek kvůli nedostatku dat.')
  exit()
else:
  print('Výsledek je dostatečně spolehlivý.')
```

@exercises ## Cvičení [

- deleni
- kontrola-souboru
  ]@

Hotovo!

Hurá, pokud jste dorazili až sem, máte hotovo. Nalepte si lísteček a pokud chcete, můžete pokračovat bonusovými příklady.

@exercises bonuses [

- maximum-ze-dvou-cisel
- maximum-ze-tri-cisel
  ]@

## Cyklus FOR

Nyní už jsme připravení na pořádnou jízdu. V předchozí částí jsme si ukázali, jak nějakou část kódu vynechat, pokud není splněna nějaká podmínka. Nyní si ukážeme, jak nějakou část kódu opakovat vícekrát po sobě.

Cyklus FOR jste vlastně už ve zjednodušené formě viděli při chroustání seznamů. Vezměme si například takovýto program:

```py
jmena = ['petr', 'pavel', 'jitka', 'jana']
delky = [len(jmeno) for jmeno in jmena]
```

Se svými zkušenostmi jste jistě schopni popsat, co přesně takový program dělá. Jednoduše chroustání projde jednotlivé prvky seznamu jmena a vyrobí nový seznam, který pro každé jméno obsahuje jeho délku.

Co kdybychom ale chtěli projít nějaký seznam prvek po prvku, ale nechtěli bychom vyrábět žádný nový seznam? Mohli bychom třeba chtít jen vypsat délky jmen pod sebe na obrazovku. V takovém případě použijeme místo chroustání seznamů skutečný FOR cyklus:

```py
jmena = ['petr', 'pavel', 'jitka', 'jana']
for jmeno in jmena:
  print(len(jmeno))
```

Všimněte si, že cyklus FOR je v základu dost podobný chroustání seznamů. I tady říkáme, že se má něco provést pro každý prvek seznamu. Jen teď máme podstatně větší volnost v tom, co s jednotlivými prvky provedeme. Podobně jako v případě podmínek můžeme cyklu FOR předat celý blok příkazů najednou:

```py
jmena = ['petr', 'pavel', 'jitka', 'jana']
for jmeno in jmena:
  mail = jmeno + '@gmail.com'
  print(mail)
```

Dokonce se můžeme opravdu odvázat a vložit do bloku v cyklu FOR i podmínku.

```py
jmena = ['petr', 'pavel', 'jitka', '', 'jana']
for jmeno in jmena:
  if len(jmeno) < 1:
    mail = 'neplatný email'
  else:
    mail = jmeno + '@gmail.cz'
  print(mail)
```

Tímto jsme vlastně vysvětlili to hlavní a zásadní, co o cyklu FOR zatím potřebujeme vědět. Možná se to na první pohled nezdá, ale přidáním cyklu do našeho programátorského arzenálu jsme otevřeli pandořinu skříňku plnou možností, co v našich programech můžeme dělat. Také jsme ovšem otevřeli bránu do samotných pekel, neboť už si díky cyklům můžeme troufnout na mnohem komplikovanější problémy. Na ty bude často potřeba pořádně roztočit mozkové závity.

Ukažme si například, jak se pomocí cyklu spočítá součet všech čísel v seznamu.

```py
soucet = 0
for cislo in cisla:
  soucet = soucet + cislo
```

Ne, že bychom zrovna takovýto kus kódu nutně potřebovali, když můžeme použít funkci `sum()`. Tento příklad ale ukazuje, že s cykly můžeme dělat spoustu zajímavých věcí.

@exercises ## Cvičení [

- hratky-s-cykly
- poznavacky
  ]@

## Čtení na doma

Ještě než se přesuneme k hlavnímu tématu, ukážeme si, jak dělat hezčí import funkcí z modulů. Do této chvíle, pokud jsme chtěli použít například funkci `mean` z modulu `statistics`, psali jsme něco jako.

```py
import statistics
prumer = statistics.mean(data)
```

Pokud funkce z tohoto modulu používáme v našem programu často, budeme název `statistics` psát tolikrát, až se upíšeme k smrti. Abychom byli při psaní kódu efektivnější, přejmenujeme si během importu název modulu na něco kratšího, například takto

```py
import statistics as stat
prumer = stat.mean(data)
```

Může se nám také stát, že z nějakého modulu potřebujeme jen některé funkce, například funkce `randint()` a `uniform()` z modulu `random`. V takovém případě můžeme funkce importovat takto

```py
from random import randint, uniform
```

Takto importované funkce pak můžeme používat **bez tečkové notace**

```py
from random import randint, uniform
hod_kostkou = randint(1, 6)
hod_desetinnou_kostkou = uniform(1, 6)
```

### Podmínky s více větvemi

V této lekci jsme si zatím představili pouze podmínky s jednou nebo dvěma větvemi. Když chci něco provést jen v případě, že jsem z písemky dostal více než 90 bodů, napíšu podmínku s jednou větví.

```py
if bodu > 90:
  print('Dobrá práce')
```

Pokud chci něco provést v případě, že podmínka nebyla splněna, použiju podmínku s dvěma větvemi.

```py
if bodu > 90:
  print('Dobrá práce')
else:
  print('Špatná práce')
```

Co kdybych ale například chtěl rozdělit známky podle počtů bodů? Tedy za více než 90 by bylo A, za 80 až 90 B a tak dále. V takovém případě bych mohl použít podmínku s více větvemi.

```py
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
```

Zde je dobré vědět, jakým způsobem Python takovou podmínku vyhodnocuje. Nejdřív se podívá, jestli je splněna první větev. Pokud ano, vykoná příslušný blok kódu a **zbytek větví přeskočí**. Pokud první větev není splněna, zkouší, jestli je splněna druhá. Pokud ano, vykoná příslušný blok a opět zbytek přeskočí. Takto pokračuje dokud nevyčerpá všechny větve nebo nenarazí na `else`. Důležité je tedy zapamatovat si, že pokud výraz v nějaké větvi uspěje, zbytek větví se přeskočí a Python se na ně ani nepodívá.

@exercises ## Doporučené úložky na doma [

- heslo
- prevod-na-usd
- banka
- hadanky
- vzestupny-seznam
  ]@

@exercises ## Volitelné úložky na doma [

- pisemky
- maximum
- druhe-maximum
- k-te-maximum
- ruleta
- prestupny-rok
  ]@

