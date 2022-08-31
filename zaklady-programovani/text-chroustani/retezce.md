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

### Jaké jsou všechny metody řetězců?

**Pozor!** Aby vám následující tip fungoval na Windows, je třeba doinstalovat balíček `pyreadline`. To uděláme tak, že v příkazové řádce operačního systému (ne v Pythonu) spustíme příkaz

```
pip install pyreadline
```

Potom stačí za nějakou naší proměnnou typu `str` napsat tečku a zmáčknout tabulátor.

```pycon
>>> s = ''
>>> s.<Tab>
s.capitalize()    s.isalpha()       s.ljust(          s.rsplit(
s.casefold()      s.isascii()       s.lower()         s.rstrip(
s.center(         s.isdecimal()     s.lstrip(         s.split(
s.count(          s.isdigit()       s.maketrans(      s.splitlines(
s.encode(         s.isidentifier()  s.partition(      s.startswith(
s.endswith(       s.islower()       s.removeprefix(   s.strip(
s.expandtabs(     s.isnumeric()     s.removesuffix(   s.swapcase()
s.find(           s.isprintable()   s.replace(        s.title()
s.format(         s.isspace()       s.rfind(          s.translate(
s.format_map(     s.istitle()       s.rindex(         s.upper()
s.index(          s.isupper()       s.rjust(          s.zfill(
s.isalnum()       s.join(           s.rpartition(
>>> s.
```

## Cvičení: Řetězce, metody
::exc[excs>prevod-pismen]
::exc[excs>cisla-jako-text]
::exc[excs>cisla-v-textu]

## Bonusy
::exc[excs>chytrejsi-cisla-jako-text]
