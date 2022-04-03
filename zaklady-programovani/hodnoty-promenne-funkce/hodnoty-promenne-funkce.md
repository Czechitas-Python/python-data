V této kapitole si představíme úplné základy programování v Pythonu. Ještě nebudeme psát celé programy, ale budeme zatím Pythonu posílat jednotlivé příkazy a uvidíme, co nám odpoví.

Abychom si mohli s Pythonem povídat, musíme spustit takzvanou _Python konzoli_. To je prostředí, ve kterém můžeme s Pythonem komunikovat a posílat mu příkazy.

Pokud pracujete pod Windows, Python konzoli spustíte tak, že do terminálu napíšete příkaz

```shell
$ py
```

Pokud pracujete na Macu nebo Linuxu, správný příkaz je

```shell
$ python3
```

## Hodnoty

:term{cs="Hodnoty" en="Values"} představují všechny možné druhy dat, se kterými můžou naše programy pracovat. Hodnoty se dle způsobu použití dělí do různých kategorií zvaných :term{cs="datové typy" en="data types"}. Datových typů existuje velké množství. V tuto chvíli si představíme ty nejzákladnější - celá čísla a desetinná čísla.

### Celá čísla

Nejjednodušší datový typ jsou :term{cs="celá čísla" en="integers"}. Pod tento typ patří hodnoty jako 12, 1321500, -5, 0 a podobně. Pokud do Python konzole napíšete hodnotu, Python vám ji vypíše zpátky, což znamená, že vám rozumí 🙂.

```pycon
>>> 127
127
```

### Desetinná čísla

S celými čísly bychom si dlouho nevystačili. Dalším datovým typem tedy budou :term{cs="desetinná čísla" en="floating point numbers"}, např. 13.4, 6.0, -0.0001, 0.0 apod. Pozor, že programátoři vždycky píší desetinná čísla s tečkou, nikoliv s čárkou.

## Aritmetické operátory

Nyní už máme prostředky k tomu, abychom mohli pomocí Pythonu něco spočítat. V Pythonu máme k dispozici běžné aritmetické operátory:

- sčítání: **`+`**
- odčítání: **`-`**
- násobení: **`*`**
- dělení: **`/`**

Díky těmto operátorům můžeme Python použít jako kalkulačku a psát :term{cs="aritmetické výrazy" en="arithmetic expressions"} jako ve škole.

```pycon
>>> 12 * 13 + 10
166
>>> (13.4 - 1.4) / 4
3.0
```

Všimněte si, že můžeme používat kulaté závorky, pokud potřebujeme změnit prioritu operací.

## Proměnné

Při komplikovanějších výpočtech se nám často stane, že si potřebujeme nějaký mezivýpočet uložit pro pozdější použití. K tomu nám slouží takzvané :term{cs="proměnné" en="variables"}. Proměnná je jakási pojmenovaná krabička nebo šuplík, do kterého si můžeme uložit nějakou hodnotu, abychom ji neztratili a mohli ji používat v dalších výpočtech.

Můžeme například v rámci dietního programu spočítat, kolik vanilkových věnečků denně jsme spořádali za posledních 5 dní.

```pycon
>>> celkem = 1 + 2 + 4 + 1 + 6
>>> prumer = celkem / 5
```

### Jména proměnných

Už od úplných začátků s programováním je dobré učit se dobrým návykům, které budou později prospěšné nejen vám, ale hlavně lidem ve vašem okolí. Jedním z takových návyků je správné pojmenovávání proměnných.

1. Název proměnné by neměl začínat velkým písmenem, např. ~~<var>Pocet</var>~~. Takové názvy jsou rezervované pro speciální typy proměnných, ke kterým se v tomto kurzu dostaneme až téměř na konci.
1. Název proměnné by neměl obsahovat diakritiku, např. ~~<var>počet</var>~~. Programovací jazyky vznikaly v anglickém prostředí, kde se diakritika nepoužívá, takže si s ní většina jazyků neporadí.
1. Víceslovné proměnné nesmí obsahovat mezeru, např. ~~<var>pocet hodin</var>~~. To by si Python myslel, že to jsou dvě proměnné za sebou a nevěděl by co s tím. Pokud chcete proměnnou s více slovy, použijte takzvanou :term{cs="velbloudí notaci" en="camel case"} <var>pocetHodin</var> nebo :term{cs="hadí notaci" en="snake case"} <var>pocet_hodin</var>.
1. Vždy proměnnou pojmenujte tak, aby její název jasně napovídal, co se uvnitř ní nachází. Například proměnná <var>pocet_hodin</var> jasně říká, že v ní bude uložen asi nějaký počet hodin. Můžeme podlehnout touze název proměnné zkrátit například na <var>pcthdn</var>, aby se nám lépe psala. Až ovšem někdo další bude takový program číst, bude mlátit hlavou do stolu, cože proboha znamená zkratka <var>pcthdn</var>.
1. Naposledy je dobré si uvědomit, že programy i programátoři se téměř vždy pohybují v mezinárodním prostředí. Takže je vždycky lepší pojmenovávat proměnné anglicky. V tomto kurzu ještě tohle pravidlo trošku rozvolníme, ale i tak si můžete začít zvykat na proměnné s názvem <var>number_of_hours</var>.

### Nástrahy

Dejte pozor na to, že Python není Excel. Do proměnné se jako do šuplíku ukládá pouze hodnota a nikoliv celý výpočet. Pokud tedy napíšeme například

```pycon
>>> sazba = 350
>>> vyplata = 8 * sazba
```

bude v proměnné <var>vyplata</var> uložena hodnota 2800. Jestliže potom změníme hodnotu v proměnné <var>sazba</var> na něco jiného, například

```pycon
>>> sazba = 420
```

v proměnné <var>vyplata</var> bude nadále uložena hodnota 2800. Pokud chceme výsledek výpočtu aktualizovat, musíme jej spustit znova.

```pycon
>>> vyplata = 8 * sazba
```

## Cvičení: Hodnoty, proměnné
::exc[excs>vyplata]


## Funkce

S čísly jsme zatím byli schopní pracovat pouze pomocí aritmetických operátorů. To nám ale brzy nebude stačit a budeme potřebovat složitější operace, kterým říkáme :term{cs="funkce" en="function"}.

Funkce je nějaký komplikovanější výpočet zabalený do jakési krabičky. Této krabičce dáme nějaké jméno, abychom jej mohli používat na různých místech v našem programu.

Dobrým příkladem je funkce `round()`, která pro nás dělá zaokrouhlování. Můžeme tedy psát

```pycon
>>> round(3.4)
3
```

Tomuto zápisu se říká :term{cs="volání funkce" en="function call"}. Když funkci voláme, předáváme jí takzvaný :term{cs="argument" en="argument"}, v našem případě číslo 3.4. Když funkci zavoláme s nějakým argumentem, funkce takzvaně :term{cs="vrátí" en="return"} výsledek.

Funkci si můžeme představit například jako topinkovač. Topinkovač pro nás dělá nějakou užitečnou činnost, kterou chceme často opakovat (opéká topinky). Má svoje jméno (topinkovač). Do topinkovače dáme chleba (argument) a spustíme je (zavoláme). Topinkovač chvíli pracuje a pak nám vrátí výsledek - topinky. Důležité je, že nemusíme řešit jak to topinkovač vlastně dělá, že dokáže opéct chleba. Důležité pro nás je, že to umí a že jej můžeme kdykoliv použít.

::fig[Toaster]{src=assets/toaster.jpg size=50}

## Seznamy

Zatím jsme byli schopní do jedné proměnné uložit pouze jednu hodnotu. Pro práci s daty ale budeme potřebovat pracovat s větším množstvím hodnot než pouze s jednou. K tomu nám poslouží takzvané :term{cs="seznamy" en="lists"}.

Představme si, že si chci zaznamenat počet vanilkových věnečků snědených za posledních 7 dní. V Pythonu si můžu pro tento účel vytvořit seznam, který si uložím do vhodně pojmenované proměnné.

```pycon
>>> venecky = [1, 2, 4, 1, 6, 0, 1]
```

Chceme-li přistoupit k jednotlivým hodnotám uvnitř seznamu, použijeme k tomu hranaté závorky.

```pycon
>>> venecky[0]
1
>>> venecky[4]
6
```

**POZOR!** Programátoři jsou podivné bytosti, které vždy počítají od nuly, nikoliv od jedničky. Proto také první hodnota v našem seznamu má index 0.

Snadno také můžeme některou hodnotu v seznamu změnit. Například když si vzpomeneme, že jsme trošku zalhali ohledně konzumace věnečků v sobotu:

```pycon
>>> venecky[5] = 12
```

Z jednoho seznamu můžeme také získat menší kusy podle zadaných mezí

```pycon
>>> venecky[2:5]
[4, 1, 6]
>>> venecky[:3]
[1, 2, 4]
>>> venecky[3:]
[1, 6, 12, 1]
```

### Vnořené seznamy

Seznam může obsahovat jakékoliv hodnoty, tedy nejen celá čísla. Nezapomeňte, že seznamy jsou také hodnoty, takže jeden seznam může obsahovat jiný seznam jako svůj prvek. Například takto:

```pycon
>>> seznam = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

Rozmyslete si, co vypíšou následující výrazy:

```pycon
>>> seznam[0][1]
>>> seznam[2][0]
>>> seznam[1:][1]
>>> seznam[:1][2]
```

### Užitečné funkce nad seznamy

Pro práci se seznamy se nám může hodit několik funkcí:

`len()`
: Vrátí délku seznamu

`sum()`
: Vrátí součet všech prvků v seznamu

`min()`
: Vrátí nejmenší prvek seznamu

`max()`
: Vrátí největší prvek seznamu

`sorted()`
: Vrátí setříděný seznam

## Cvičení: Seznamy
::exc[excs>pohyby-na-uctu]

## Povinné čtení na doma

Přečtěte si povídání o dalších vymoženostech Pythonu, které se nám nevešly do živé lekce. Cílem je, abyste se postupně učili rozumět textům o programování bez cizí pomoci.

### Další hezké operátory

Během přednášky jsme neprobrali úplně všechny aritmetické operátory, které můžeme v Pythonu použít. Kromě sčítání, odčítání, násobení a dělení máme ještě tyto:

<!-- prettier-ignore -->
- Mocnění: **`**`**
- Celočíselné dělení: **`//`**
- Zbytek po dělení: **`%`**

Mocnění nás zachrání od zdlouhavého opakovaného násobení, tedy místo abychom psali

```pycon
>>> 2*2*2*2*2
32
```

můžeme prostě napsat

```pycon
>>> 2**5
32
```

Pokud si na chvíli vybavíte kruté hodiny matematiky na střední škole, možná si vzpomenete, že mocnění lze použít i k zajímavějším výpočtům. Můžeme například spočítat druhou odmocninu.

```pycon
>>> 16**0.5
4
```

Dalším užitečným operátorem je celočíselné dělení. Dejme tomu, že jsme si dopřáli dlouhou dovolenou, která trvala 33 dní, a chceme spočítat, kolik to bylo celých týdnů. Normální dělení nám vrátí desetinné číslo, takže místo toho použijeme dělení celočíselné.

```pycon
>>> 33 // 7
4
```

Všimněte si, že nám po čtyřech týdnech zbude ještě pár dní. Pokud chceme přesně vědět, kolik dní nám bylo po dělení sedmi, použijeme operátor :term{cs="zbytek" en="division reminder"}.

```pycon
>>> 33 % 7
5
```

## Doporučené úložky na doma
::exc[excs>uroky]
::exc[excs>delka-filmu]
::exc[excs>prumerne-teploty]
::exc[excs>prumer]

## Volitelné úložky na doma
::exc[excs>novy-koberec]
::exc[excs>rozpeti]
::exc[excs>vlastni-min-max]
::exc[excs>stred-seznamu]
::exc[excs>stred-seznamu-2]
