Konzole jazyka Python už nám pomalu přestává stačit na větší a komplikovanější problémy. Potřebovali bychom místo jednoho příkazu spustit příkazů více po sobě a také být schopni si takovou sekvenci příkazů uložit, abychom ji mohli spouštět vícekrát pro různá data. Začneme tedy psát první _programy_.

## Programy

Mějme následující zadání. Spočítejte průměrnou denní teplotu naměřenou za daný týden podle následující tabulky a najděte den, ve který byla teplota nejblíže průměru.

```py
mereni = [
    ['po', 17.3],
    ['út', 16.8],
    ['st', 15.1],
    ['čt', 13.2],
    ['pá', 14.0],
    ['so', 13.9],
    ['ne', 15.8]
]
```

Abychom se dostali k výsledku, budeme s touto tabulkou potřebovat provést několik operací a místo toho, abychom je zadávali do Python konzole jednu po druhé, napíšeme si příkazy jednoduše za sebe do obyčejného textového souboru s příponou `.py`. Pojmenujme jej například `teplota.py`.

```py
mereni = [
    ['po', 17.3],
    ['út', 16.8],
    ['st', 15.1],
    ['čt', 13.2],
    ['pá', 14.0],
    ['so', 13.9],
    ['ne', 15.8]
]
teploty = [radek[1] for radek in mereni]
prumer = sum(teploty)/len(teploty)
rozdily = [abs(t - prumer) for t in teploty]
min_rozdil = min(rozdily)
index = rozdily.index(min_rozdil)
```

Pokud chceme takovýto program spustit, musíme nejdříve náš terminál nasměrovat na složku, ve které máme uložen náš soubor `teploty.py`. Poté napíšeme do terminálu, **pozor, nikoliv do Python konzole** , následující příkaz.

```shell
python teploty.py
```

V případě MacOS nezapomeneme upřesnit Python verze 3

```shell
python3 teploty.py
```

Náš program se sice spustí, ale nevypíše žádný výsledek. To je proto, že když spouštíme programy, Python žádné výsledky sám od sebe nevypisuje. Musíme to provést sami pomocí funkce `print()`. Na konec našeho programu tedy přidáme řádek

```py
print(index)
```

Pokud náš program spustíme znovu, vypíše nám index, na kterém se nachází den s teplotou nejblíže k průměru.

Možná bychom ale chtěli, aby program místo indexu vypsal spíše název dne v týdnu. To zařídíme tak, že poslední řádek změníme na

```py
print(mereni[index][0])
```

Ještě hezčí bude, pokud uživateli sdělíme výsledek nějak přívětivě, například takto:

```py
print('Den s teplotou nejblíž průměru je ' + str(mereni[index][0]))
```

## Cvičení: Programy
::exc[excs>jmeno-a-mesto]
::exc[excs>vyplata-jako-program]
::exc[excs>teploty-jako-program]
