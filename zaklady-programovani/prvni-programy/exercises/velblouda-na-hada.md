---
title: Jak proměnit velblouda na hada
demand: 5
---

Napište program, který dostane na příkazovém řádku název proměnné ve velbloudí notaci a vrátí tentýž název zapsaný v hadí notaci.

Příklad:

```shell
$ python3 velbloud-had.py velbloudHoniHada
velbloud_honi_hada
```

Ano, tohle už není procházka růžovým sadem a jde o úložku spíše pro fajnšmekry, Python gurmány a lidi s neutišitelnou touhou nenechat žádný příklad nevyřešený. Vězte, že skutečně existuje řešení, které používá výhradně probrané techniky. Vyplatí se mrknout na to, jaké všechny metody nabízí Python řetězce, jinak ale není potřeba žádné googlení, jen se nesmíte bát věci, které už tak dobře znáte, opravdu použít, a nemít je ve své programátorské dílně jen vystavené za sklem.

Některé pasáže programu si lze mírně ulehčit použítím funkce `enumerate()`, která vám při chroustání seznamů vrací nejen prvek seznamu, ale i jeho index. Vyzkoušejte například následující příkaz

```py
[[i, jmeno] for i, jmeno in enumerate(['petr', 'jana', 'vlasta', 'onyx'])]
```

Úlohu lze však vyřešit i bez `enumerate()`!
