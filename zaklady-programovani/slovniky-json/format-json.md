## Formát JSON

JSON je formát pomocí kterého můžeme zapsat strukturovaná data jako čistý text. S jedním takovým datovým formátem jste se již potkali, jmenuje se CSV.

JSON formát původně pochází z jazyka, který se jmenuje JavaScript. Ten se hodně používá pro tvorbu webových stránek a jelikož výměna dat nejčastěji probíhá po internetu, ujal se formát JSON všeobecně jako standard pro výměnu dat mezi programy. Výhoda pro nás je, že JSON vypadá téměř stejně jako Python slovníky. Liší se pouze tím, že vždy používá dvojité uvozovky a hodnoty `True` a `False` se píší s malým písmenem, tedy `true` a `false`. Náš absolvent kurzu z úvody lekce by tedy ve formátu JSON vypadal takto:

```json
{
    "jmeno": "Petr",
    "prijmeni": "Roman",
    "rok": 2017,
    "dochazka": 0.95,
    "vyznamenani": true
}
```

### Čtení JSON dat

V Pythonu je velice jednoduché převést JSON na obyčejný Python slovník. Stačí nám k tomu modul jménem `json`. Vyzkoušíme si to na našem seznamu absolventů. Nejdřív si tato data stáhneme jako soubor [absolventi.json](assets/absolventi.json). Ten pak můžeme v Pythonu otevřít a převést na JSON následujícím programem.

```py
import json
with open('absolventi.json', encoding='utf-8') as soubor:
    text = soubor.read()
absolventi = json.loads(text)
print(absolventi)
```

V tomto programu používáme metodu `read`, která umí celý soubor načíst se vším všudy do jednoho velkého řetězce. Tento řetězec pak můžeme předat funkci `loads` z modulu `json`, která tento řetězec přečte a pokud jsou v něm data ve formátu JSON, převede je na Python slovníky.

Pokud bychom se nechtěli sami obtěžovat se čtením souboru, můžeme použít metodu `load`, která umí přečíst JSON přímo z otevřeného souboru.

```py
import json
with open('absolventi.json', encoding='utf-8') as soubor:
    absolventi = json.load(soubor)
print(absolventi)
```

Pokud se ptáte k čemu je nám vůbec funkce `loads`, když můžeme rovnou použít funkci `load`, vydržte do další části této lekce, kde budeme stahovat JSON z internetu. Ten nám totiž vždy přijde jako textový řetězec.

### Zápis JSON dat

Zápis JSON dat do souboru je podobně jednoduché jako čtení. Stačí si osvojit funkci `dump`. Dejme tomu, že máme jednoduchý JSON, který obsahuje například odpracované hodiny pro každý den v týdnu. Ten chceme zapsat do textového souboru.

```py
import json
hodiny = {'po': 8, 'ut': 7, 'st': 6, 'ct': 7, 'pa': 8}
with open('hodiny.json', mode='w', encoding='utf-8') as soubor:
    json.dump(hodiny, soubor)
```

Pokud bychom z nějakého důvodu chtěli pouze vytvořit řetězec obsahující JSON ale nezapisovat jej do souboru, můžeme použít funkci `json.dumps`.

```pycon
>>> hodiny = {'po': 8, 'ut': 7, 'st': 6, 'ct': 7, 'pa': 8}
>>> import json
>>> json.dumps(hodiny)
'{"po": 8, "ut": 7, "st": 6, "ct": 7, "pa": 8}'
```

### Stahování dat z internetu

V předchozím příkladu jsem naše data načetli ze souboru na disku. Pokud však narazíte na vstřícného poskytovatele dat, je možné si data stáhnout z takzvaného API (Application Programming Interface) přímo z internetu. Zkratka API se používá jako označení nějakého přípojného bodu na internetu, odkud si můžete stáhnout data v nějakém strojově čitelném formátu. Nejčastěji je tímto formátem právě JSON.

Malá potíž je ovšem v tom, že Python sám o sobě neobsahuje modul pro stahování dat z internetu. Musíme proto do našeho Pythonu doinstalovat takzvaný externí balíček.

## Externí moduly a balíčky

Python sám o sobě obsahuje mnoho užitečných modulů pro řešení různých typů úloh. Už jsme viděli modul `random` pro práci s náhodnými čísly, modul `statistics` pro základní statistické funkce nebo modul `sys` pro práci s operačním systémem. Všem modulům, které jsou součástí základní instalace Pythonu, se dohromady říká :term{cs="standardní knihovna" en="standard library"}. Přehled všech modulů, které standardní knihovna obsahuje můžete najít [v Python dokumentaci](https://docs.python.org/3/library/).

Čas od času ale v Pythonu potřebujeme vykonat nějakou činnost, pro kterou není ve standardní knihovně dostupný žádný modul, například stáhnou data z internetu. V takovém případě budeme muset z internetu stáhnout a nainstalovat takzvaný :term{cs="balíček" en="package"}.

Balíčky obsahují moduly, které po instalaci balíčku můžeme importovat v našem programu.

Ke stahování dat z internetu potřebujete balíček jménem `requests`. Nainstalujeme jej příkazem

```shell
pip3 install requests
```

Pozor, že ve Windows tento příkaz vypadá takto.

```shell
pip install requests
```

Může se stát, že výše uvedený příkaz nebude fungovat protože nemáte nainstalovaný správce balíčků `pip`\- V takovém případě bude potřeba znova spustit instalaci Pythonu a během ní zaškrtnout, že chcete nainstalovat také `pip`.

## Stahování dat z API

Jeden ze cvičných zdrojů dat najdeme na adrese `https://api.kodim.cz/python-data/people`. Naším jediným cílem je data získat jako text. Pak už jej převedeme na Python slovníky právě s využitím výše zmiňované funkce `loads`.

```py
import requests
import json
response = requests.get('https://api.kodim.cz/python-data/people')
data = json.loads(response.text)
print(data)
```

## Cvičení: API a JSON
::exc[excs>seznam-lidi]
::exc[excs>svatky]
