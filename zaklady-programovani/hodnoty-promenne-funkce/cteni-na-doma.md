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
::exc[excs>delka-filmu]
::exc[excs>prumerne-teploty]
::exc[excs>prumer]

## Volitelné úložky na doma
::exc[excs>novy-koberec]
::exc[excs>rozpeti]
::exc[excs>vlastni-min-max]
::exc[excs>stred-seznamu]
::exc[excs>stred-seznamu-2]
