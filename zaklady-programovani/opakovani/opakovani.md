Následující příklad v sobě zahrnuje většinu věcí, kterou jsme se do teď v kurzu naučili. Můžete jej vyzkoušet a zjistit, jak na tom jste se svými programátorskými schopnostmi a co jste si z kurzu zapamatovali.

## Prváci

Na Fakultu hybridních přírodních umění nastupují nově přijatí studenti. Tabulku těchto studentů s jejich rodnými čísly najdete v souboru [studenti.txt](assets/studenti.txt). Tabulka je evidentně vykopírovaná z Excelu, neboť hodnoty jsou zde odděleny tabulátory. Na každém řádku je jméno a příjmení studenta a jeho rodné číslo. Vytvořte Python program a proveďte v něm následující úkony.

1. Načtěte data ze souboru do vašeho programu jako tabulku v podobě seznamu seznamů. Každý vnořený seznam bude představovat jeden řádek tabulky.
1. Přidejte do tabulky sloupec, který bude udávat věk studenta. Věk studenta zjistíte podle roku narození, což jsou první dvě cifry rodného čísla.
1. Přidejte do tabulky sloupec, který bude udávat zda je student muž či žena. Pohlaví poznáte podle měsíce narození (druhé dvě cifry rodného čísla). Pokud je člověk ženského pohlaví, přičítá se k první cifře měsíce narození číslo 5.
1. Přidejte do tabulky sloupec, který bude udávat univerzitní email studenta. Univerzitní mail vznikne tak, že se vezme prvních pět písmenek příjmení a první tři písmenka křestního jména. Za takto vzniklý řetězec se připojí doména `@hybrid.edu`.

**Příklad:** Student se jménem Květoslav Štístko bude mít email `stistkve@hybrid.edu`. Všimněte si, že pro tuto konstrukci potřebujeme jméno zbavit diakritiky. To lze v Pythonu provést pomocí modulu `unidecode`. Tento modul není ve výchozí instalaci Pythonu k dispozici, musíme si jej proto doinstalovat:

```shell
pip3 install unidecode
```

Popřípadě na Windows:

```shell
pip install unidecode
```

Pozor, že na Macu je potřeba použít `pip3`. Tento modul obsahuje funkci `unidecode` (náhodou se jmenuje stejně jako modul samotný). Pokud tuto funkci zavoláte s řetězcem s diakritikou, vrátím vám řetězec bez diakritiky. Využijte tuto funkci ke splnění tohoto úkolu.

5. Uložte výslednou tabulku ve formátu JSON do souboru s názvem `studenti.json`. K tomu bude potřeba seznam seznamů převést na seznam slovníků. Každý řádek tabulky tedy bude reprezentován slovníkem, kde klíče jsou názvy sloupečků.
