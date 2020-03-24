# Slovníky, JSON

V našich programech budeme často potřebovat pracovat s různě strukturovanými
daty, která obsahují mnoho druhů hodnot. Představme si například, že
zpracováváme seznam absolventů nějakého kurzu. Každý absolvent má svoje jméno,
příjmení (což jsou řetězce), rok absolvování kurzu (celé číslo), výslednou
docházku v procentech (desetinné číslo) a informaci o tom, zda prospěl s
vyznamenáním (pravdivostní hodnota).

Jelikož už známe seznamy, mohli bychom zkusit reprezentovat absolventa třeba
takto:

    
    
    absolvent = ['Petr', 'Roman', 2017, 0.95, True]

Hned ale vidíme, že z takového seznamu není úplně zřejmé, co která hodnota
znamená. Musíme si pamatovat, že na indexu 0 je křestní jméno, na indexu 3
docházka apod. Mnohem pohodlnější by bylo, kdybychom mohli jednotlivé hodnoty
místo indexování přímo pojmenovat. A přesně k tomuto účelu máme v Pythonu
takzvané _slovníky_.

## Slovníky

Slovník umožňuje pojmenovat hodnoty v nějaké datové struktuře tak, abychom
pomocí těchto jmen mohli k hodnotám poté přistupovat. Našeho absolventa bychom
pomocí slovníku reprezentovali takto

    
    
    absolvent = {
      'jmeno': 'Petr',
      'prijmeni': 'Roman',
      'rok': 2017,
      'dochazka': 0.95,
      'vyznamenani': True
    }

Pokud pak chceme získat například jméno či docházku našeho absolventa, píšeme

    
    
    >>> absolvent['jmeno']
    'Petr'
    >>> absolvent['dochazka']
    0.95

První důležitá věc ohledně slovníků je, že slovníky jsou opět hodnoty jako
každé jiné. Mohou proto být součástí seznamů. Můžeme tedy snadno vyrobit
seznam absolventů našeho kurzu:

    
    
    absolventi = [
      {'jmeno': 'Petr', 'prijmeni': 'Roman', 'rok': 2017, 'dochazka': 0.95, 'vyznamenani': True},
      {'jmeno': 'Jana', 'prijmeni': 'Kočanská', 'rok': 2015, 'dochazka': 0.92, 'vyznamenani': True},
      {'jmeno': 'Eva', 'prijmeni': 'Horká', 'rok': 2014, 'dochazka': 0.85, 'vyznamenani': False},
      {'jmeno': 'Ivo', 'prijmeni': 'Roubeník', 'rok': 2017, 'dochazka': 0.75, 'vyznamenani': False}
    ]

Kdybychom pak chtěli získat například příjmení absolventa na indexu 2, psali
bychom

    
    
    >>> absolventi[2]['prijmeni']
    'Horká'

Nebo bychom mohli projít všechny absolventy a spočítat jejich průměrnou
docházku na kurz.

    
    
    >>> from statistics import mean
    >>> mean([ab['dochazka'] for ab in absolventi])
    0.8765

### Složitější struktury

Stejně jako u proměnných a seznamů můžeme do slovníku uložit jakoukoliv
hodnotu. Není tedy problém mít ve slovníku seznam nebo další slovník. Tím se
otvírá prostor pro mnohem komplikovanější datové struktury. Takto bychom mohli
reprezentovat například kurz Czechitas jménem Úvod do programování.

    
    
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

Všimněte si, jak slovník představující jeden kurz, obsahuje pod klíčem
`konani` seznam dalších slovníků. Každý z nich reprezentuje jedno konání kurzu
a dále obsahuje například seznam koučů atd. Kdybychom tedy například chtěli
seznam všech koučů na druhém konání kurzu, napsali bychom

    
    
    kurz['konani'][1]['koucove']

## Cvičení

### Kurz

Založte si program v Pythonu a zkopírujte si do něj datovou strukturu kurzu
Úvod do programování z lekce výše.

  1. Vypište na výstup počet účastnic na posledním konání kurzu.
  2. Vypište na výstup jméno posledního kouče na prvním konání kurzu.
  3. Vypište na výstup celkový počet konání kurzu.
  4. Vypište na výstup všechna místa, na kterých se kurz konal. Použijte chroustání seznamů.

### Knihovna

Uvažte, jak byste pomocí slovníku reprezentovali údaje o knize v knihovně.
Jaké klíče a hodnoty ve slovníku budou? Zcela jistě bude každá kniha obsahovat
například název. Chtěli bychom také, aby kniha umožňovala mít vícero autorů a
vícero vydání. Ve vašem programu vytvořte proměnnou, který bude obsahovat
jednu knihu s vámi vymyšlenou strukturou.

Hotovo!

Hurá, pokud jste dorazili až sem, máte hotovo. Nalepte si lísteček a pokud
chcete, můžete pokračovat bonusovými příklady.

## Bonusy

### Recepty

Prohlédněte na následujicí reprezentaci receptu:

    
    
    {
      'nazev': 'Batáty se šalvějí a pancettou',
      'narocnost': 'stredni',
      'doba': 30,
      'ingredience': [
        ['batát', '1', '15 kč'],
        ['olivový olej', '2 lžíce', '2 kč'],
        ['pancetta', '4-6 plátků', '21 kč'],
        ['přepuštěné máslo', '2 lžíce', '5 kč'],
        ['mletý černý pepř', '1/2 lžičky', '0.5 kč'],
        ['sůl', '1/2 lžičky', '0.1 kč'],
        ['muškátový oříšek', 'špetka', '1 kč'],
        ['česnek', '2 stroužky', '1 kč'],
        ['šalvějové lístky', '20-25', '12 kč']
      ]
    }

Uložte si tuto strukturu do proměnné recept na začátek nového programu.
Vypište pomocí funkce `print` kolik bude celé jídlo stát korun zaokrouhlené na
celé koruny nahoru.

## Formát JSON

JSON je formát pomocí kterého můžeme zapsat strukturovaná data jako čistý
text. S jedním takovým datovým formátem jste se již potkali, jmenuje se CSV.

JSON formát původně pochází z jazyka, který se jmenuje JavaScript. Ten se
hodně používá pro tvorbu webových stránek a jelikož výměna dat nejčastěji
probíhá po internetu, ujal se formát JSON všeobecně jako standard pro výměnu
dat mezi programy. Výhoda pro nás je, že JSON vypadá téměř stejně jako Python
slovníky. Liší se pouze tím, že vždy používá dvojité uvozovky a hodnoty `True`
a `False` se píší s malým písmenem, tedy `true` a `false`. Náš absolvent kurzu
z úvody lekce by tedy ve formátu JSON vypadal takto:

    
    
    {"jmeno": "Petr", "prijmeni": "Roman", "rok": 2017, "dochazka": 0.95, "vyznamenani": true}

### Čtení JSON dat

V Pythonu je velice jednoduché převést JSON na obyčejný Python slovník. Stačí
nám k tomu modul jménem `json`. Vyzkoušíme si to na našem seznamu absolventů.
Nejdřív si tato data stáhneme jako soubor [absolventi.json](/download/python-
data/absolventi.json). Ten pak můžeme v Pythonu otevřít a převést na JSON
následujicím programem.

    
    
    import json
    soubor = open('absolventi.json', encoding='utf-8')
    text = soubor.read()
    soubor.close()
    absolventi = json.loads(text)
    print(absolventi)

V tomto programu používáme metodu `read`, která umí celý soubor načíst se vším
všudy do jednoho velkého řetězce. Tento řetězec pak můžeme předat funkci
`loads` z modulu `json`, která tento řetězec přečte a pokud jsou v něm data ve
formátu JSON, převede je na Python slovníky.

Pokud bychom se nechtěli sami obtěžovat se čtením souboru, můžeme použít
metodu `load`, která umí přečíst JSON přímo z otevřeného souboru.

    
    
    import json
    soubor = open('absolventi.json', encoding='utf-8')
    absolventi = json.load(soubor)
    soubor.close()
    print(absolventi)

Pokud se ptáte k čemu je nám vůbec funkce `loads`, když můžeme rovnou použít
funkci `load`, vydržte do další části této lekce, kde budeme stahovat JSON z
internetu. Ten nám totiž vždy přijde jako textový řetězec.

### Zápis JSON dat

Zápis JSON dat do souboru je podobně jednoduché jako čtení. Stačí si osvojit
funkci `dump`. Dejme tomu, že máme jednoduchý JSON, který obsahuje například
odpracované hodiny pro každý den v týdnu. Ten chceme zapsat do textového
souboru.

    
    
    import json
    hodiny = {'po': 8, 'ut': 7, 'st': 6, 'ct': 7, 'pa': 8}
    soubor = open('hodiny.json', 'w', encoding='utf-8')
    json.dump(hodiny, soubor)
    soubor.close()
    

Pokud bychom z nějakého důvodu chtěli pouze vytvořit řetězec obsahující JSON
ale nezapisovat jej do souboru, můžeme použít funkci `json.dumps`.

    
    
    >>> hodiny = {'po': 8, 'ut': 7, 'st': 6, 'ct': 7, 'pa': 8}
    >>> import json
    >>> json.dumps(hodiny)
    '{"po": 8, "ut": 7, "st": 6, "ct": 7, "pa": 8}'

### Stahování dat z internetu

V předchozím příkladu jsem naše data načetli ze soubrou na disku. Pokud však
narazíte na vstřícného poskytovatele dat, je možné si data stáhnout z
takzvaného API (Applicattion Programming Interface) přímo z internetu. Zkratka
API se používá jako označení nějakého přípojného bodu na internetu, odkud si
můžete stáhnout data v nějakém strojově čitelném formátu. Nejčastěji je tímto
formátem právě JSON.

Malá potíž je ovšem v tom, že Python sám o sobě neobsahuje modul pro stahování
dat z internetu. Musíme proto do našeho Pythonu doinstalovat takzvaný externí
balíček.

## Externí moduly a balíčky

Python sám o sobě obsahuje mnoho užitečných modulů pro řešení různých typů
úloh. Už jsme viděli modul `random` pro práci s náhodnými čísly, modul
`statistics` pro základní statistické funkce nebo modul `sys` pro práci s
operačním systémem. Všem modulům, které jsou součástí základní instalace
Pythonu, se dohromady říká _standardní knihovna_. Přehled všech modulů, které
standardní knihovna obsahuje můžete najít [v Python
dokumentaci](https://docs.python.org/3/library/).

Čas od času ale v Pythonu potřebujeme vykonat nějakou činnost, pro kterou není
ve standardní knihovně dostupný žádný modul, například stáhnou data z
internetu. V takovém případě budeme muset z internetu stáhnout a naistalovat
takzvaný _balíček_. Balíčky obsahují moduly, které po instalaci balíčku můžeme
importovat v našem programu.

Ke stahování dat z intertnetu potřebujete balíček jménem `requests`.
Nainstalujeme jej příkazem

    
    
    $ pip3 install requests

Pozor, že ve Windows tento příkaz vypadá takto.

    
    
    $ pip install requests

Může se stát, že výše uvedený příkaz nebude fungovat protože nemáte
nainstalovaný správce balíčků `pip`\- V takovém případě bude potřeba znova
spustit instalaci Pythonu a během ní zaškrtnout, že chcete nainstalovat také
`pip`.

## Stahování dat z API

Jeden ze cvičných zdrojů dat najdeme na adrese `http://api.kodim.cz/python-
data/people`. Naším jediným cílem je data získat jako text. Pak už jej
převedeme na Python slovníky právě s využítím výše zmiňované funkce `loads`.

    
    
    import requests
    import json
    response = requests.get('http://api.kodim.cz/python-data/people')
    data = json.loads(response.text)
    print(data)
    

## Cvičení

### Seznam lidí

Jak už jsme si ověřili v lekci, datové API na adrese
`http://api.kodim.cz/python-data/people` obsahuje seznam lidí. Napište
program, který tento seznam z API stáhne a převede z formátu JSON na Python
slovníky. Proveďte následující úkoly.

  1. Zjistěte kolik lidí celkem seznam obsahuje.
  2. Zjistěte jaké všechny informace máme o jednotlivých osobách.
  3. Zjistěte, kolik je v souboru mužů a žen.

### Svátky

Na adrese `http://svatky.adresa.info/json` najdete API, které vám odpoví, kdo
má dneska svátek.

  1. Využijte toto API k tomu, abyste napsali program, který po spuštění vypíše na obrazovku kdo má dneska svátek.
  2. Pokud použijete adresu `http://svatky.adresa.info/json?date=DDMM`, kde místo DDMM doplníte datum, dostanete jméno, které má svátek v zadaný den. Formát DDMM znamená že 6. ledna bude zapsáno jako 0601, 12. září jako 1209 apod. Napište program, který dostane na příkazové řádce číslo dne a číslo měsíce a vypíše na výstup kdo má v daný den svátek. Použijte váš program abyste zjistili, kdo má svátek 29. února.

## Čtení na doma

Touto lekcí končí úvodní části kurzu o programování v Pythonu. Před tím, než
se vrhneme do další části, si ukážeme poslední třešničku na dortu, která může
občas hodně ulehčit práci.

### Formátování řetězců

Často se nám v Pythonu může stát, že potřebujeme vytvořit řetězec, který
obsahuje hodnoty z několika různých proměnných. Mějme například seznam útrat,
který vypadá takto:

    
    
    utraty = [
      ['Pavel', 'mléko', 54],
      ['Jana', 'prací prášek', 312],
      ['Robert', 'mouka', 32],
      ['Zuzana', 'vajíčka', 47],
    ]
    

Představme si, že bychom chtěli každý řádek takové tabulky vypsat takto:

    
    
      Pavel utratil/a 54 kč za mléko.
    

S našimi současnými znalostmi bychom mohli napsat takovýto program

    
    
    for utrata in utraty:
      print(utrata[0] + ' utratila/a ' + str(utrata[2]) + ' kč za ' + utrata[1] + '.')  
    

Takovýto zápis pomocí sčítání řetězců je dost nepohodlný. Pokud by navíc
tabulka obsahovala o pár sloupečků více, snadno se nám výraz v metodě `print`
vymkne z rukou.

Od verze 3.6 jazyk Python obsahuje způsob, jak zápis výše zjednodušit. Pokud
těsně před řetězec napíšete písmeno f (z anglického _format_ ), můžete do
řetězce vložit jakoukoliv proměnnou, pokud ji uzavřete do složených závorek.

Místo zápisu

    
    
    vyplata = 500000
    zprava = 'vaše výplata činí ' + str(vyplata) + ' kč'
    

můžete psát

    
    
    vyplata = 500000
    zprava = f'vaše výplata činí {vyplata} kč'
    

Takovýto zápis je mnohem čitelnější a přehlednější. Všimněte si, že dokonce
ani nemusíme hodnotu v proměnné vyplata převádět na řetězec. Python to za nás
udělá automaticky. Náš program s útratami by pak s použitím formátování
řetězců vypadal takto:

    
    
    for utrata in utraty:
      print(f'{utrata[0]} utratila/a {utrata[2]} kč za {utrata[1]}.')
    

