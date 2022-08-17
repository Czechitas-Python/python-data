## Povinné čtení na doma

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

## Doporučené úložky na doma
::exc[excs>heslo]
::exc[excs>prevod-na-usd]
::exc[excs>banka]
::exc[excs>hadanky]
::exc[excs>vzestupny-seznam]

## Volitelné úložky na doma
::exc[excs>pisemky]
::exc[excs>maximum]
::exc[excs>druhe-maximum]
::exc[excs>k-te-maximum]
::exc[excs>ruleta]
::exc[excs>prestupny-rok]
