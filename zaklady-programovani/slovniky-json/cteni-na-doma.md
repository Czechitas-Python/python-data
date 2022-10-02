## Povinné čtení na doma

Touto lekcí končí úvodní části kurzu o programování v Pythonu. Před tím, než se vrhneme do další části, si ukážeme poslední třešničku na dortu, která může občas hodně ulehčit práci.

### Formátování řetězců

Často se nám v Pythonu může stát, že potřebujeme vytvořit řetězec, který obsahuje hodnoty z několika různých proměnných. Mějme například seznam útrat, který vypadá takto:

```py
utraty = [
    ['Pavel', 'mléko', 54],
    ['Jana', 'prací prášek', 312],
    ['Robert', 'mouka', 32],
    ['Zuzana', 'vajíčka', 47],
]
```

Představme si, že bychom chtěli každý řádek takové tabulky vypsat takto:

```
Pavel utratil/a 54 kč za mléko.
```

S našimi současnými znalostmi bychom mohli napsat takovýto program

```py
for utrata in utraty:
    print(utrata[0] + ' utratila/a ' + str(utrata[2]) + ' kč za ' + utrata[1] + '.')
```

Takovýto zápis pomocí sčítání řetězců je dost nepohodlný. Pokud by navíc tabulka obsahovala o pár sloupečků více, snadno se nám výraz ve funkci `print()` vymkne z rukou.

Od verze 3.6 jazyk Python obsahuje způsob, jak zápis výše zjednodušit. Pokud těsně před řetězec napíšete písmeno `f` (z anglického <i>format</i> ), můžete do řetězce vložit jakoukoliv proměnnou, pokud ji uzavřete do složených závorek.

Místo zápisu

```py
vyplata = 500000
zprava = 'vaše výplata činí ' + str(vyplata) + ' kč'
```

můžete psát

```py
vyplata = 500000
zprava = f'vaše výplata činí {vyplata} kč'
```

Takovýto zápis je mnohem čitelnější a přehlednější. Všimněte si, že dokonce ani nemusíme hodnotu v proměnné vyplata převádět na řetězec. Python to za nás udělá automaticky. Náš program s útratami by pak s použitím formátování řetězců vypadal takto:

```py
for utrata in utraty:
    print(f'{utrata[0]} utratila/a {utrata[2]} kč za {utrata[1]}.')
```
