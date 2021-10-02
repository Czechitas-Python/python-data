V minulé lekci jsme se bavili o tom, jak dostat do našeho programu data pomocí parametrů příkazové řádky. Takový způsob ale brzy narazí na své limity především proto, že na příkazovou řádku se nám vejde jen pár hodnot. Proto dnes přejdeme k druhému způsobu předávání dat do našeho programu a tím je čtení souborů na disku.

## Čtení ze souborů

V praxi často máme data uložena v nějakém souboru na disku v nějakém textovém formátu. Ukážeme si, jak takový soubor v Pythonu otevřít a data z něj přečíst.

Pro naše první experimenty si stáhněte soubor [mereni.txt](assets/mereni.txt). Ten obsahuje naměřené teploty během týdne, které jsme už několikrát v našich programech používali.

Pokud chceme otevřít tento soubor v nějakém našem programu, nejjednodušší je zkopírovat jej do téže složky, ve které máme program uložený. Potom v programu použijeme funkci `open()`, která slouží k otevírání souborů. Náš kód pak může vypadat například takto:

```py
vstup = open('mereni.txt', encoding='utf-8')
radky = [radek for radek in vstup]
vstup.close()
print(radky)
```

Jakmile soubor otevřeme voláním funkce `open()`, proměnná vstup bude obsahovat jednotlivé řádky našeho souboru seřazené jeden za druhým. Není to přímo Python seznam řádků, ale i tak můžeme použít chroustání seznamů a projít soubor řádek po řádku a uložit si tyto řádky do skutečného seznamu. Vzpomeňte si na hodnotu `range`, která také není technicky seznamem, ale můžeme ji chroustat jako by jím byla.

Jakmile jsme se souborem hotovi, musíme ho vždy zavřít voláním metody `close()`. Výstup z našeho programu pak bude vypadat takto:

```py
['po\t17.3\n', 'út\t16.8\n', 'st\t15.1\n', 'čt\t13.2\n', 'pá\t14.0\n', 'so\t13.9\n', 'ne\t15.8\n']
```

Výstupem je skutečně seznam řetězců, které ale obsahují znaky zpětných lomítek. Tato zpětná lomítka slouží k vyjádření speciálních znaků, které by jinak nešly do řetězce vložit. Anglicko/česky se jim říká _escape sekvence_ a my si představíme základní dvě. Nový řádek se píše jako `'\n'`, tabulátor jako `'\t'`. Existuje jich ještě mnoho dalších, ale tyto nám zatím postačí.

Vidíme tedy, že každý náš řádek končí znakem nového řádku a hodnoty na něm jsou odděleny tabulátorem. Pokud bychom chtěli načtené řádky rozdělit na jednotlivé hodnoty, bude náš program vypadat například takto:

```py
vstup = open('mereni.txt', encoding='utf-8')
radky = [radek.split('\t') for radek in vstup]
vstup.close()
radky = [[radek[0], float(radek[1])] for radek in radky]
print(radky)
```

[[[ excs Cvičení: Čtení ze souborů
- vyplata-presneji
- pocet-slov
- pujcovna
]]]

## Zápis do souboru

Když už umíme data ze souboru číst, pojďme se také naučit jak data do souboru zapsat. Konec konců, naše programy budou potřebovat nejen data zpracovávat ale také data produkovat.

Zápis do souboru se provádí pomocí metody `write()`. Ta jako svůj parametr bere řetězec a zapíše jej do toho otevřeného souboru, na kterém ji zavoláme. Abychom ale mohli tuto metodu zavolat, musíme náš soubor otevřít takzvaně pro zápis. K tomu nám poslouží druhý parametr funkce `open()`. Pojďme si to vyzkoušet na příkladu.

Dejme tomu, že máme seznam uživatelů, které chceme zapsat do souboru `uzivatele.txt`.

```py
jmena = ['Roman', 'Jana', 'Radek', 'Petra', 'Vlasta']
soubor = open('uzivatele.txt', 'w', encoding='utf-8')
[soubor.write(jmeno) for jmeno in jmena]
soubor.close()
```

Všimněte si druhého parametru `'w'` při volání funkce `open()`. Díky němu se nám soubor otevře pro zápis. Pokud soubor na disku ještě neexistuje, funkce `open()` jej před otevřením vytvoří. Pokud soubor již existuje, funkce `open()` vymaže před otevřením jeho obsah. Vždy tedy pomocí metody `write()` zapisujeme do prázdného souboru.

Pokud však otevřete soubor, který vytvořil náš předchozí program, uvidíte následující výsledek

```
RomanJanaRadekPetraVlasta
```

Je to proto, že metoda `write()` na rozdíl od funkce `print()` nedělá
automatické odřádkování. Konce řádků tedy do souboru musíme zapsat my.
Upravíme tedy zápis do souboru v našem předchozím programu takto:

```py
[soubor.write(jmeno + '\n') for jmeno in jmena]
```

[[[ excs Cvičení: Zápis do souborů
- rozepsana-vyplata
- hody-kostkou
]]]

[[[ excs Bonus
- dny-v-mesici
]]]

## Povinné čtení na doma

Na lekci jsme si ukazovali, jak číst a zapisovat data z/do textových souborů. Co ale jiné formáty, jako například Excel?

Je důležité si uvědomit, že Excel není datový formát, ani to není synonymum pro tabulku dat. Excel je pouze název programu od firmy Microsoft. Podobně jako se všem náklaďákům začalo říkat tatrovky a vysavačům luxy, začalo se tabulkám s daty říkat excely. Existují ale i jiné programy na práci s tabulkami, například LibreOffice Calc nebo Google Sheets. Microsoft Excel je navíc komerční produkt, který funguje jen na některých operačních systémech, a rozhodně není zadarmo. Ne každý si jej tedy může nebo chce dovolit. Z těchto i jiných důvodů není excelová tabulka vhodný formát pro výměnu dat. Téměř vždy je lepší data z Excelu nebo z jiného tabulkového nástroje před zpracováním exportovat do textového souboru nebo do SQL databáze.

Existují dva základní způsoby, jak převést data z tabulky do textu. My v tomto textu budeme pracovat s Google Sheets, neboť je to nejdostupnější tabulkový editor. Tyto postupy však více či méně fungují i v jiných editorech.

### Hodnoty oddělené tabulátory

První postup je prostě danou tabulku vybrat myší a zkopírovat do textového souboru a ten uložit. V takovém případě nám vzniknou hodnoty, které jsou oddělené pomocí tabulátorů. Z lekce už víme, že není problém takovéto soubory do našeho programu načíst. Podobně, pokud vytvoříme textový soubor tak, že hodnoty na řádku jsou oddělené pomocí tabulátorů, lze je přímo zkopírovat do Google Sheets, které podle tabulátorů vytvoří oddělené sloupečky. Vytvořte si nějakou jednoduchou tabulku v Google Sheets a vyzkoušejte si, že to opravdu funguje oběma směry.

### Formát CSV

Výše uvedený postup funguje pouze pro malé tabulky, protože se vám asi nebude chtít ručně kopírovat tabulku o 100 000 řádcích. Pro výměnu tabulkových dat v textové podobě se ustálil všeobecně používaný formát zvaný _CSV_ z anglického <i>Comma Separated Values</i>. Jak název napovídá, v tomto formátu nejsou hodnoty odděleny tabulátory, nýbrž čárkami. Google Sheets umí tento formát exportovat, nemusíme tedy nic kopírovat. Stačí v menu vybrat <i>Soubor</i> -> <i>Stáhnout jako</i> -> <i>Hodnoty oddělené čárkami</i>. Tím se vám aktuální list stáhne jako textový soubor, který pak můžete normálně otevřít v Python programu. Všimněte si, že takto můžeme dokonce stáhnout i hodnoty oddělené tabulátory (formát <i>TSV</i>).

Pokud chceme provést obrácený postup, tedy nahrát CSV data do tabulky Google, je třeba jít v menu na <i>Soubor</i> -> <i>Importovat</i> -> <i>Nahrát</i> , a poté na vašem počítači vybrat kýžený soubor CSV.

## Nepovinné čtení - kódování textu

V lekci jsme při otvírání souborů používali mysteriózní argument `encoding='utf-8'`. Tímto způsobem Pythonu říkáme, jaké kódování textu náš soubor používá. Ale co je to kurňa kódování textu?

Kódování textu souvisí s tím, jak si počítač data ukládá do paměti. Nyní slovo <i>data</i> používáme v širším kontextu, tedy nejen pro tabulky hodnot, ale také pro všechny ostatní textové soubory, audio, video, programy, prostě úplně cokoliv, co můžete uložit na váš harddisk. Fungování paměti počítače je sice velmi technická věc, ale nám bude stačit, že paměť se skládá z dále nedělitelných buněk, jakýchsi chlívečků, do kterých si počítač může uložit co chce. Technicky se těmto buňkám říká <i>bajty</i>. Potíž je v tom, že jeden bajt (anglicky byte) je velmi malý kousek paměti a navíc se do něj dá uložit pouze číslo, nic jiného. Navíc toto číslo může být pouze z rozmezí 0 až 255.

Pokud tedy chceme do paměti uložit kus textu, počítač si každé písmenko musí interně převést na číslo, a to pak uložit do jedné buňky. Velké písmeno A má například kód 65, vykřičník má kód 33, a tak dále. Anglický text, který má např. 1024 znaků, tak zabere 1024 buněk paměti, nebo-li 1024 bajtů, nebo-li jeden kilobajt.

Právě v převádění znaků na čísla spočívá velký kámen úrazu. V minulosti se totiž technologické firmy a standardizační organizace neshodly na tom, jak na čísla převádět znaky, které nepatří do anglické abecedy. Navíc je problém, že neanglických znaků je víc než 256. Kdyby tak jen šlo o písmenka s čárkami a háčky, ale co třeba azbuka, řečtina a další jazyky. Navíc Číňané nebo Japonci taky mají počítače a chtějí na nich používat svoje brutální abecedy o tisících a tisících znaků. Kódy pro neanglické znaky tedy jistě budou větší než 255, tedy se nám rozhodně nevejdou do jedné buňky a navíc ani není jasné, které znaky má znaková sada vůbec zahrnovat. Vzniklo tak spousta způsobů jak různé znaky kódovat ‒ takzvané znakové sady. V každé znakové sadě má stejné neanglické písmenku různý kód a každé obsahuje jen některé vybrané neanglické znaky. Jedna znaková sada například obsahuje některé české znaky čárkami, ale už neobsahuje háčky, nebo zase obsahuje háčky ale chybí jím 'ř', které má pouze čeština, a tak dále a tak dále.

### Unicode a UTF-8

Není divu, že programátoři měli ze všech těch různých znakových sad za chvíli hlavu jak balón. Postupně tedy dotlačili technologické firmy a organizace k tomu, aby standardizovaly jednu neměnnou znakovou sadu, která bude obsahovat, teď se držte, **úplně všechny znaky z úplně všech jazyků na celé planetě** a každý znak bude mít jasně určený kód. Tomuto standardu se říká Unicode a k dnešnímu dni obsahuje 137 374 znaků včetně čínštiny, cyrilice, smajlíků a různých piktogramů, každý znak se svým unikátním číslem. Díky tomu, že tato webová stránka používá Unicode znakovou sadu, může obsahovat písmenko 'ř', které má číslo 345, znak letadla '✈', který má číslo 9992, nebo znak z hlaholice 'Ⰶ' zvaný <i>živěte</i> s číslem 11270.

Teď ovšem pozor. Unicode ještě není kódování textu, nýbrž pouze znaková sada, tedy jenom seznam znaků a jim přiřazených čísel. Protože kódy pro většinu znaků jsou větší než 255, potřebujeme mít způsob, jak rozdělit takto velká čísla na více bajtů, abychom zároveň šetřili pamětí. Standard Unicode nabízí více možností jak toto provést, z nichž nepoužívanější se jmenuje _UTF-8_.

A proto jsme, milé děti, museli použít při otvírání souborů v Pythonu argument `encoding='utf-8'`. Dnes už je kódování UTF-8 naprostý standard. Používají jej všechny moderní webové stránky, moderní programovací jazyky a textové editory. Bohužel na systému Windows se ještě často setkáte se starým způsobem kódování. Dejte si proto pozor, pod jakým kódováním váš textový soubor ukládáte a vždy vyberte UTF-8. Jinak bude váš textový soubor v Pythonu vypadat jako rozsypaná rýže.

### Všude bordel

Teď už bychom si naivně mohli myslet, že je ve všem pořádek, ale to by byl život příliš snadný. Obzvlášť operační systém Windows umí někdy do věcí kvalitně hodit vidle. Například Poznámkový blok používá jako výchozí nastavení pro ukládání textových souborů kódování ANSI, které je už dávno zastaralé a vůbec nedává smysl ho nadále používat. Pokud si v Poznámkovém bloku při ukládání rozbalíte nabídku kódování, uvidíte tam ale také možnost "kódování Unicode", což je nesmysl, protože Unicode není kódování, nýbrž znaková sada. Standard Unicode nabízí více možných kódování: UTF-8, UTF-16 a UTF-32, které se liší tím, jak moc šetří pamětí. A z nepochopitelných důvodu se občas **kódování** UTF-16 pro **znakovou sadu** Unicode říká **kódování Unicode** i přesto, že téměř všichni používají kódování UTF-8.

Občas programátorům nezbude, než mlátit hlavou do stolu a křičet PROČ? Ale tak je to občas i v životě. Takže nezapomeňte naučit svoje děti, aby vždy ukládaly textové soubory jako UTF-8. Svět pak bude zase o kousek lepším místem.

[[[ excs Doporučené úložky na doma
- pasazeri
- preznamkovani
]]]

[[[ excs Volitelné úložky na doma
- karty-2
- karty-3
]]]
