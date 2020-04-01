V předchozí kapitole jsme si představili tři důležité typy hodnot: celá čísla,
desetinná čísla a seznamy. Dnes přidáme další důležitý typ hodnot, abychom v
Pythonu mohli pracovat nejen s čísly, ale i s texty.

## Řetězce

Pokud chceme v Pythonu zadat nějak kousek textu, použijeme takzvaný <term cs="řetězec" en="string">.
Řetězce se v Pythonu uzavírají do jednoduchých nebo dvojitých uvozovek.
Například:

```pycon
>>> 'martin'
>>> '12. března 2018'
>>> "prací prášek"
>>> "Don't panic"
```

Řetězce se chovají v něčem podobně jako čísla a v něčem podobně jako seznamy.
Můžeme je například sčítat

```pycon
>>> jmeno = 'martin' + ' ' + 'podloucký'
```

Můžeme však také přistupovat k jednotlivým písmenům nebo pracovat s
podřetězci.

```pycon
>>> jmeno[3]
't'
>>> jmeno[:6]
'martin'
>>> jmeno[7:]
'podloucký'
```

Podobně jako u seznamů můžeme na řetězcích volat také funkci `len()`

```pycon
>>> len(jmeno)
16
```

Jelikož řetězec je opět hodnota jako každá jiná, není problém vyrobit seznam
řetězců

```pycon
>>> jmena = ['martin', 'jana', 'petr', 'simona']
```

## Převody hodnot

Do této chvíle jsme viděli čtyři typy hodnot: celá čísla, desetinná čísla,
řetězce a seznamy. Je velmi důležité se naučit vždy si dobře uvědomovat
hodnotu jakého typu máme v proměnné zrovna uloženou.

Uvažte proměnnou definovanou takto

```pycon
>>> vek = '18'
```

Všimněte si, že číslo 18 je uzavřeno v uvozovkách. To znamená, že jej Python
chápe jako kus textu, tedy sekvenci symbolů `1` a `8`. Pythonu nezáleží na
tom, jaké symboly používáte uvnitř řetězců, písmenka jsou pro něj totéž jako
číslice. Řetězec `'18'` je pro něj tedy skoro totéž jako `'ahoj'` nebo
`'Petr'`, prostě nějaký kousek textu.

Pokud se tedy pokusíte například o takovýto výpočet

```pycon
>>> vek + 5
```

obdržíte od Pythonu chybu:

```
Traceback (most recent call last):
File "<stdin>", line 1, in
TypeError: Can't convert 'int' object to str implicitly
```

Touto zprávou se nám snaží Python říct, že neví, jak má sečíst řetězec a
číslo. Python umí sečíst dvě čísla nebo dva řetězce, ale sčítat řetězec a
číslo je jako byste po něm chtěli spočítat `'ahoj' + 1`. Takový výpočet nedává
smysl.

### Převod z řetězce na číslo a zpět

S výše uvedeným problémem si můžeme poradit pomocí několika nových funkcí.
První se jmenuje `int()`. Pokud této funkci dáte řetězec, jenž obsahuje celé
číslo, vrátí vám tato funkce hodnotu typu celé číslo.

```pycon
>>> int('18')
18
```

Podobně můžete použít funkci `float()` na řetězce obsahující desetinná čísla.

```pycon
>>> float('3.14')
3.14
```

Často také budeme potřebovat převést nějakou hodnotu na řetězec. K tomu nám
slouží funkce `str()`. Mějme například takového proměnné:

```pycon
>>> hodin = 12
>>> minut = 35
```

Cheme-li vyrobit hezky vypadající čas ve formátu 12:35, použijeme funkci
`str()` takto:

```pycon
>>> str(hodin) + ':' + str(minut)
'12:35'
```

## Metody

V minulé lekci jsme viděli takzvané funkce, které za nás vykonávají často
opakované činnosti jako například zaokrouhlování, zjišťování délky seznamu
apod. Některé funkce se však hodí na práci pouze s jedním typem hodnoty.
Například bychom mohli mít funkci `upper()`, která by převedla všechna písmena
v řetězci na velká písmena. Kdyby taková funkce existovala, mohli bychom ji
volat třeba takto

```pycon
>>> upper('martin')
'MARTIN'
```

Je pochopitelné, že taková funkce funguje pouze pro řetězce. Pro ostatní
hodnoty nedává smysl. Těžko si představit, co by taková funkce měla vrátit
například v takovémto případě:

```pycon
>>> upper(3.14)
```

Funkce, které pracují pouze na jednom typu hodnoty, se programátoři Pythonu
rozhodli svázat přímo s touto hodnotu. Můžeme tedy říct, že funkce `upper()`
patří řetězcům. Pokud tedy máme nějaký řetězec, funkci, která patří pouze k
typu řetězec, zavoláme pomocí takzvané _tečkové notace_.

```pycon
>>> 'martin'.upper()
'MARTIN'
```

Funkcím, které patří jen konkrétním typům hodnot, říkáme _metody_. Všimněte
si, že metoda `upper()` pro řetězce v Pythonu skutečně existuje, takže výše
uvedený kód bude opravdu fungovat. Podobně existuje například metoda
`lower()`. Vyzkoušejte si ji.

### Užitečné metody na řetězcích

`strip()`
: Odstraní všechny bílé znaky na začátku a konci řetězce

```pycon
>>> '  martin   '.strip()
'martin'
```

`split(sep)`
: Rozseká řetězec na kousky podle zadaného oddělovače sep. Např.

```pycon
>>> 'po ut st čt pá'.split(' ')
['po', 'ut', 'st', 'čt', 'pá']
```

nebo

```pycon
>>> '3.12,4.1,9.6,-127,0'.split(',')
['3.12', '4.1', '9.6', '-127', '0']
>>> '3.12,4.1,9.6,-127,0'.split('.')
['3', '12,4', '1,9', '6,-127,0']
```

`join(list)`
: Spojí řetězce v seznamu list do jednoho velkého řetězce podle zadaného separátoru.

```pycon
>>> '+'.join(['1', '2', '3', '4'])
'1+2+3+4'
>>> '/'.join(['dokumenty', 'dapraha', 'python', 'priklady'])
'dokumenty/dapraha/python/priklady'
```

@exercises ## Cvičení - řetězce, metody [

- prevod-pismen
- cisla-jako-text
- cisla-v-textu
  ]@

@exercises bonuses [

- chytrejsi-cisla-jako-text
  ]@

## Chroustání seznamů

Často se může stát, že potřebujeme nějakým způsobem zpracovat všechny hodnoty
v nějakém seznamu a vyrobit tak seznam nový.

Představme si, že zpracováváme známky z písemek, které hodnotili programátoři.
Ti místo známek 1 až 5 používali známky 0 až 4.

```py
pisemky = [0, 2, 0, 1, 1, 3]
```

Z takového zápisu nás bolí hlava, takže chceme známky převést do běžného
formátu, tedy ke každé z nich přičíst jedničku. To provedeme pomocí takzvaného
<term cs="chroustání seznamů" en="list comprehension">

```pycon
>>> [znamka+1 for znamka in pisemky]
[1, 3, 1, 2, 2, 4]
```

**Poznámka:** Anglický termín _list comprehension_ nemá žádný oficiální český překlad. Čeští programátoři zcela běžne používají tento anglický termín. Je to ale trochu škoda, protože většina programátorských pojmů český ekvivalent má. Proto zde trochu na truc a také pro lehké odlehčení tématu zavádíme název vlastní a uvidíme, kolik absolventek Digitální akademie bude potřeba, aby se uchytil v běžné praxi 😜.

Seznam můžeme zchroustat jakýmkoliv výrazem. Když si například půjdeme v
záchvatu zodpovědnosti zaběhat, abychom vyvážili špatné svědomí z jezení
věnečků, můžeme si například takto zaznamenat uběhnuté kilometry v prvních
pěti dnech.

```pycon
>>> kilometry = [2.4, 2.6, 0, 3.5, 1.8]
```

Pokud se pak rozhodneme, že bychom chtěli jen celé kilometry bez desetinných
čísel, napíšeme

```pycon
>>> [round(beh) for beh in kilometry]
```

## Seznamy seznamů

Ještě zajímavější situace nastane, budeme-li chtít zchroustat seznam seznamů.
Minulý týden jsme vyráběli seznam známek ze čtyř písemek pro šest účastníků
kurzu. Mohl by vypadat například takto:

```py
pisemky = [
  [1, 3, 2, 1],
  [3, 1, 1, 2],
  [4, 2, 2, 2],
  [1, 1, 1, 1],
  [1, 2, 2, 1],
  [1, 4, 1, 3]
]
```

Pokud chceme získat dejme tomu všechny známky z první písemky, chceme vlastně
všechny první hodnoty ze všech seznamů uvnitř seznamu pisemky. To můžete
udělat takto:

```pycon
>>> prvni = [znamky[0] for znamky in pisemky]
>>> prvni
[1, 3, 4, 1, 1, 1]
```

## Cvičení

### Seznamy čísel

Mějme zadaný následující seznam

```py
cisla = [1.12, 4.51, 2.64, 13.1, 0.1]
```

Vytvořte seznam, který obsahuje

1. každé z čísel ze seznamu cisla vynásobené dvěma,
2. každé z čísel ze seznamu cisla s opačným znaménkem,
3. každé z čísel ze seznamu cisla umocněné na druhou,
4. každé z čísel ze seznamu cisla jako řetězec.

### Seznamy řetězců

Mějme zadaný následující seznam

```py
jmena = ['Roman', 'Jan', 'Miroslav', 'Petr', 'Gabriel']
```

Vytvořte seznam, který obsahuje

1. počty písmen ve všech jménech,
2. všechna jména napsaná velkými písmeny,
3. všechna jména plus písmeno `'a'` na konci (stanou se z nich tedy ženská jména),
4. všechna jména převedená na malá písmena s koncovkou `'@email.cz'`.

### Seznam teplot

Mějme zadaný následující seznam naměřených teplot. Seznam obsahuje teploty
naměřené pro každý den v týdnu ve čtyřech časech - ráno, v poledne, večer a v
noci.

```py
teploty = [
    [2.1, 5.2, 6.1, -0.1],
    [2.2, 4.8, 5.6, -1.0],
    [3.3, 6.5, 5.9, 1.2],
    [2.9, 5.6, 6.0, 0.0],
    [2.0, 4.6, 5.5, -1.2],
    [1.0, 3.2, 2.1, -2.0],
    [0.4, 2.7, 1.3, -2.8]
]
```

1. Vytvořte seznam průměrných teplot pro každý den.
2. Vytvořte seznam ranních teplot.
3. Vytvořte seznam nočních teplot.
4. Vytvořte seznam dvouprvkových seznamů obsahujících pouze denní a noční teplotu.
5. Spočítejte celkovou průměrnou teplotu za celý týden.

### Čtení kódu

Popište vlastními slovy co následující výrazy udělají se zadaným seznamem
`seznam`. Až když máte ve svojí hlavjénce jasno, tak je zkuste napsat do Python
konzole a ověřte, zda jste měli pravdu.

```py
seznam = [1, 4, 9, 16, 25, 36, 49, 64]
```

1.             [x**0.5 for x in seznam]
1.             [x % 2 for x in seznam]
1.             [[x // 2, x % 2] for x in seznam]

```py
seznam = ['12.03.2014', '10.01.2015', '06.06.1986']
```

4.             [int(datum[3:5]) for datum in seznam]
1.             [int(datum[:2])-1 for datum in seznam]
1.

```py
[
    [int(datum[:2]), int(datum[3:5]), int(datum[6:])] for datum in seznam
]
```

7.             [datum.split('.') for datum in seznam]
1.             ['/'.join(datum.split('.')) for datum in seznam]

## Čtení na doma

Prozatím jsme na svých poutích po krajině Pythonu potkali následující hodnoty:

- Celá čísla: 1, 57, -61, 0, ...
- Desetinná čísla: 1.13, 3.01548, -0.0001, 0.0, ...
- Řetězce: 'Martin', "ahoj", '51', "20.7.2014", ...
- Seznamy: [1, 2, 3], ['po', 'ut', 'st'], ...

Abychom mohli začít dělat opravdu zajímavé věci, budeme potřebovat ještě další
typ hodnoty...

### Pravdivostní hodnoty

Datový typ <term cs="pravdivostní hodnota" en="bool"> slouží k tomu, abychom
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
seznam nebo retězec prvek <i>neobsahuje</i>.

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

## Domácí úkoly ‒ povinné

### Ověřování věku

**Obtížnost: Pohodička**

Následující seznam obsahuje věky uživatelů naší malé sociální sítě.

```py
veky = [35, 12, 44, 11, 18, 21, 28, 18]
```

1. Vytvořte pomocí chroustání seznamů seznam celých čísel, které udávají, kolik jednotlivým uživatelům zbývá do 18ti let. Záporná čísla budou znamenat, že uživatel už věk překročil.
2. Vytvořte pomocí chroustání seznamů seznam pravdivostních hodnot, které udávají, který uživatel je starší 18ti let.
3. Vytvořte pomocí chroustání seznamů seznam pravdivostních hodnot, které udávají, který uživatel má přesně 18 let.

### Promítání

**Obtížnost: To dáš**

V letním kině Šmajchl mají program na každý den uložený jako dva seznamy.
První seznam obsahuje názvy filmů a druhý jejich délky v minutách, např.
takto:

```py
nazvy = [
    'Někdo to rád horké, extended edition',
    'Adéla ještě nevečeřela',
    'Kulový blesk'
]
delky = [136, 105, 82]
```

Použijte chroustání seznamů a vyrobte seznam trvani, který bude obsahovat
délky filmů nikoliv jako čísla v minutách, ale jako řetězce v hodinách a v
minutách. Výsledek tedy bude vypadat takto

```py
trvani = ['2:16', '1:45', '1:22']
```

### Počty obyvatel

**Obtížnost: To dáš**

Mějme počty obyvatel v jednotlivých krajích ČR podle následující tabulky.

| Kraj                 | Počet obyvatel |
| -------------------- | -------------- |
| Hlavní město Praha   | 1 280 508      |
| Jihočeský kraj       | 638 782        |
| Jihomoravský kraj    | 1 178 812      |
| Karlovarský kraj     | 296 749        |
| Kraj Vysočina        | 508 952        |
| Královéhradecký kraj | 550 804        |
| Liberecký kraj       | 440 636        |
| Moravskoslezský kraj | 1 209 879      |
| Olomoucký kraj       | 633 925        |
| Pardubický kraj      | 517 087        |
| Plzeňský kraj        | 578 629        |
| Středočeský kraj     | 1 338 982      |
| Ústecký kraj         | 821 377        |
| Zlínský kraj         | 583 698        |

Tuto tabulku máme reprezentovanou jako seznam:

```py
kraje = [
    ['Hlavní město Praha', '1 280 508'],
    ['Jihočeský kraj', '638 782'],
    ['Jihomoravský kraj', '1 178 812'],
    ['Karlovarský kraj', '296 749'],
    ['Kraj Vysočina', '508 952'],
    ['Královéhradecký kraj', '550 804'],
    ['Liberecký kraj', '440 636'],
    ['Moravskoslezský kraj', '1 209 879'],
    ['Olomoucký kraj', '633 925'],
    ['Pardubický kraj', '517 087'],
    ['Plzeňský kraj', '578 629'],
    ['Středočeský kraj', '1 338 982'],
    ['Ústecký kraj', '821 377'],
    ['Zlínský kraj', '583 698']
]
```

1. Vytvořte seznam, který obsahuje pouze názvy všech krajů, tedy první sloupeček této tabulky.
2. Vytvořte seznam, který obsahuje počty obyvatel jako čísla.
3. Do vhodně pojmenované proměnné uložte seznam, který reprezentuje výše uvedenou tabulku jako dva seznamy: seznam jmen a seznam počtů obyvatel jako čísla.

### Volby

**Obtížnost: Zapni hlavu**

Máme pět kandidátů na post prezidenta ČR. Následující tabulka obsahuje hlasy,
které jednotliví kandidáti získali v prvním kole prezidentských voleb.

| Kraj                 | Igor Rezek | Augustýn Doležal | Vladan Bednář | Ondřej Brotz | Radim Kašpar |
| -------------------- | ---------- | ---------------- | ------------- | ------------ | ------------ |
| Hlavní město Praha   | 78774      | 43179            | 225111        | 144799       | 242854       |
| Jihočeský kraj       | 91062      | 22451            | 17475         | 53391        | 46450        |
| Jihomoravský kraj    | 179186     | 216499           | 4493          | 156305       | 61222        |
| Karlovarský kraj     | 9619       | 53476            | 926           | 64737        | 34566        |
| Kraj Vysočina        | 66904      | 85730            | 27271         | 12964        | 38041        |
| Královéhradecký kraj | 118755     | 1929             | 30426         | 25178        | 31952        |
| Liberecký kraj       | 64467      | 40993            | 81181         | 39392        | 4335         |
| Moravskoslezský kraj | 11221      | 97970            | 26179         | 98539        | 112578       |
| Olomoucký kraj       | 171064     | 7638             | 8752          | 96666        | 39738        |
| Pardubický kraj      | 74235      | 101680           | 18920         | 45904        | 1922         |
| Plzeňský kraj        | 39309      | 1505             | 10531         | 30458        | 40228        |
| Středočeský kraj     | 131584     | 1812             | 241122        | 22267        | 99326        |
| Ústecký kraj         | 194133     | 39985            | 200997        | 28229        | 20780        |
| Zlínský kraj         | 66188      | 51607            | 15977         | 177272       | 17664        |

Data máme k dispozici v následujícím formátu

```py
hlasy = [
    [78774, 43179, 225111, 144799, 242854],
    [91062, 22451, 17475, 53391, 46450],
    [179186, 216499, 4493, 156305, 61222],
    [9619, 53476, 926, 64737, 34566],
    [66904, 85730, 27271, 12964, 38041],
    [118755, 1929, 30426, 25178, 31952],
    [64467, 40993, 81181, 39392, 4335],
    [11221, 97970, 26179, 98539, 112578],
    [171064, 7638, 8752, 96666, 39738],
    [74235, 101680, 18920, 45904, 1922],
    [39309, 1505, 10531, 30458, 40228],
    [131584, 1812, 241122, 22267, 99326],
    [194133, 39985, 200997, 28229, 20780],
    [66188, 51607, 15977, 177272, 17664]
]
```

Zodpovězte následující otázky

1. Kolik získal každý kandidát hlasů v celé ČR?
2. Který kandidát vyhrál první kolo voleb?
3. Ve kterých krajích byla nejvyšší a nejnižší volební účast
4. Vytvořte tabulku, která ukazuje který kandidát vyhrál v kterém kraji.
5. Vytvořte tabulku podobnou té z tohoto cvičení, která místo čísel bude obsahovat jaké procento celkového počtu hlasů získal každý kandidát v daném kraji.

**Nápověda:** postupuje tak, že použijete na každý řádek tabulky zvlášť
chroustání seznamů. Tabulku můžete sestavit tak, že tento postup ručně
zopakujete 13 krát, jednou pro každý kraj. Pokud toužíte po elegantnějším
řešení, vyčkejte na nepovinné úložky.

6. Vytvořte seznam pravdivostních hodnot, který bude říkat, ve kterých krajích překročila volební účast 50 %.

## Domácí úkoly ‒ nepovinné

### Elegantní volby

**Obtížnost: Zavařovačka**

Pokud vás trápí, že řešení varianty e) v úloze o volbách není příliš
elegantní, zkuste sestavit Python výraz na jeden řádek, který celý bod e)
vyřeší najednou. Bude potřeba do sebe zanořit dvě chroustání seznamů, jedno
přes hodnoty v řádcích a druhé přes jednotlivé kraje.
