Mnoho webových stránek na internetu obsahuje velmi zajímavá a užitečná data.
Takových dat můžu být velký objem a mohou být rozházená po různých stránkách
pod mnoha odkazy a není v našich silách je ručně ze stránek vykopírovat.
Příkladem budiž například historická data o naměřených teplotách ze stránek
[Českého hydrometeorologického ústavu](http://portal.chmi.cz/historicka-
data/pocasi/uzemni-teploty). Tato data jsou dostupná pouze skrze tabulky
vložené přímo do webových stránek. Pokud chceme takovéto množství dat ze
stránek dostat do našeho programu, musíme použít takzvaný _web scraping_.

## HTML

Web scraping je technika pomocí které můžeme strojově číst obsah webových
stránek na internetu. Webové stránky často vypadají velmi komplikovaně a
sofistikovaně, ale nakonec jsou to pouhopouhé textové soubory psané ve
speciálním jazyce zvaném HTML (HyperText Markup Language). Naštěstí pro nás
není HTML jazyk programovací, nýbrž takzvaně _značkovací_. Není tedy zdaleka
tak složitý jako například jazyk Python. Jazyk HTML má relativně jednoduchou
strukturu a ani pro úplného začátečníka není těžké se v něm zorientovat.
Pomocí HTML tvůrci webů definují samotný obsah stránek, tedy texty, obrázky,
odkazy apod. Samotný vzhled stránky (barvičky, styl písma, rozmístění prvků na
stránce apod.) se vytváří v jazyce zvaném CSS, který ale v tuto chvíli můžeme
nechat být, neboť z hlediska zpracování dat nás vzhled stránek nezajímá.

### HTML značky (tagy)

V následující ukázce vidíte kód webové stránky zároveň s tím jak by takovou
stránku zobrazil prohlížeč.

    
    
    <html>
    <head>
      <meta charset="UTF-8">
      <title>Ukazka</title>
    </head>
    <body>
      <h1>Nadpis prvni urovně</h1>
      <p>
        Text nějakeho odstavce, který obsahuje 
        <em>zvýrazněný text</em> a také <strong>
        důležitý text.</strong>
      </p>
    
      <h2>Nadpis druhé úrovně</h2>
      <div class="sekce1">
        <p>
          Druhý odstavec je v takzvaném divu, což je 
          značka, která nemá sama o sobě žádný význam.
          Také zde máme
          <a href=&quothttp;://www.czechitas.cz"> odkaz na 
          stránky Czechitas</a>.
        </p>
    
        <ol type="a">
          <li>Prvni položka seznamu</li>
          <li>Druha položka seznamu</li>
          <li>Třeti položka seznamu</li>
        </ol>
      </div>
    </body>
    </html>
    

![Ukázka HTML](/czechitas/python-data/assets/datova-analyza/webscraping/ukazka-html.png)

Vytvořte si na svém počítači složku `ukazka-html` a otevřete ji ve Visual
Studiu. Vytvořte v této složce soubor `ukazka.html` a zkopírujte do něj výše
uvedený kód a uložte. Poté tento soubor najděte v průzkumníku a dvojklikem by
se vám měl otevřít ve vašem oblíbeném prohlížeči. Můžete tak zkontrolovat, že
prohlížeč vaši stránku skutečně zobrazí tak, jak je uvedeno na obrázku výše.

V naší první webové stránce jsme viděli takzvané _HTML značky_. Značky se píší
do špičatých závorek a většina značek má otevírací a zavírací část. Například
značka `em` pro zvýraznění textu vypadá takto

![HTML značka](/czechitas/python-data/assets/datova-analyza/webscraping/html-znacka.png)

Značky mohou mít takzvané atributy, které dále specifikují, co značka bude
přesně zobrazovat. Například značka `ol` představuje seznam položek a má
atribut zvaný `type`, který určuje, jestli se číslování položek děje pomocí
písmen nebo čísel.

![HTML atribut](/czechitas/python-data/assets/datova-analyza/webscraping/html-atribut.png)

Zajímavá a téměř nejpoužívanější je značka `div`, která sama o sobě nemá žádný
vizuální význam. Slouží totiž k členění stránky na menší části. Všimněte si,
že naší ukázkové stránka značku `div` také používá. Navíc u ní najdeme atribut
`class`. Ten se běžně používá k stylování stránky a často podle něj můžeme při
webscrapingu odlišit důležité části stránky.

Všech HTML značek je kolem stovky a mnoho z nich má spoustu možných atributů.
Rozumět všem těmto značkám je prací webových vývojářů. Nám bude stačit získat
nějaké malé povědomí alespoň o pár základních.

Pokud by vás zajímalo, co vše je v HTML možné, přehled všech používaných
značek [najdete zde (anglicky)](https://developer.mozilla.org/en-
US/docs/Web/HTML/Element).

## Cvičení

### Porozumění HTML

Cílem tohoto cvičení je pokusit se vyznat ve zdrojovém kódu jednoduché webové
stránky a získat tak povědomí o tom jak funguje jazyk HTML. Postupujte dle
následujících kroků.

  1. Stáhněte si následující [ZIP soubor](/download/python-data/dhmo.zip), který rozbalte někam na váš počítač. V rozbalené složce `dhmo` rozkliněte soubor `index.html`. V prohlížeči by se vám měla otevřít jednoduchá webová stránka pojednávající o škodlivosti jedné velmi zajímavé chemikálie. Stránka nevypadá příliš vábně, protože není napojena na žádné CSS styly, a vidíme tedy jen čistý obsah.
  2. Složku `dhmo` si otevřete ve Visual Studiu a podívejte se na obsah souboru `index.html`. Uvidíte spoustu HTML značek. Některé z nich znáte, některé jste v životě neviděli. Nenechte se vylekat tím, že některým částem tohoto souboru vůbec nerozumíte. Zkuste v souboru najít nějaký kousek textu, který vidíte na vaší otevřené webové stránce a tím se trochu zorientovat. 
  3. V úvodním odstavci stránky jsou tři překlepy. Opravte je přímo v souboru `index.html`. Nezapomeňte jej uložit. Obnovte stránku ve vašem prohlížeči (zkratka Ctrl+R nebo CMD+R) a měli byste vidět změny, které jste provedli.
  4. Najděte v souboru `index.html` část, která obsahuje výčet faktů o DHMO. Tyto seznamy jsou číslované, což naznačuje HTML značka `<ol>`. Změňte u obou seznamů tuto značku na `<ul>`, což znamená nečíslovaný seznam. Nezapomeňte změnit i uzavírací značku seznamu (ta s lomítkem). Otevírací a uzavírací značky musí vždy souhlasit!
  5. Najděte poblíž začátku souboru `index.html` značku `<img>`, která do stránky vkládá úvodní obrázek. Atribut `src` udává cestu k souboru s obrázkem. Všimněte si, že blízko ke konci souboru těsně před seznamem odkazů je ještě jedna značka `<img>`, které ale atribut `src` chybí a proto na stránce žádný obrázek nevidíme. Nastavte atribut `src` na hodnotu `img/dhmo-ban.png` a podívejte se, jak se stránka změnila. 
  6. Podobně jako náš obrázek, poslední odkaz v seznamu odkazů nemá atribut `href`, což způsobuje, že se odkaz na stránce nezobrazuje jako odkaz. Atribut `href` říká, na kterou adresu má odkaz vést. Nastavte proto v posledním odkazu hodnotu atributu `href` na `http://www.snopes.com/science/dhmo.asp`.
  7. Téměř na začátku souboru `index.html` najdete značku `<title>`. Ta udává název stránky, který se zobrazuje v záložce prohlížeče. Změňte tento název prostě na "DHMO šíří hrůzu". 
  8. Pokud chcete vidět, jak by tato stránka vypadala nastylovaná, vložte na nový řádek před značkou `<title>` tento kód
    
        <link rel="stylesheet" href="style.css" />

Uložte soubor, obnovte stránku v prohlížeči a kochejte se.

## Web scraping v Pythonu

Abychom mohli s obsahem webových stránek pracovat přímo v Pythonu, potřebujeme
nainstalovat modul, který umí číst HTML značky a pomocí těchto značek v HTML
souborech vyhledávat. Takových modulů pro jazyk Pythoh existuje vícero. My
použijeme balíček zvaný `requests-html`, který je určený přímo pro web
scraping. Nainstalovat jej můžeme příkazem

    
    
    pip3 install requests-html

Opět pozor, že na Windows je tento příkaz bez čísla 3.

    
    
    pip install requests-html

Abychom mohli v našem programu scrapovat, musíme nejdřív webovou stránku
otevřít. Vzhledem k tomu, že obsah textového souboru už do proměnné načíst
umíme, stačí tedy jen použít náš nový modul, aby si tento obsah přečetl a
umožnil v něm vyhledávat.

Ve Visual Studiu ve složce s naší ukázkovou stránkou si vytvořte program
`scrape.py` s tímto obsahem

    
    
    from requests_html import HTML
    soubor = open('sample.html', encoding="utf-8")
    obsah = soubor.read()
    soubor.close()
    html = HTML(html=obsah)

Proměnná html, nyní obsahuje naši HTML stránku ve formátu, který můžeme použít
k vyhledávání.

HTML značky můžeme vyhledávat podle jména. Takto například najdeme všechny
odstavce a vypíšeme jejich text každý na nový řádek.

    
    
    for odstavec in html.find('p'):
      print(odstavec.text)
    

Velmi časté je také vyhledávání podle třídy (atribut `class`). Třídy se
vyhledávají tak, že jejich název začneme tečkou.

    
    
    html.find('.sekce1')

Snadno také můžeme přistupovat k atributům nalezených značek. Takto můžeme
například najít adresy všech odkazů na naší stránce.

    
    
    for odkaz in html.find('a'):
      print(odkaz.attrs['href'])

### Složitější pravidla vyhledávání

Vyhledávací řetězce v metodě `find()` mohou být složitější, než jak jsme
viděli doposud.

Můžeme vyhledávat podle více značek najednou. Například najít všechny nadpisy
první i druhé úrovně.

    
    
    html.find('h1, h2')

Můžeme vyhledávat podle atributů. Například najít všechny seznamy, kde atribut
`type` je roven `a`.

    
    
    html.find('ol[type="a"]')

Můžeme vyhledávat podle zanoření. Například najít všechny odstavce, které jsou
uvnitř značky s třídou `sekce1`.

    
    
    html.find('.sekce1 p')

Mezera ve vyhledávacím řetězci znamená libovolně hluboké zanoření. Pokud
bychom chtěli pouze odstavce, které jsou _přímým_ potomkem značky s třídou
`sekce1`, použijeme symbol zobáčku.

    
    
    html.find('.sekce1 > p')

Pokud tyto techniky zkombinujeme, můžeme například najít všechny položky ve
všech seznamech, jejichž atribut `type` je roven `a`.

    
    
    html.find('ol[type="a"] li')

## Scraping přes internet

Zatím jsme scrapovali pouze stránku, kterou jsme měli uloženou na disku.
Pomocí modulu `requests-html` můžeme však také snadno otevřít stránku přímo na
internetu. Na adrese <http://scrape.kodim.cz/sample/index> najdete naši malou
ukázkovou stránku z úvodu. Na adrese <http://scrape.kodim.cz/dhmo/index>
najdete také finální verzi stránky šířící poplach ohledně DHMO.

Načteme v Pythonu první z odkazů a stejně jako prve vypíšeme texty všech
odstavců.

    
    
    from requests_html import HTMLSession
    session = HTMLSession()
    stranka = session.get('http://scrape.kodim.cz/sample/index')
    for odstavec in stranka.html.find('p'):
      print(odstavec.text)

Dále můžeme postupovat úplně stejně jako když jsme zpracovávali stránky z
disku. Pokud chcete vidět celý stažený zdrojový kód stránky jako text, napište

    
    
    print(stranka.html.html)

## Cvičení

### Scraping DHMO

Napište program, který bude pracovat se stránkou o DHMO na adrese
<http://scrape.kodim.cz/dhmo/index>.

  1. Nechť program vypíše na výstup nadpisy všech sekcí (značka `h2`).
  2. Nechť program vypíše na výstup cesty všech odkazů na stránce (značka `a`, atribut `href`). 
  3. Nechť program vypíše na výstup cesty ke všem obrázkům na stránce (značka `img`, atribut `src`.

### Scraping Kodim.cz

Jistě vás nepřekvapí, že stránky, které právě čtete, se dají také snadno
scrapovat.

Napište program, který vypíše na výstup všechny povinné a nepovinné domácí
úložky z lekce [První programy](/kurzy/python-data/prvni-programy") spolu s
jejich obtížností.

## Web scraping vs JavaScript

Web scraping je velmi mocná technika. Její úspěšnost však závisí na tom, jakým
způsobem jsou webové stránky napsány. Pokud jsou napsány prasácky a
nekonzistentně, tak si web scrapingem můžeme snadno způsobit velký bolehlav.

Jeden z velkých problémů pro web scraping však představují stránky, které jsou
vytvořené celé v JavaScriptu. Velkým trendem v dnešní době je nepsat HTML kód
stránky přímo, jako jsme to viděli výše. Místo toho se použije jazyk
JavaScript, který kód stránky sám vygeneruje. Tím může být stránka mnohem
flexibilnější a interaktivnější, což je hezké pro uživatele. Pro nás to však
znamená, že když stránku stahujeme v Pythonu, neobdržíme značky HTML, ale
JavaScriptový program, který nejdříve musíme v Pythonu spustit a nechat si
výsledné HTML vygenerovat.

Podívejte se například na [tuto stránku](https://react-shopping-
cart-67954.firebaseapp.com/), která je psána přesně tímto způsobem. Pokud
chceme takovou stránku scrapovat, musíme použít takovýto kód.

    
    
    from requests_html import HTMLSession
    session = HTMLSession()
    stranka = session.get('https://react-shopping-cart-67954.firebaseapp.com/')
    stranka.html.render(sleep=5)
    

## Domácí úložky ‒ povinné

### Káva na Mall.cz

**Obtížnost: To dáš**

Jedna ze stránek, která má pěknou strukturu pro scrapování, je například
[Mall.cz](https://www.mall.cz). Můžete si zde v bezpečí potrénovat své
scrapovací schopnosti dříve, než budete zkoušet vytáhnout data z nějaké
webovky, která je napsaná trošku víc prasácky.

Vaším úkolem v tomto cvičení je napsat program, který stáhne všechny nabízené
instantní kávy ze stránky [www.mall.cz/instantni-
kava](https://www.mall.cz/instantni-kava). Výstupem vašeho programu bude CSV
soubor, který bude obsahovat tři sloupečky: název produktu, cena a zda je
produkt skladem.

## Čtení na doma

Webscraping je velmi široká oblast a těžko se člověk do jejích tajů dostane
během jedné lekce. Obzvláště u komplikovanějších stránek je často nutné
zkoušet různé techniky a přístupy, umět si poradit v různých situacích,
nenechat se snadno odradit ošklivě napsaným HTML kódem a vůbec být mazaný jako
liška.

