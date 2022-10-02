---
title: Čtení kódu
demand: 2
---

Popište vlastními slovy co následující výrazy udělají se zadaným seznamem
`seznam`. Až když máte ve svojí hlavjénce jasno, tak je zkuste napsat do Python
konzole a ověřte, zda jste měli pravdu.

```pycon
>>> seznam = [1, 4, 9, 16, 25, 36, 49, 64]
>>> [x**0.5 for x in seznam]
>>> [x % 2 for x in seznam]
>>> [[x // 2, x % 2] for x in seznam]
```

```pycon
>>> seznam = ['12.03.2014', '10.01.2015', '06.06.1986']
>>> [int(datum[3:5]) for datum in seznam]
>>> [int(datum[:2])-1 for datum in seznam]
>>> [[int(datum[:2]), int(datum[3:5]), int(datum[6:])] for datum in seznam]
>>> [datum.split('.') for datum in seznam]
>>> ['/'.join(datum.split('.')) for datum in seznam]
```
