V předchozí kapitole jsme si představili tři důležité typy hodnot: celá čísla,
desetinná čísla a seznamy. Dnes přidáme další důležitý typ hodnot, abychom v
Pythonu mohli pracovat nejen s čísly, ale i s texty.

## Řetězce

Pokud chceme v Pythonu zadat nějak kousek textu, použijeme takzvaný :term{cs="řetězec" en="string"}.
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

Chceme-li vyrobit hezky vypadající čas ve formátu 12:35, použijeme funkci
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

## Cvičení: Řetězce, metody
::exc[excs>prevod-pismen]
::exc[excs>cisla-jako-text]
::exc[excs>cisla-v-textu]

## Bonusy
::exc[excs>chytrejsi-cisla-jako-text]

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
:term{cs="chroustání seznamů" en="list comprehension"}

```pycon
>>> [znamka+1 for znamka in pisemky]
[1, 3, 1, 2, 2, 4]
```

**Poznámka:** Anglický termín _list comprehension_ nemá žádný oficiální český překlad. Čeští programátoři zcela běžně používají tento anglický termín. Je to ale trochu škoda, protože většina programátorských pojmů český ekvivalent má. Proto zde trochu na truc a také pro lehké odlehčení tématu zavádíme název vlastní a uvidíme, kolik absolventek Digitální akademie bude potřeba, aby se uchytil v běžné praxi 😜.

Seznam můžeme zchroustat jakýmkoliv výrazem. Když si například půjdeme v
záchvatu zodpovědnosti zaběhat, abychom vyvážili špatné svědomí z jedení
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

## Cvičení: Chroustání seznamů
::exc[excs>seznamy-cisel]
::exc[excs>seznamy-retezcu]
::exc[excs>seznam-teplot]
::exc[excs>cteni-kodu]

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
