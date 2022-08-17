## Povinné čtení na doma

Prozatím jsme na svých poutích po krajině Pythonu potkali následující hodnoty:

- Celá čísla: 1, 57, -61, 0, ...
- Desetinná čísla: 1.13, 3.01548, -0.0001, 0.0, ...
- Řetězce: 'Martin', "ahoj", '51', "20.7.2014", ...
- Seznamy: [1, 2, 3], ['po', 'ut', 'st'], ...

Abychom mohli začít dělat opravdu zajímavé věci, budeme potřebovat ještě další
typ hodnoty...

### Pravdivostní hodnoty

Datový typ :term{cs="pravdivostní hodnota" en="bool"} slouží k tomu, abychom
mohli v našem programu vyjádřit, zda je něco pravda či nepravda. Proto nám
pro tento typ stačí pouze dvě hodnoty: `True` (pravda) a `False` (nepravda).
Pravdivostní hodnoty jsou opět hodnoty jako každé jiné. Můžeme je tady
ukládat do proměnných

```py
vysledek = False
```

nebo je používat v seznamech. Zkusme například vyjádřit, který den v týdnu je
pracovní.

```py
[True, True, True, True, True, False, False]
```

Mnoho užitečných operátorů v Pythonu vrací právě pravdivostní hodnoty.
Například operátor `in`, vrátí `True`, pokud se daný prvek nachází uvnitř
seznamu nebo řetězce.

```pycon
>>> 3 in [1, 2, 3]
True
>>> 4 in [1, 2, 3]
False
>>> 'r' in 'Martin'
True
>>> 'x' in 'Martin'
False
```

Existuje také obrácený operátor `not in`, který vrací `True`, pokud daný
seznam nebo řetězec prvek <i>neobsahuje</i>.

```pycon
>>> 3 not in [1, 2, 3]
False
>>> 4 not in [1, 2, 3]
True
```

Velmi užitečné jsou také následující porovnávací operátory

- `>` větší než
- `>=` větší nebo rovno
- `<` menší než
- `<=` menší nebo rovno
- `==` rovno
- `!=` nerovno

Můžeme se tedy ptát například takto

```pycon
>>> 4 > 3
True
>>> 4 < 3
False
```

Takovéto otázky jsou dost zbytečné, protože odpověď již známe předem. Pokud
ovšem použijeme proměnné a funkce, můžeme se ptát na zajímavější věci.

```pycon
>>> vek >= 18
```

Výsledek bude `True` pokud proměnná věk obsahuje hodnotu větší nebo rovnu 18.

```pycon
>>> jmeno == 'Martin'
```

Výsledek `True`, pokud proměnná jmeno obsahuje hodnotu `'Martin'`.

```pycon
>>> len(seznam) != 4
```

Výsledek `True`, pokud je délka seznamu různá od 4.

## Doporučené úložky na doma
::exc[excs>overovani-veku]
::exc[excs>promitani]
::exc[excs>pocty-obyvatel]
::exc[excs>volby]

## Volitelné úložky na doma
::exc[excs>elegantni-volby]
