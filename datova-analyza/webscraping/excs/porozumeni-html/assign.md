---
title: Porozumění HTML
demand: 3
---

Cílem tohoto cvičení je pokusit se vyznat ve zdrojovém kódu jednoduché webové stránky a získat tak povědomí o tom jak funguje jazyk HTML. Postupujte dle následujících kroků.

1. Stáhněte si následující [ZIP soubor](assets/dhmo.zip), který rozbalte někam na váš počítač. V rozbalené složce `dhmo` rozklikněte soubor `index.html`. V prohlížeči by se vám měla otevřít jednoduchá webová stránka pojednávající o škodlivosti jedné velmi zajímavé chemikálie. Stránka nevypadá příliš vábně, protože není napojena na žádné CSS styly, a vidíme tedy jen čistý obsah.
1. Složku `dhmo` si otevřete ve Visual Studiu a podívejte se na obsah souboru `index.html`. Uvidíte spoustu HTML značek. Některé z nich znáte, některé jste v životě neviděli. Nenechte se vylekat tím, že některým částem tohoto souboru vůbec nerozumíte. Zkuste v souboru najít nějaký kousek textu, který vidíte na vaší otevřené webové stránce a tím se trochu zorientovat.
1. V úvodním odstavci stránky jsou tři překlepy. Opravte je přímo v souboru `index.html`. Nezapomeňte jej uložit. Obnovte stránku ve vašem prohlížeči (zkratka Ctrl+R nebo CMD+R) a měli byste vidět změny, které jste provedli.
1. Najděte v souboru `index.html` část, která obsahuje výčet faktů o DHMO. Tyto seznamy jsou číslované, což naznačuje HTML značka `<ol>`. Změňte u obou seznamů tuto značku na `<ul>`, což znamená nečíslovaný seznam. Nezapomeňte změnit i uzavírací značku seznamu (ta s lomítkem). Otevírací a uzavírací značky musí vždy souhlasit!
1. Najděte poblíž začátku souboru `index.html` značku `<img>`, která do stránky vkládá úvodní obrázek. Atribut `src` udává cestu k souboru s obrázkem. Všimněte si, že blízko ke konci souboru těsně před seznamem odkazů je ještě jedna značka `<img>`, které ale atribut `src` chybí a proto na stránce žádný obrázek nevidíme. Nastavte atribut `src` na hodnotu `img/dhmo-ban.png` a podívejte se, jak se stránka změnila.
1. Podobně jako náš obrázek, poslední odkaz v seznamu odkazů nemá atribut `href`, což způsobuje, že se odkaz na stránce nezobrazuje jako odkaz. Atribut `href` říká, na kterou adresu má odkaz vést. Nastavte proto v posledním odkazu hodnotu atributu `href` na `http://www.snopes.com/science/dhmo.asp`.
1. Téměř na začátku souboru `index.html` najdete značku `<title>`. Ta udává název stránky, který se zobrazuje v záložce prohlížeče. Změňte tento název prostě na "DHMO šíří hrůzu".
1. Pokud chcete vidět, jak by tato stránka vypadala nastylovaná, vložte na nový řádek před značkou `<title>` tento kód

```html
<link rel="stylesheet" href="style.css" />
```

Uložte soubor, obnovte stránku v prohlížeči a kochejte se.
