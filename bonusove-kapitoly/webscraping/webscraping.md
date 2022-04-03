Mnoho webových stránek na internetu obsahuje velmi zajímavá a užitečná data. Takových dat můžu být velký objem a mohou být rozházená po různých stránkách pod mnoha odkazy a není v našich silách je ručně ze stránek vykopírovat. Příkladem budiž například historická data o naměřených teplotách ze stránek [Českého hydrometeorologického ústavu](http://portal.chmi.cz/historicka-data/pocasi/uzemni-teploty). Tato data jsou dostupná pouze skrze tabulky vložené přímo do webových stránek. Pokud chceme takovéto množství dat ze stránek dostat do našeho programu, musíme použít takzvaný _web scraping_.

## HTML

Web scraping je technika pomocí které můžeme strojově číst obsah webových stránek na internetu. Webové stránky často vypadají velmi komplikovaně a sofistikovaně, ale nakonec jsou to pouhopouhé textové soubory psané ve speciálním jazyce zvaném HTML (HyperText Markup Language). Naštěstí pro nás není HTML jazyk programovací, nýbrž takzvaně _značkovací_. Není tedy zdaleka tak složitý jako například jazyk Python. Jazyk HTML má relativně jednoduchou strukturu a ani pro úplného začátečníka není těžké se v něm zorientovat. Pomocí HTML tvůrci webů definují samotný obsah stránek, tedy texty, obrázky, odkazy apod. Samotný vzhled stránky (barvičky, styl písma, rozmístění prvků na stránce apod.) se vytváří v jazyce zvaném CSS, který ale v tuto chvíli můžeme nechat být, neboť z hlediska zpracování dat nás vzhled stránek nezajímá.

### HTML značky (tagy)

V následující ukázce vidíte HTML kód celé webové stránky tak, jak by si ji stáhl prohlížeč odněkud ze server.

```html
<html>
<head>
  <meta charset="UTF-8">
  <title>Ukázka</title>
</head>
<body>
  <h1>Nadpis první úrovně</h1>
  <p>
    Text nějakého odstavce, který obsahuje
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
      <li>První položka seznamu</li>
      <li>Druhá položka seznamu</li>
      <li>Třetí položka seznamu</li>
    </ol>
  </div>
</body>
</html>
```

Stránka se poté v prohlížeči zobrazí nějak takto. Zatím nevypadá příliš vábně, protože není nastylovaná. Styly nás však v této lekci nezajímají, protože pro webscraping nejsou důležité.

::fig[Ukázka HTML]{src=assets/ukazka-html.png size=80}

Vytvořte si na svém počítači složku `ukazka-html` a otevřete ji ve Visual Studiu. Vytvořte v této složce soubor `ukazka.html` a zkopírujte do něj výše uvedený kód a uložte. Poté tento soubor najděte v průzkumníku a dvojklikem by se vám měl otevřít ve vašem oblíbeném prohlížeči. Můžete tak zkontrolovat, že prohlížeč vaši stránku skutečně zobrazí tak, jak je uvedeno na obrázku výše.

V naší první webové stránce jsme viděli takzvané :term{cs="HTML značky" en="HTML tags"}. Značky se píší do špičatých závorek a většina značek má otevírací a zavírací část. Například značka `em` pro zvýraznění textu vypadá takto

::fig[HTML značka]{src=assets/html-znacka.png size=60}

Značky mohou mít takzvané atributy, které dále specifikují, co značka bude přesně zobrazovat. Například značka `ol` představuje seznam položek a má atribut zvaný `type`, který určuje, jestli se číslování položek děje pomocí písmen nebo čísel.

::fig[HTML atribut]{src=assets/html-atribut.png size=60}

Zajímavá a téměř nejpoužívanější je značka `div`, která sama o sobě nemá žádný vizuální význam. Slouží totiž k členění stránky na menší části. Všimněte si, že naší ukázkové stránka značku `div` také používá. Navíc u ní najdeme atribut `class`. Ten se běžně používá k stylování stránky a často podle něj můžeme při webscrapingu odlišit důležité části stránky.

Všech HTML značek je kolem stovky a mnoho z nich má spoustu možných atributů. Rozumět všem těmto značkám je prací webových vývojářů. Nám bude stačit získat nějaké malé povědomí alespoň o pár základních.

Pokud by vás zajímalo, co vše je v HTML možné, přehled všech používaných značek [najdete zde (anglicky)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).

## Cvičení
::exc[excs>porozumeni-html]

## Web scraping v Pythonu

Abychom mohli s obsahem webových stránek pracovat přímo v Pythonu, potřebujeme nainstalovat modul, který umí číst HTML značky a pomocí těchto značek v HTML souborech vyhledávat. Takových modulů pro jazyk Python existuje vícero. My použijeme balíček zvaný `requests-html`, který je určený přímo pro web scraping. Nainstalovat jej můžeme příkazem

```shell
pip3 install requests-html
```

Popř. na Windows

```shell
py -m pip install requests-html
```

Abychom mohli v našem programu scrapovat, musíme nejdřív webovou stránku otevřít. Vzhledem k tomu, že obsah textového souboru už do proměnné načíst umíme, stačí tedy jen použít náš nový modul, aby si tento obsah přečetl a umožnil v něm vyhledávat.

Ve Visual Studiu ve složce s naší ukázkovou stránkou si vytvořte program `scrape.py` s tímto obsahem

```py
from requests_html import HTML
with open('sample.html', encoding='utf-8') as soubor:
  obsah = soubor.read()
html = HTML(html=obsah)
```

Proměnná html, nyní obsahuje naši HTML stránku ve formátu, který můžeme použít k vyhledávání.

HTML značky můžeme vyhledávat podle jména. Takto například najdeme všechny odstavce a vypíšeme jejich text každý na nový řádek.

```py
for odstavec in html.find('p'):
  print(odstavec.text)
```

Velmi časté je také vyhledávání podle třídy (atribut `class`). Třídy se vyhledávají tak, že jejich název začneme tečkou.

```py
html.find('.sekce1')
```

Snadno také můžeme přistupovat k atributům nalezených značek. Takto můžeme například najít adresy všech odkazů na naší stránce.

```py
for odkaz in html.find('a'):
  print(odkaz.attrs['href'])
```

### Složitější pravidla vyhledávání

Vyhledávací řetězce v metodě `find()` mohou být složitější, než jak jsme viděli doposud.

Můžeme vyhledávat podle více značek najednou. Například najít všechny nadpisy první i druhé úrovně.

```py
html.find('h1, h2')
```

Můžeme vyhledávat podle atributů. Například najít všechny seznamy, kde atribut `type` je roven `a`.

```py
html.find('ol[type="a"]')
```

Můžeme vyhledávat podle zanoření. Například najít všechny odstavce, které jsou uvnitř značky s třídou `sekce1`.

```py
html.find('.sekce1 p')
```

Mezera ve vyhledávacím řetězci znamená libovolně hluboké zanoření. Pokud bychom chtěli pouze odstavce, které jsou _přímým_ potomkem značky s třídou `sekce1`, použijeme symbol zobáčku.

```py
html.find('.sekce1 > p')
```

Pokud tyto techniky zkombinujeme, můžeme například najít všechny položky ve všech seznamech, jejichž atribut `type` je roven `a`.

```py
html.find('ol[type="a"] li')
```

## Scraping přes internet

Zatím jsme scrapovali pouze stránku, kterou jsme měli uloženou na disku. Pomocí modulu `requests-html` můžeme však také snadno otevřít stránku přímo na internetu. Na adrese <https://apps.kodim.cz/python-data/scrape> najdete naši malou ukázkovou stránku z úvodu. Na adrese <https://apps.kodim.cz/python-data/dhmo> najdete také finální verzi stránky šířící poplach ohledně DHMO.

Načteme v Pythonu první z odkazů a stejně jako prve vypíšeme texty všech odstavců.

```py
from requests_html import HTMLSession
session = HTMLSession()
stranka = session.get('https://apps.kodim.cz/python-data/scrape')
for odstavec in stranka.html.find('p'):
  print(odstavec.text)
```

Dále můžeme postupovat úplně stejně jako když jsme zpracovávali stránky z disku. Pokud chcete vidět celý stažený zdrojový kód stránky jako text, napište

```py
print(stranka.html.html)
```

## Cvičení: Scraping
::exc[excs>scraping-dhmo]
::exc[excs>scraping-kodim.cz]

## Web scraping vs JavaScript

Web scraping je velmi mocná technika. Její úspěšnost však závisí na tom, jakým způsobem jsou webové stránky napsány. Pokud jsou napsány prasácky a nekonzistentně, tak si web scrapingem můžeme snadno způsobit velký bolehlav.

Jeden z velkých problémů pro web scraping však představují stránky, které jsou vytvořené celé v JavaScriptu. Velkým trendem v dnešní době je nepsat HTML kód stránky přímo, jako jsme to viděli výše. Místo toho se použije jazyk JavaScript, který kód stránky sám vygeneruje. Tím může být stránka mnohem flexibilnější a interaktivnější, což je hezké pro uživatele. Pro nás to však znamená, že když stránku stahujeme v Pythonu, neobdržíme značky HTML, ale JavaScriptový program, který nejdříve musíme v Pythonu spustit a nechat si výsledné HTML vygenerovat.

Podívejte se například na [tuto stránku](https://react-shopping-cart-67954.firebaseapp.com/), která je psána přesně tímto způsobem. Pokud chceme takovou stránku scrapovat, musíme použít takovýto kód.

```py
from requests_html import HTMLSession
session = HTMLSession()
stranka = session.get('https://react-shopping-cart-67954.firebaseapp.com/')
stranka.html.render(sleep=5)
```

## Doporučené úložky na doma
::exc[excs>kava-na-mall.cz]

## Čtení na doma

Webscraping je velmi široká oblast a těžko se člověk do jejích tajů dostane během jedné lekce. Obzvláště u komplikovanějších stránek je často nutné zkoušet různé techniky a přístupy, umět si poradit v různých situacích, nenechat se snadno odradit ošklivě napsaným HTML kódem a vůbec být mazaný jako liška.
