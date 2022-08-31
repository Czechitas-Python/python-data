## Moduly

Doposud jsme v našich programech měli k dispozici pouze několik základních funkcí. Zatím jsme viděli tyto

`abs`, `round`, `len`, `sum`, `min`, `max`, `sorted`, `int`,
`float`, `str`, `print`.

Později si ukážeme, že jich ještě několik přibude, ale o moc víc jich už k dispozici není. S takto omezeným množstvím funkcí bychom si dlouho nevystačili. Python naštěstí nabízí mnoho takzvaných _modulů_ , které obsahují spousty dalších užitečných funkcí.

Moduly jsou v podstatě balíčky funkcí zaměřených na nějaké konkrétní téma, například statistika, zpracování textu, práce se soubory na disku apod. Pokud chceme používat funkce z nějakého modulu, musíme jej nejdřív takzvaně _importovat_.

Prvním velmi užitečným balíčkem funkcí je modul `math`. Importujeme jej příkazem

```pycon
import math
```

který napíšeme na začátek našeho programu. Pokud pracujeme v Python konzoli, napíšeme tento příkaz prostě na konzoli a dokud ji nezavřeme, můžeme modul používat.

Kromě mnoha jiných obsahuje modul `math` funkce `ceil()` a `floor()`, které zaokrouhlují buď vždy jen dolů nebo jen nahoru. Abychom je mohli zavolat, musíme použít tečkovou notaci.

```pycon
>>> math.ceil(3.1)
4
>>> math.floor(3.7)
3
```

Mnozí z vás už si stěžovali, že Python neobsahuje funkci, která počítá průměr. Nyní takovou funkci můžeme získat, pokud importujeme modul `statistics`. Tento modul obsahuje mimo jiné funkci `mean()`, která počítá vytoužený průměr.

```pycon
>>> import statistics
>>> statistics.mean([1, 2, 3, 4, 5, 6])
3.5
```

### Pozor na názvy skriptů!

**Pozor!** Nikdy nepojmenovávejte svůj skript stejně jako modul, který používáte. Pokud byste pojmenovali svůj skript `math.py`, uvnitř napsali `import math` a používali nějakou funkci z tohoto modulu, Python ji bohužel nenajde. V tu chvíli totiž místo "pravého" modulu `math` naimportoval skript `math.py` ve vašem pracovním adresáři a v něm jistě volanou funkci nemáte definovanou.

Pokud se vám to náhodou stalo a Python vám vypsal něco jako:

```
AttributeError: partially initialized module 'math' has no attribute 'ceil' (most likely due to a circular import)
```

Víte už, čím to je. Přejmenujte váš skript na jiný název a pokud se vám v pracovním adresáři vytvořil adresář `__pycache__`, tak jej také smažte.


### Co vše najdu v modulu

Po naimportování modulu musím vědět jakou funkci z daného modulu chci zavolat. Seznam všech funkcí daného modulu najdeme v [dokumentaci](https://docs.python.org/3/library/math.html) nebo si můžeme nechat od Pythonu poradit.

**Pozor!** Aby vám následující tip fungoval na Windows, je třeba doinstalovat balíček `pyreadline`. To uděláme tak, že v příkazové řádce operačního systému (ne v Pythonu) spustíme příkaz

```shell
pip install pyreadline
```

Po úspěšné instalaci si pak spustíme znovu Python konzoli příkazem `python`, naimportujeme si nějaký modul (např. `math`), napíšeme `math.` a stiskneme tabulátor

```pycon
>>> import math
>>> math.<Tab>
math.acos(       math.erf(        math.isfinite(   math.pi
math.acosh(      math.erfc(       math.isinf(      math.pow(
math.asin(       math.exp(        math.isnan(      math.prod(
math.asinh(      math.expm1(      math.isqrt(      math.radians(
math.atan(       math.fabs(       math.lcm(        math.remainder(
math.atan2(      math.factorial(  math.ldexp(      math.sin(
math.atanh(      math.floor(      math.lgamma(     math.sinh(
math.ceil(       math.fmod(       math.log(        math.sqrt(
math.comb(       math.frexp(      math.log10(      math.tan(
math.copysign(   math.fsum(       math.log1p(      math.tanh(
math.cos(        math.gamma(      math.log2(       math.tau
math.cosh(       math.gcd(        math.modf(       math.trunc(
math.degrees(    math.hypot(      math.nan         math.ulp(
math.dist(       math.inf         math.nextafter(
math.e           math.isclose(    math.perm(
>>> math.
```

Tabulátor je velmi užitečná klávesa, protože umí doplňovat názvy i našich proměnných a funkcí.

## Parametry příkazové řádky

Poslední avšak velmi důležitý modul, jenž si v tuto chvíli představíme, je modul `sys`. Ten obsahuje funkce, které umožňují Pythonu komunikovat s operačním systémem, ve kterém je spuštěný. Nás z tohoto modulu bude zajímat především proměnná (ano, moduly mohou obsahovat kromě funkcí také proměnné) s názvem `argv` Ta nám umožní přistupovat k takzvaným _parametrům příkazové řádky_.

Všechny programy, které jsme zatím společně vytvořili, obsahovaly všechna nezbytná data jaksi natvrdo přímo uvnitř kódu programu. Možná vás napadne, že například program, který má naměřené teploty z minulého týdne zadrátované přímo uvnitř kódu, nám je jen pramálo k užitku. Nemůžeme mu předat nově naměřené teploty jinak, než upravit jeho zdrojový kód. Do skutečně užitečného programu musíme být schopni dostat data jaksi z venku. K tomu máme vícero možností ‒ například nahrát data ze souboru na disku, což se naučíme v příští lekci, můžeme je stáhnout z internetu (také se časem naučíme), ale také je můžeme programu předat přímo na příkazové řádce, když jej spouštíme.

Představme si například program, kterému bychom chtěli předat počet minut a on by nám vypsal v hezkém formátu kolik to dohromady dělá hodin a zbylých minut. Pojmenujme náš program například `cas.py`. Pokud chceme zjistit, jaký čas představuje 325 minut, zavoláme náš program takto:

```pycon
python3 cas.py 325
```

Číslo 325 v tomto příkazu je právě to, čemu říkáme _parametr_. Teď už jen zbývá se k tomuto číslu nějak dostat zevnitř našeho programu.

```py
import sys
celkem = int(sys.argv[1])
hodin = celkem // 60
minut = celkem % 60
print(str(hodin) + ':' + str(minut))
```

To nejdůležitější se děje na druhém řádku, kde používáme hodnotu `sys.argv[1]`. Proměnná `sys.argv` totiž obsahuje seznam všech parametrů, které náš program dostal na příkazovém řádku. Zajímavé je, že tento seznam jako první položku obsahuje samotný název programu. Tedy, pokud bychom si nechali proměnnou `sys.argv` vytisknout na obrazovku, byl by její obsah po spuštění našeho programu

```
['cas.py', '325']
```

Tedy na prvním místě je název programu a na druhém je náš parametr, který jsme prve zadali na příkazové řádce. Všimněte si ovšem, že náš parametr je řetězec. Python totiž všechny parametry na příkazové řádce bere jako řetězce, nehledě na to, jestli jsou to čísla nebo cokoliv jiného. My chceme ale v našem programu čas jako číslo, neboť s ním chceme provádět různá matematická cvičení. Proto musíme náš parametr převést na číslo pomocí již známé funkce `int()`, což právě provádíme na druhém řádku našeho programu.

### Nač se držet při zemi

Zatím jsme na příkazové řádce předali pouze jeden parametr. Nebuďme ale troškaři. Na příkazové řádce si můžeme dovolit předávat zajímavější věci, například celý seznam hodnot. Můžeme kupříkladu napsat program, který spočítá součet všech zadaných hodnot. Pozor ovšem na to, že hodnoty na příkazové řádce jsou vždy řetězce, takže pokud je to potřeba, musíme si je sami převést na čísla.

```py
import sys
cisla = [int(c) for c in sys.argv[1:]]
print('Součet zadaných čísel: ' + str(sum(cisla)))
```

Program poté můžeme volat třeba takto:

```shell
python3 soucet.py 57 41 37 22 12
Součet zadaných čísel: 169
```

Všimněte si, že na druhém řádku našeho programu používáme `sys.argv[1:]`. Je to proto, abychom se zbavili názvu programu, který vždy zabírá první prvek seznamu parametrů. Naše čísla se tedy nacházejí až od prvního indexu nahoru.

## Cvičení: Moduly, parametry řádky
::exc[excs>cas-v-minutach]
::exc[excs>zaokrouhlovani]
::exc[excs>domena-a-url]
::exc[excs>prumer-versus-median]

## Bonusy
::exc[excs>klasicke-zaokrouhlovani]
