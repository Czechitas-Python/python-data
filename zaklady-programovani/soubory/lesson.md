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

## Cvičení

### Výplata přesněji

Zatím jsme výplatu počítali za předpokladu, že každý měsíc odpracujeme stejný počet hodin, což není příliš realistické. Vytvořte proto textový soubor `vykaz.txt`, který bude obsahovat 12 řádků a na každém řádku počet odpracovaných hodin za každý měsíc za poslední rok.

1. Otevřete tento soubor ve svém programu a načtěte hodnoty na řádcích do seznamu `vykaz`. Vytiskněte tento seznam na konzoli funkcí `print()` abyste si ověřili, že jste soubor načetli správně.
1. Nechte uživatele zadat na příkazovém řádku hodinovou mzdu. Spočítejte a na výstup vytiskněte celkovou výplatu za celý rok a průměrnou výplatu na jeden měsíc.

### Počet slov

Stáhněte si odevzdanou [slohovou práci](assets/praha.txt). Zadání bylo sepsat text o nejméně 150ti slovech pojednávající o našem hlavním městě. Napište program, který spočítá počet slov v tomto textu, abychom věděli, zda bylo zadání formálně splněno. Nechte se vést následujícím návodem.

1. Nechte váš program otevřít soubor a načíst jednotlivé řádky do seznamu.
1. Každý řádek převeďte na seznam slov. Slovem se rozumí vše, co je odděleno mezerou nebo novým řádkem.
1. Vypište na výstup seznam hodnot udávající počty slov na každém řádku.
1. Vypište na výstup celkový počet všech slov v souboru.

### Půjčovna

Půjčovna aut má v každém kraji ČR jedno auto s danou SPZ. Ke konci roku chce zjistit, kolik všechna auta najezdila dohromady kilometrů. V souboru [auta.txt](assets/auta.txt) je pro každou SPZ zaznamenáno kolik dané auto ujelo kilometrů za daný rok. Hodnoty jsou v tisících kilometrů. Bohužel se v jednotlivých krajích blbě zkoordinovali a někdo používal desetinnou čárku, někdo zase tečku.

1. Napište program, který na výstup vypíše součet všech ujetých kilometrů. Jistě se vám bude hodit metoda řetězců jménem `replace()`.
1. Upravte váš program tak, aby jméno souboru k otevření dostal na příkazové řádce, abychom mohli takto zpracovávat výkazy z různých souborů, aniž bychom museli upravovat samotný kód programu.

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

Je to proto, že metoda `write()` narozdíl od funcke `print()` nedělá
automatické odřádkování. Konce řádků tedy do souboru musíme zapsat my.
Upravíme tedy zápis do souboru v našem předchozím programu takto:

```py
[soubor.write(jmeno + '\n') for jmeno in jmena]
```

## Cvičení

### Dny v měsíci

Napište program, který bude mít přímo v kódu zapsaný počet dní v jednotlivých měsících takto:

```py
pocty_dni = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
```

1. Nechte váš program vypsat tento seznam do souboru s názvem `kalendar.txt`, každé číslo na jeden řádek.
1. Upravte váš program tak, aby zároveň s počtem dnů vypisoval i název měsíce. Oddělte v souboru název měsíce a počet dnů pomocí tabulátoru.
1. Upravte váš program tak, aby jako první řádek výsledného souboru obsahoval nadpisy pro jednotlivé sloupce, tedy `měsíc` a `počet dní`.

### Rozepsaná výplata

Modifikujte program pro počítání výplaty z předchozí sekce tak, aby nevypisoval průměrnou výplatu za rok, nýbrž aby vypsal konkrétní vyplacenou částku pro každý měsíc zvlášť.

1. Nejprve tyto informace vypište na výstup pomocí funkce `print()`.
1. Poté program upravte tak, aby vypsal tyto výsledky do souboru.

### Hody kostkou

Napište program, který vytvoří seznam deseti náhodných hodů dvanáctistěnnou kostkou.

1. Nejdříve tento seznam vytiskněte na konzoli pomocí funkce `print()`.
1. Upravte váš program tak, aby náhodné hody kostkou vypsal do souboru s názvem `hody.txt` na jeden řádek oddělené čárkou a mezerou.
1. Upravte váš program tak, aby počet hodů dostal jako parametr na příkazové řádce. Zkuste použitím vašeho programu vyrobit 100, 1000 a 10 000 hodů.

## Čtení na doma

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

Kódování textu souvisí s tím, jak si počítač data ukládá do paměti. Nyní slovo <i>data</i> používáme v širším kontextu, tedy nejen pro tabulky hodnot, ale také pro všechny ostatní textové soubory, audio, video, programy, prostě úplně cokoliv, co můžete uložit na váš harddisk. Fungování paměti počítače je sice velmi technická věc, ale nám bude stačit, že pamět se skládá z dále nedělitelných buněk, jakýchsi chlívečků, do kterých si počítač může uložit co chce. Technicky se těmto buňkám říká <i>bajty</i>. Potíž je v tom, že jeden bajt (anglicky byte) je velmi malý kousek paměti a navíc se do něj dá uložit pouze číslo, nic jiného. Navíc toto číslo může být pouze z rozmezí 0 až 255.

Pokud tedy chceme do paměti uložit kus textu, počítač si každé písmenko musí interně převést na číslo, a to pak uložit do jedné buňky. Velké písmeno A má například kód 65, vykřičník má kód 33, a tak dále. Anglický text, který má např. 1024 znaků, tak zabere 1024 buněk paměti, nebo-li 1024 bajtů, nebo-li jeden kilobajt.

Právě v převádění znaků na čísla spočívá velký kámen úrazu. V minulosti se totiž technologické firmy a standardizační organizace neshodly na tom, jak na čísla převádět znaky, které nepatří do anglické abecedy. Navíc je problém, že neanglických znaků je víc než 256. Kdyby tak jen šlo o písmenka s čárkami aháčky, ale co třeba azbuka, řečtina a další jazyky. Navíc Číňané nebo Japonci taky mají počítače a chtějí na nich používat svoje brutální abecedy o tisících a tisících znaků. Kódy pro neanglické znaky tedy jistě budou větší než 255, tedy se nám rozhodně nevejdou do jedné buňky a navíc ani není jasné, které znaky má znaková sada vůbec zahrnovat. Vzniklo tak spousta způsobů jak různé znaky kódovat ‒ takzvané znakové sady. V každé znakové sadě má stejné neanglické písmenku různý kód a každé obsahuje jen některé vybrané neanglické znaky. Jedna znaková sada například obsahuje některé české znaky čárkami, ale už neobsahuje háčky, nebo zase obsahuje háčky ale chybí jím 'ř', které má pouze čeština, a tak dále a tak dále.

### Unicode a UTF-8

Není divu, že programátoři měli ze všech těch různých znakových sad za chvíli hlavu jak balón. Postupně tedy dotlačili technologické firmy a organizace k tomu, aby standardizovaly jednu neměnnou znakovou sadu, která bude obsahovat, teď se držte, **úplně všechny znaky z úplně všech jazyků na celé planetě** a každý znak bude mít jasně určený kód. Tomuto standardu se říká Unicode a k dnešnímu dni obsahuje 137 374 znaků včetně čínštiny, cyrilice, smajlíků a různých piktogramů, každý znak se svým unikátním číslem. Díky tomu, že tato webová stránka používá Unicode znakovou sadu, může obsahovat písmenko 'ř', které má číslo 345, znak letadla '✈', který má číslo 9992, nebo znak z hlaholice 'Ⰶ' zvaný <i>živěte</i> s číslem 11270.

Teď ovšem pozor. Unicode ještě není kódování textu, nýbrž pouze znaková sada, tedy jenom seznam znaků a jim přiřazených čísel. Protože kódy pro většinu znaků jsou větší než 255, potřebujeme mít způsob, jak rozdělit takto velká čísla na více bajtů, abychom zároveň šetřili pamětí. Standard Unicode nabízí více možností jak toto provést, z nichž nepoužívanější se jmenuje _UTF-8_.

A proto jsme, milé děti, museli použít při otvírání souborů v Pythonu argument `encoding='utf-8'`. Dnes už je kódování UTF-8 naprostý standard. Používají jej všechny moderní webové stránky, moderní programovací jazyky a textové editory. Bohužel na systému Windows se ještě často setkáte se starým způsobem kódování. Dejte si proto pozor, pod jakým kódováním váš textový soubor ukládáte a vždy vyberte UTF-8. Jinak bude váš textový soubor v Pythonu vypadat jako rozsypaná rýže.

### Všude bordel

Teď už bychom si naivně mohli myslet, že je ve všem pořádek, ale to by byl život příliš snadný. Obzvlášť operační systém Windows umí někdy do věcí kvalitně hodit vidle. Například Poznámkový blok používá jako výchozí nastavení pro ukládání textových souborů kódování ANSI, které je už dávno zastaralé a vůbec nedává smysl ho nadále používat. Pokud si v Poznámkovém bloku při ukládání rozbalíte nabídku kódování, uvidíte tam ale také možnost "kódování Unicode", což je nesmysl, protože Unicode není kódování, nýbrž znaková sada. Standard Unicode nabízí více možných kódování: UTF-8, UTF-16 a UTF-32, které se liší tím, jak moc šetří pamětí. A z nepochopitelných důvodu se občas **kódování** UTF-16 pro **znakovou sadu** Unicode říká **kódování Unicode** i přesto, že témeř všichni používají kódování UTF-8.

Občas programátorům nezbude, než mlátit hlavou do stolu a křičet PROČ? Ale tak je to občas i v životě. Takže nezapomeňte naučit svoje děti, aby vždy ukládaly textové soubory jako UTF-8. Svět pak bude zase o kousek lepším místem.

## Domácí úložky ‒ povinné

### Pasažéři

**Obtížnost: To dáš**

Autobus mezi Zdebudevsí a Kozoprdy jezdí čtyřikrát denně každý všední den v týdnu. Za poslední týden jsme naměřili počty pasažérů pro každou jízdu tam i zpět. Data jsou uložená v souboru [pasazeri.txt](assets/pasazeri.txt). Jízda vždy obsahuje dvě čísla oddělená čárkou, která udávají počet pasažérů směrem tam a směrem zpět.

1. Napište program, který pro první den vypíše, kolik pasažérů jelo celkem směrem tam a kolik směrem zpět.
1. Nechť váš program vypisuje součty pasažérů ze celý týden, tedy kolik lidí za celý týden jelo směrem tam a kolik směrem zpět.

### Přeznámkování

**Obtížnost: Zapni hlavu**

Univerzita pro celoživotní vzdělávání se rozhodla změnit svůj známkovací systém z číselných známek 1 až 5 na hodnocení písmeny A až F. Bohužel změna se odehrála jaksi uprostřed semestru, takže je potřeba změnit aktuální výkazy o známkách z čísel na písmena. Nechte se vést následujícím postupem.

1. Otevřete si [dokument](https://docs.google.com/spreadsheets/d/1mm2iZ2TWosQ4Yv4cahgMQrMsicneTrkrcdVP3Nz1PQY/edit?usp=sharing) s jedním výkazem známek.
1. Zkopírujte si tuto tabulku do textového souboru.
1. Napište program, který tuto tabulku načte ze souboru a změní všechny známky tak, že 1 bude A, 2 bude B, 3 bude C, 4 bude D a 5 bude F.
1. Vypište váš výsledek do nějakého souboru tak, aby se z něj dal zase zkopírovat do tabulky Google.
1. Vytvořte novou Google tabulku, která vypadá stejně jako ta výše avšak s převedenými známkami.

## Domácí úložky ‒ nepovinné

### Karty 2

**Obtížnost: Zapni hlavu**

Napište program, který vylosuje seznam 4 náhodných hracích karet podobně jako v úložce Karty 1 z minulé lekce. Můžeme si představovat, že rozdáváme karty například v pokru. Zatím pro jednoduchost nebudeme řešit, že se nám může nějaká karta v seznamu opakovat.

1. Vymyslete, jak budete vylosovanou kartu v seznamu reprezentovat. Vypište pak tento seznam na výstup.
1. Dále k tomuto seznamu vypište součet hodnot všech vylosovaných karet. Položme hodnotu karet J, Q a K rovnu deseti a eso rovnu jedné.

### Karty 3

**Obtížnost: Zapni hlavu**

Zkusme vyřešit problém losování karet tak, aby se nám nemohlo stát, že nám nějaká karta padne vícekrát, když by správně v balíčku měla být od každé karty pouze jedna.

Ze souboru [karty.txt](assets/karty.txt) si načtěte do seznamu kompletní balíček karet. Zadání je stejné jako v předchozí úložce, tedy vylosovat 4 karty z balíčku a vypsat je jako seznam spolu se součtem hodnot.

Existuje vícero možných postupů, které vedou ke stejnému výsledku. Zde už můžete trochu zagooglit. Ve většině postupů se vám bude hodit příkaz, který umí odstranit prvek seznamu na zadaném indexu:.

```pycon
>>> x = [1, 2, 3]
>>> del x[0]
>>> x
[2, 3]
```

Také se vám může hodit funkce `shuffle()` z modulu `random`, která umí náhodně zamíchat seznam.
