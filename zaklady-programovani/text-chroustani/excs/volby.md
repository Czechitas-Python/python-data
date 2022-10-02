---
title: Volby
demand: 3
---

Máme pět kandidátů na post prezidenta ČR. Následující tabulka obsahuje hlasy, které jednotliví kandidáti získali v prvním kole prezidentských voleb.

| Kraj                 | Igor Rezek | Augustýn Doležal | Vladan Bednář | Ondřej Brotz | Radim Kašpar |
| -------------------- | ---------- | ---------------- | ------------- | ------------ | ------------ |
| Hlavní město Praha   | 78774      | 43179            | 225111        | 144799       | 242854       |
| Jihočeský kraj       | 91062      | 22451            | 17475         | 53391        | 46450        |
| Jihomoravský kraj    | 179186     | 216499           | 4493          | 156305       | 61222        |
| Karlovarský kraj     | 9619       | 53476            | 926           | 64737        | 34566        |
| Kraj Vysočina        | 66904      | 85730            | 27271         | 12964        | 38041        |
| Královéhradecký kraj | 118755     | 1929             | 30426         | 25178        | 31952        |
| Liberecký kraj       | 64467      | 40993            | 81181         | 39392        | 4335         |
| Moravskoslezský kraj | 11221      | 97970            | 26179         | 98539        | 112578       |
| Olomoucký kraj       | 171064     | 7638             | 8752          | 96666        | 39738        |
| Pardubický kraj      | 74235      | 101680           | 18920         | 45904        | 1922         |
| Plzeňský kraj        | 39309      | 1505             | 10531         | 30458        | 40228        |
| Středočeský kraj     | 131584     | 1812             | 241122        | 22267        | 99326        |
| Ústecký kraj         | 194133     | 39985            | 200997        | 28229        | 20780        |
| Zlínský kraj         | 66188      | 51607            | 15977         | 177272       | 17664        |

Data máme k dispozici v následujícím formátu

```py
hlasy = [
    [78774, 43179, 225111, 144799, 242854],
    [91062, 22451, 17475, 53391, 46450],
    [179186, 216499, 4493, 156305, 61222],
    [9619, 53476, 926, 64737, 34566],
    [66904, 85730, 27271, 12964, 38041],
    [118755, 1929, 30426, 25178, 31952],
    [64467, 40993, 81181, 39392, 4335],
    [11221, 97970, 26179, 98539, 112578],
    [171064, 7638, 8752, 96666, 39738],
    [74235, 101680, 18920, 45904, 1922],
    [39309, 1505, 10531, 30458, 40228],
    [131584, 1812, 241122, 22267, 99326],
    [194133, 39985, 200997, 28229, 20780],
    [66188, 51607, 15977, 177272, 17664]
]
```

Zodpovězte následující otázky

1. Kolik získal každý kandidát hlasů v celé ČR?
1. Který kandidát vyhrál první kolo voleb?
1. Ve kterých krajích byla nejvyšší a nejnižší volební účast
1. Vytvořte tabulku, která ukazuje který kandidát vyhrál v kterém kraji.
1. Vytvořte tabulku podobnou té z tohoto cvičení, která místo čísel bude obsahovat jaké procento celkového počtu hlasů získal každý kandidát v daném kraji.

   **Nápověda:** postupuje tak, že použijete na každý řádek tabulky zvlášť chroustání seznamů. Tabulku můžete sestavit tak, že tento postup ručně zopakujete 13 krát, jednou pro každý kraj. Pokud toužíte po elegantnějším řešení, vyčkejte na nepovinné úložky.

