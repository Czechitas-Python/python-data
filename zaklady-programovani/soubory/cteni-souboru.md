V minulé lekci jsme se bavili o tom, jak dostat do našeho programu data pomocí parametrů příkazové řádky. Takový způsob ale brzy narazí na své limity především proto, že na příkazovou řádku se nám vejde jen pár hodnot. Proto dnes přejdeme k druhému způsobu předávání dat do našeho programu a tím je čtení souborů na disku.

## Čtení ze souborů

V praxi často máme data uložena v nějakém souboru na disku v nějakém textovém formátu. Ukážeme si, jak takový soubor v Pythonu otevřít a data z něj přečíst.

Pro naše první experimenty si stáhněte soubor [mereni.txt](assets/mereni.txt). Ten obsahuje naměřené teploty během týdne, které jsme už několikrát v našich programech používali.

Pokud chceme otevřít tento soubor v nějakém našem programu, nejjednodušší je zkopírovat jej do téže složky, ve které máme program uložený. Potom v programu použijeme funkci `open()`, která slouží k otevírání souborů. Nejčastěji se soubor otevírá v kombinaci se klíčovým slovem `with`. Tím automaticky zajistíme uzavření souboru a nebudeme ho blokovat. Současně si otevřený soubor musíme pojmenovat. Jméno vložíme za další klíčové slovo `as`. Náš soubor `mereni.text` tedy dostal "přezdívku" `vstup`.

Všimni si, že prostřední řádek je odsazený o jedno odsazení vpravo. To není náhoda, tento řádek se totiž nachází v **bloku**. Pomocí bloku říkáme, v jaké části programu chceme pracovat s naším souborem a kdy ho již Python může uzavřít. Mezi řádkem 2 a 3 tedy v tichosti dojde k uzavření souboru. Nám to ale vůbec nevadí, protože obsah souboru máme překopírovaný do seznamu `radky` a ten nám nikam nezmizí.

Na konci úvodního řádku bloku vkládáme dvojtečku. Dvojtečka na konci řádku pak pro nás bude sloužit jako připomenutí, abychom alespoň jeden následující řádek odsadili. Ve stresu z toho ale být nemusíme, protože editor kódu to většinou udělá za nás. Celý obsah souboru uložíme do seznamu `radky` pomocí metody `readlines()`. Ta uloží každý řádek souboru jako jeden prvek seznamu.

Náš kód pak může vypadat například takto:
```py
with open('mereni.txt', encoding='utf-8') as vstup:
    radky = vstup.readlines()
print(radky)
```

Výstup z našeho programu pak bude vypadat takto:

```py
['po\t17.3\n', 'út\t16.8\n', 'st\t15.1\n', 'čt\t13.2\n', 'pá\t14.0\n', 'so\t13.9\n', 'ne\t15.8\n']
```

Výstupem je skutečně seznam řetězců, které ale obsahují znaky zpětných lomítek. Tato zpětná lomítka slouží k vyjádření speciálních znaků, které by jinak nešly do řetězce vložit. Anglicko/česky se jim říká _escape sekvence_ a my si představíme základní dvě. Nový řádek se píše jako `'\n'`, tabulátor jako `'\t'`. Existuje jich ještě mnoho dalších, ale tyto nám zatím postačí.

Vidíme tedy, že každý náš řádek končí znakem nového řádku a hodnoty na něm jsou odděleny tabulátorem. Pokud bychom chtěli načtené řádky rozdělit na jednotlivé hodnoty, bude náš program vypadat například takto:

```py
with open('mereni.txt', encoding='utf-8') as vstup:
    radky = vstup.readlines()

radky = [radek.split('\t') for radek in radky]
radky = [[radek[0], float(radek[1])] for radek in radky]
print(radky)
```

## Cvičení: Čtení ze souborů
::exc[excs>vyplata-presneji]
::exc[excs>pocet-slov]

## Bonus
::exc[excs>pujcovna]
