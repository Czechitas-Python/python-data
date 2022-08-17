## Povinné čtení na doma

Opět je zde pro vás malá samovzdělávací lekce. Nejdříve se podíváme na to, jak můžeme do chroustání seznamů zapojit podmínky, ukážeme si, jak se generují náhodná čísla a potom si představíme další zajímavou hodnotu.

### Podmínky

Podmínky slouží k tomu, abychom nějaký kus kódu mohli vykonat jen v případě, že je splněna nějaká podmínka. Nejjednodušší použití podmínek najdeme při zpracování seznamů. Mějme například seznam uběhnutých kilometrů a chceme z něj jen nenulové hodnoty.

```pycon
>>> ubehnuto = [12, 0, 4, 5, 0, 6]
>>> [beh for beh in ubehnuto if beh != 0]
[12, 4, 5, 6]
```

Nebo bychom mohli z následujícího seznamu měst chtít pouze názvy těch měst, která mají nad 50 000 obyvatel.

```pycon
>>> mesta = [['Zlín', 76010], ['Jičín', 16792], ['Aš', 13093]]
>>> [mesto[0] for mesto in mesta if mesto[1] > 50000]
['Zlín']
```

### Náhodná čísla

Jeden z velmi zajímavých a užitečných modulů v Pythonu, který jsme na hodině nezmínili, je modul zvaný `random`. Slouží ke generování náhodných čísel a jiných náhodných věcí. Podíváme se na funkce `randint()` a `uniform().`

Funkce `randint(a, b)` generuje náhodná celá čísla ze zadaného intervalu. Můžeme tak simulovat například hody šestistěnnou hrací kostkou:

```pycon
>>> import random
>>> random.randint(1, 6)
4
>>> random.randint(1, 6)
6
>>> random.randint(1, 6)
1
```

Funkce `uniform(a, b)` funguje podobně jako `randint()`, generuje však náhodná <i>desetinná</i> čísla ze zadaného intervalu.

```pycon
>>> random.uniform(1, 6)
3.0445222265782617
>>> random.uniform(1, 6)
3.655355475003799
>>> random.uniform(1, 6)
4.435795489936791
```

Tyto funkce se nám mohou hodit pro generování náhodných dat nebo pro psaní různých her a hříček.

### Rozsahy

Za posledních pár lekcí už jsme se naučili používat pěknou řádku typů hodnot:

- celá čísla
- desetinná čísla
- řetězce
- pravdivostní hodnoty
- seznamy

Nyní nám přibude jedna navíc, která se jmenuje :term{cs="rozsah" en="range"}. Rozsahy slouží k tomu, abychom v Pythonu uměli říct, že chceme všechna čísla z nějakého rozmezí hodnot. Pokud bychom například chtěli všechna čísla mezi 1 a 10, mohli bychom vyrobit seznam

```py
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

To vypadá přímočaře a jednoduše. Ovšem to pouze do chvíle, kdy po vás budu chtít seznam od 1 do 10 000. Pokud byste chtěli takový seznam vyrobit, upíšete se k smrti. Navíc si Python bude muset všechna tato čísla v takovém seznamu pamatovat a to je trochu zbytečné. Když víme, že v seznamu jsou opravdu všechna čísla v zadaném rozmezí, stačí si pamatovat jen krajní hodnoty, tedy 1 a 10 000. A přesně k tomu slouží hodnota typu rozsah.

Chceme-li všechna čísla od 1 do 10, napíšeme prostě

```py
range(1, 11)
```

Pozor na to, že funkce `range()` chápe druhý parametr jako **vyjma** , nikoliv včetně.

Pojďme vyzkoušet, co se stane, když takovýto výraz napíšeme do Python konzole

```pycon
>>> range(1, 11)
range(1, 11)
```

Python nám prostě odpověděl totéž, co jsme napsali, úplně stejně jako kdybychom napsali prostě číslo 50 nebo řetězec `'ahoj'`. Rozsah je prostě hodnota, ve které si Python pamatuje dolní a horní mez a to je všechno. Výhodou rozsahů však je, že je můžeme používat všude tam, kde bychom normálně použili seznam. Pokud nás například zajímá součet hodnot od 1 do 20, můžeme prostě napsat

```pycon
>>> sum(range(1, 21))
210
```

Všimněte si, že jsme takto spočítali součet aniž bychom museli vypisovat všechny hodnoty mezi 1 a 20. Náš nejsilnější kanón je teď samozřejmě chroustání seznamů a ano, i tam můžeme s výhodou použít rozsahy. Pokud bychom například chtěli všechny násobky trojky mezi 1 a 100, stačí napsat

```pycon
>>> [x for x in range(1, 101) if x % 3 == 0]
```

Pokud bychom mermomocí chtěli opravdu všechny hodnoty z rozsahu jako seznam, můžeme jej převést na seznam pomocí funkce `list()`

```pycon
>>> list(range(1, 10))
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

## Doporučené úložky na doma
::exc[excs>minuty]
::exc[excs>fahrnheit-vs-celsius]
::exc[excs>uprava-retezce]
::exc[excs>hazeni-kostkou]
::exc[excs>karty-1]

## Volitelné úložky na doma
::exc[excs>hada-na-velblouda]
::exc[excs>velblouda-na-hada]
