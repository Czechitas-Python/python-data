---
title: Hádanky
demand: 2
---

Projděte si následující program a zkuste předpovědět co nejpřesněji, jaký bude jeho výstup. Zkuste co nejvýstižněji (jednou dvěma větami) zformulovat, co program dělá.

1.

```py
cisla = [3, 5, 8, 0, 4, 2, 0, 7, 6, 2, 0, 5]
suma = 0
for cislo in cisla:
    suma = suma + cislo
    if cislo == 0:
        print(suma)
        suma = 0
```

2.

```py
cisla = [3, 5, 8, 0, 4, 2, 0, 7, 6, 2, 0, 5]
index = 0
for cislo in cisla:
    if index % 2 == 0:
        print(cislo)
    index +=  1
```
