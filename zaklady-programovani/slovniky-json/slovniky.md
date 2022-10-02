V našich programech budeme často potřebovat pracovat s různě strukturovanými daty, která obsahují mnoho druhů hodnot. Představme si například, že zpracováváme seznam absolventů nějakého kurzu. Každý absolvent má svoje jméno, příjmení (což jsou řetězce), rok absolvování kurzu (celé číslo), výslednou docházku v procentech (desetinné číslo) a informaci o tom, zda prospěl s vyznamenáním (pravdivostní hodnota).

Jelikož už známe seznamy, mohli bychom zkusit reprezentovat absolventa třeba takto:

```py
absolvent = ['Petr', 'Roman', 2017, 0.95, True]
```

Hned ale vidíme, že z takového seznamu není úplně zřejmé, co která hodnota znamená. Musíme si pamatovat, že na indexu 0 je křestní jméno, na indexu 3 docházka apod. Mnohem pohodlnější by bylo, kdybychom mohli jednotlivé hodnoty místo indexování přímo pojmenovat. A přesně k tomuto účelu máme v Pythonu datový typ :term{cs="slovník" en="dictionary"}.

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

## Cvičení: Slovníky
::exc[excs>kurz]
::exc[excs>knihovna]

## Bonusy
::exc[excs>recepty]
