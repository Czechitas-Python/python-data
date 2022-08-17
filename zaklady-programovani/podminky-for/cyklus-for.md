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

## Cvičení: Cyklus FOR
::exc[excs>hratky-s-cykly]
::exc[excs>poznavacky]
