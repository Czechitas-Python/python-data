---
title: Půjčovna
demand: 4
---

Půjčovna aut má v každém kraji ČR jedno auto s danou SPZ. Ke konci roku chce zjistit, kolik všechna auta najezdila dohromady kilometrů. V souboru [auta.txt](assets/auta.txt) je pro každou SPZ zaznamenáno kolik dané auto ujelo kilometrů za daný rok. Hodnoty jsou v tisících kilometrů. Bohužel se v jednotlivých krajích blbě zkoordinovali a někdo používal desetinnou čárku, někdo zase tečku.

V souboru s daty je ještě jeden problém, který není na první pohled vidět. Dá se vyřešit pomocí list comprehension s podmínkou uvedeném v předchozím čtení na doma.

1. Napište program, který na výstup vypíše součet všech ujetých kilometrů. Jistě se vám bude hodit metoda řetězců jménem `replace()`.
1. Upravte váš program tak, aby jméno souboru k otevření dostal na příkazové řádce, abychom mohli takto zpracovávat výkazy z různých souborů, aniž bychom museli upravovat samotný kód programu.
