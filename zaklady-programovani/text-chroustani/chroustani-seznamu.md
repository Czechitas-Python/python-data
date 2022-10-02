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
Zkusme se podívat na seznam známek ze čtyř písemek od šesti účastníků kurzu. Mohl by vypadat například takto:

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
