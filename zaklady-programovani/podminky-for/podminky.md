Zatím všechny naše programy vypadaly jako sekvence příkazů vykonávané jeden za druhým. Pro komplikovanější programy ale budeme potřebovat umožnit, aby se některé části programu vykonaly jen za určitých _podmínek_ , nebo se vykonávaly opakovaně v _cyklu_.

## Podmínky pro řízení běhu

V minulých kapitolách už jsme viděli podmínky při chroustání seznamů. Ty v podstatě řídily, které hodnoty se dostanou do našeho výsledného seznamu. Mnohem mocnější nástrojem jsem ovšem podmínky, které dokáží ovlivnit běh samotného programu.

Představte si, že chceme napsat program, který určí, zda je hrací kostka férová či falešná. Program načte experimentální data se souboru do proměnné hody.. Ovšem k tomu, aby náš program fungoval, potřebujeme hodů dostatek. Ze tří hodů kostkou těžko určíme, jestli je nebo není fér. Dejme tomu, že pro spolehlivý výsledek požadujeme alespoň tisíc hodů kostkou. Pokud je hodů málo, můžeme uživateli oznámit, že výsledek není spolehlivý.

```py
import statistics

with open('hody.txt') as vstup:
  hody = vstup.readlines())
hody = [int(hod) for hod in hody]

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

## Cvičení: Podmínky
::exc[excs>deleni]
::exc[excs>kontrola-souboru]

## Bonusy
::exc[excs>maximum-ze-dvou-cisel]
::exc[excs>maximum-ze-tri-cisel]
