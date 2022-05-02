V našich programech budeme často potřebovat pracovat s různě strukturovanými daty, která obsahují mnoho druhů hodnot. Představme si například, že zpracováváme seznam absolventů nějakého kurzu. Každý absolvent má svoje jméno, příjmení (což jsou řetězce), rok absolvování kurzu (celé číslo), výslednou docházku v procentech (desetinné číslo) a informaci o tom, zda prospěl s vyznamenáním (pravdivostní hodnota).

Jelikož už známe seznamy, mohli bychom zkusit reprezentovat absolventa třeba takto:

```py
absolvent = ['Petr', 'Roman', 2017, 0.95, True]
```

Hned ale vidíme, že z takového seznamu není úplně zřejmé, co která hodnota znamená. Musíme si pamatovat, že na indexu 0 je křestní jméno, na indexu 3 docházka apod. Mnohem pohodlnější by bylo, kdybychom mohli jednotlivé hodnoty místo indexování přímo pojmenovat. A přesně k tomuto účelu máme v Pythonu datový typ <term cs="slovník" en="dictionary">.

## Slovníky

Slovník umožňuje pojmenovat hodnoty v nějaké datové struktuře tak, abychom pomocí těchto jmen mohli k hodnotám poté přistupovat. Našeho absolventa bychom pomocí slovníku reprezentovali takto

```py
absolvent = {
  'jmeno': 'Petr',
  'prijmeni': 'Roman',
  'rok': 2017,
  'dochazka': 0.95,
  'vyznamenani': True
}
```

Pokud pak chceme získat například jméno či docházku našeho absolventa, píšeme

```pycon
>>> absolvent['jmeno']
'Petr'
>>> absolvent['dochazka']
0.95
```

První důležitá věc ohledně slovníků je, že slovníky jsou opět hodnoty jako každé jiné. Mohou proto být součástí seznamů. Můžeme tedy snadno vyrobit seznam absolventů našeho kurzu:

```py
absolventi = [
  {'jmeno': 'Petr', 'prijmeni': 'Roman', 'rok': 2017, 'dochazka': 0.95, 'vyznamenani': True},
  {'jmeno': 'Jana', 'prijmeni': 'Kočanská', 'rok': 2015, 'dochazka': 0.92, 'vyznamenani': True},
  {'jmeno': 'Eva', 'prijmeni': 'Horká', 'rok': 2014, 'dochazka': 0.85, 'vyznamenani': False},
  {'jmeno': 'Ivo', 'prijmeni': 'Roubeník', 'rok': 2017, 'dochazka': 0.75, 'vyznamenani': False}
]
```

Kdybychom pak chtěli získat například příjmení absolventa na indexu 2, psali bychom

```pycon
>>> absolventi[2]['prijmeni']
'Horká'
```

Nebo bychom mohli projít všechny absolventy a spočítat jejich průměrnou docházku na kurz.

```pycon
>>> from statistics import mean
>>> mean([ab['dochazka'] for ab in absolventi])
0.8765
```

### Složitější struktury

Stejně jako u proměnných a seznamů můžeme do slovníku uložit jakoukoliv hodnotu. Není tedy problém mít ve slovníku seznam nebo další slovník. Tím se otvírá prostor pro mnohem komplikovanější datové struktury. Takto bychom mohli reprezentovat například kurz Czechitas jménem Úvod do programování.

```py
kurz = {
  'nazev': 'Úvod do programování',
  'lektor': 'Martin Podloucký',
  'konani': [
    {
      'misto': 'T-Mobile',
      'koucove': [
        'Dan Vrátil',
        'Filip Kopecký',
        'Martina Nemčoková'
      ],
      'ucastnic': 30
    },
    {
      'misto': 'MSD IT',
      'koucove': [
        'Dan Vrátil',
        'Zuzana Tučková',
        'Martina Nemčoková'
      ],
      'ucastnic': 25
    },
    {
      'misto': 'Škoda DigiLab',
      'koucove': [
        'Dan Vrátil',
        'Filip Kopecký',
        'Kateřina Kalášková'
      ],
      'ucastnic': 41
    }
  ]
}
```

Všimněte si, jak slovník představující jeden kurz, obsahuje pod klíčem `konani` seznam dalších slovníků. Každý z nich reprezentuje jedno konání kurzu a dále obsahuje například seznam koučů atd. Kdybychom tedy například chtěli seznam všech koučů na druhém konání kurzu, napsali bychom

```py
kurz['konani'][1]['koucove']
```

[[[ excs Cvičení: Slovníky
- kurz
- knihovna
]]]

[[[ excs Bonusy
- recepty
]]]

## Formát JSON

JSON je formát pomocí kterého můžeme zapsat strukturovaná data jako čistý text. S jedním takovým datovým formátem jste se již potkali, jmenuje se CSV.

JSON formát původně pochází z jazyka, který se jmenuje JavaScript. Ten se hodně používá pro tvorbu webových stránek a jelikož výměna dat nejčastěji probíhá po internetu, ujal se formát JSON všeobecně jako standard pro výměnu dat mezi programy. Výhoda pro nás je, že JSON vypadá téměř stejně jako Python slovníky. Liší se pouze tím, že vždy používá dvojité uvozovky a hodnoty `True` a `False` se píší s malým písmenem, tedy `true` a `false`. Náš absolvent kurzu z úvody lekce by tedy ve formátu JSON vypadal takto:

```json
{
  "jmeno": "Petr",
  "prijmeni": "Roman",
  "rok": 2017,
  "dochazka": 0.95,
  "vyznamenani": true
}
```

### Čtení JSON dat

V Pythonu je velice jednoduché převést JSON na obyčejný Python slovník. Stačí nám k tomu modul jménem `json`. Vyzkoušíme si to na našem seznamu absolventů. Nejdřív si tato data stáhneme jako soubor [absolventi.json](assets/absolventi.json). Ten pak můžeme v Pythonu otevřít a převést na JSON následujícím programem.

```py
import json
with open('absolventi.json', encoding='utf-8') as soubor:
  text = soubor.read()
absolventi = json.loads(text)
print(absolventi)
```

V tomto programu používáme metodu `read`, která umí celý soubor načíst se vším všudy do jednoho velkého řetězce. Tento řetězec pak můžeme předat funkci `loads` z modulu `json`, která tento řetězec přečte a pokud jsou v něm data ve formátu JSON, převede je na Python slovníky.

Pokud bychom se nechtěli sami obtěžovat se čtením souboru, můžeme použít metodu `load`, která umí přečíst JSON přímo z otevřeného souboru.

```py
import json
with open('absolventi.json', encoding='utf-8') as soubor:
  absolventi = json.load(soubor)
print(absolventi)
```

Pokud se ptáte k čemu je nám vůbec funkce `loads`, když můžeme rovnou použít funkci `load`, vydržte do další části této lekce, kde budeme stahovat JSON z internetu. Ten nám totiž vždy přijde jako textový řetězec.

### Zápis JSON dat

Zápis JSON dat do souboru je podobně jednoduché jako čtení. Stačí si osvojit funkci `dump`. Dejme tomu, že máme jednoduchý JSON, který obsahuje například odpracované hodiny pro každý den v týdnu. Ten chceme zapsat do textového souboru.

```py
import json
hodiny = {'po': 8, 'ut': 7, 'st': 6, 'ct': 7, 'pa': 8}
with open('hodiny.json', mode='w', encoding='utf-8') as soubor:
  json.dump(hodiny, soubor)
```

Pokud bychom z nějakého důvodu chtěli pouze vytvořit řetězec obsahující JSON ale nezapisovat jej do souboru, můžeme použít funkci `json.dumps`.

```pycon
>>> hodiny = {'po': 8, 'ut': 7, 'st': 6, 'ct': 7, 'pa': 8}
>>> import json
>>> json.dumps(hodiny)
'{"po": 8, "ut": 7, "st": 6, "ct": 7, "pa": 8}'
```

### Stahování dat z internetu

V předchozím příkladu jsem naše data načetli ze souboru na disku. Pokud však narazíte na vstřícného poskytovatele dat, je možné si data stáhnout z takzvaného API (Application Programming Interface) přímo z internetu. Zkratka API se používá jako označení nějakého přípojného bodu na internetu, odkud si můžete stáhnout data v nějakém strojově čitelném formátu. Nejčastěji je tímto formátem právě JSON.

Malá potíž je ovšem v tom, že Python sám o sobě neobsahuje modul pro stahování dat z internetu. Musíme proto do našeho Pythonu doinstalovat takzvaný externí balíček.

## Externí moduly a balíčky

Python sám o sobě obsahuje mnoho užitečných modulů pro řešení různých typů úloh. Už jsme viděli modul `random` pro práci s náhodnými čísly, modul `statistics` pro základní statistické funkce nebo modul `sys` pro práci s operačním systémem. Všem modulům, které jsou součástí základní instalace Pythonu, se dohromady říká <term cs="standardní knihovna" en="standard library">. Přehled všech modulů, které standardní knihovna obsahuje můžete najít [v Python dokumentaci](https://docs.python.org/3/library/).

Čas od času ale v Pythonu potřebujeme vykonat nějakou činnost, pro kterou není ve standardní knihovně dostupný žádný modul, například stáhnou data z internetu. V takovém případě budeme muset z internetu stáhnout a nainstalovat takzvaný <term cs="balíček" en="package">.

Balíčky obsahují moduly, které po instalaci balíčku můžeme importovat v našem programu.

Ke stahování dat z internetu potřebujete balíček jménem `requests`. Nainstalujeme jej příkazem

```shell
pip3 install requests
```

Pozor, že ve Windows tento příkaz vypadá takto.

```shell
pip install requests
```

Může se stát, že výše uvedený příkaz nebude fungovat protože nemáte nainstalovaný správce balíčků `pip`\- V takovém případě bude potřeba znova spustit instalaci Pythonu a během ní zaškrtnout, že chcete nainstalovat také `pip`.

## Stahování dat z API

Jeden ze cvičných zdrojů dat najdeme na adrese `http://api.kodim.cz/python-data/people`. Naším jediným cílem je data získat jako text. Pak už jej převedeme na Python slovníky právě s využitím výše zmiňované funkce `loads`.

```py
import requests
import json
response = requests.get('http://api.kodim.cz/python-data/people')
data = json.loads(response.text)
print(data)
```

[[[ excs Cvičení: API a JSON
- seznam-lidi
- svatky
]]]

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
