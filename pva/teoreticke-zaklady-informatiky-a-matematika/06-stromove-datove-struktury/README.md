# Stromové datové struktury

Binární vyhledávací stromy, B-stromy, červeno-černé stromy, haldy, související operace a jejich složitost. Typické implementace, příklady použití.

## Datový typ

- Rozsah hodnot
- Jednoduchý
    - Konstatní místo v paměti
- Složený
    - Statický
        - Pole
    - Dynamický
        - List, graf, strom, ...

## Binární vyhledávací stromy

### Obecný

- Datový typ pro reprezentaci množiny prvků nad kterými je definováno uspořádání
    - Kořenový strom
    - Každý uzel má max. 2 následovníky
    - Platí:
        - Klíč levého potomka je menší roven klíči rodiče
        - Klíč pravého potomka je vetší roven klíči rodiče
- Operace:
    - Search
    - Min/Max
    - Predecessor/Successor
    - Insert
    - Delete
        - Uzel nemá potomky => smazat
        - Uzel má jednoho potomka => nahrazení potomkem
        - Uzel má dva potomky => nahrazení následníkem
- Výpis klíčů:
    - Preorder
        - Nejdřív klíč rodiče
    - Inorder
        - Klíč rodiče mezi potomky
        - Vypisuje od nejmenšího k největšímu
    - Postorder
        - Poslední klíč rodiče
- Složitost:
    - Všechno O(n)

### Vyvážený

- Jde o BVS
    - Jehož hloubka je logaritmický vůči počtu ulů
    - Složitost operací je logaritmická
- Typy:
    - AVL stromy
    - 2-3 stromy
    - 2-3-4 stromy
    - B-stromy
    - Červeno-černé stromy

### Intervalové

- Rozšíření BVS
    - Atributy: low, high, max

### Radix tree

- Rozšíření BVS
- Prefixový strom
    - Řetězce

## B-stromy

- Zobecněním BVS
- Balancovaný (vyvážený)
    - Listy mají stejnou hloubku
- Uzly mohou obsahovat více klíčů
    - Uzel má K klíčů <=> má k+1 následovníků
        - Vymezuje k+1 intervalů
- Využití
    - Databázové systémy
        - Minimalizace přístupu na disk
- Minimální stupeň stromu (t)
    - Označuje dolní a horní hranici počtu klíčů v uzlu
    - Každý uzel musí obsahovat:
        - Alespoň t-1 klíčů (t následníků)
        - Maximálně 2t-1 klíčů (2t následníků)
- Výška
    - Všechny listy mají stejnou hloubku
    - h <= LOGt(n+1/2)
- Uzly
    - n: počet klíčů
    - key1, key2, ..., keyn: uspořádané klíče
    - leaf: bool
    - c1, c2, ..., cn-1: synové
    - Platí: k1 <= c1 <= k2 <= c2 ... <= cn+1
- Složitost: O(t*logtn)
- Operace:
    - Search
    - Insert
        - Postupné (preemptivní) dělení plný uzlů (n=2t-1)
    - Detele
        - Klíč v lístu => delete
        - Klíč v uzlu => nahradíme následníkem (předchůdcem)
            - Samotné mazání se děje vždy v listu
        - Nový seznam má
            - Aspoň 2t-1 klíčů => 2 nové uzly
            - Právě 2t-2 klíčů => 1 nový uzel

### B+ Stromy

- Klíče jsou pouze v listech
    - Zřetezeny v listech
    - Vnitřní uzly pouze indexují listy

## Červeno-černé stromy

- BVS kde:
    - Každý uzel má buď černou nebo červenou barvu
    - Kořen je vždy černý
    - Každý vnitřní uzel má dva syny
    - Listy nenesou hodnotu a jsou černé
    - Červený uzel má vždy černého rodiče
    - Pro každý uzel platí, že všechny cesty z něj do listů obsahují stejný počet černých uzlů
- Výška uzlu x je rovna počtu gran na nejdelší cestře z x do listu
    - Černá výška je počet černých vrcholů
    - Uzel s výškou h má alespoň černou výšku (bh) h/2
    - Každý podstrom s kořenem má alespoň 2^bh(x) - 1 uzlů
    - Strom s n vnitřními uzly má výšku nejvýš 2log2(n+1)
- Operace:
    - Search, Max, Min, Successor, Predecessor
        - Stejně jako u obecných BVS
    - Insert, Delete
        - Potřeba rotace a korekce
- Insert
    - Vlož nový uzel jako u BVS a obarvi ho červenou barvou
    - Case 1:
        - Otec je červený
        - Strýc je červený
        - Praotec černý
        - => Invertuje barvy výše zmíněných
    - Case 2:
        - Uzel je pravým synem otce
        - Otec je červený a je levým synem svého otce
        - Strýc je černý
        - Praotec je černý
        - => Proveď rotaci kolem otce doleva a pokračuje na Case 3
    - Case 3:
        - Uzel je levým synem otce
        - Otec je červený a je levým synem svého otce
        - Strýc je černý
        - Praotec je černý
        - => Proveď rotaci kolem praotce doprava a vyměň barvi praotce a strýce
- Delete
    - Smaž jako u BVS
    - Pokud je uzel červený je hotovo
    - Pokud je černý a:
        - Nemá žádného syna
        - Má jednoho syna
            - Uzel musí být černý a syn červený
            - Nahraď uzel synem
            - Syn dostane černou barvy (má dvě barvy)
        - Má dva syny
            - Vyměníme za následníka a ponechámu barvu původního uzlu
            - Pokud měl následník černou barvu, tak černý bude nově jeho pravý syn (má dvě barvy)
- Korekce
    - Uzel má černou a červenou barvu => černá
    - Uzel má dvě černé barvy a bratr je červený => levá rotace kolem otce a výměna barev mezi otcem a pracotcem
    - Uzel má dvě černé barvy a bratr a jeho synové mají černou => přesuň černou barvu do otce
    - Uzel má dvě černé barvy a bratr a jeho pravý syn jsou černí, levý syn bratra je červený => pravá rotace kolem bratra a vyměň barvy mezi původním a novým bratrem
    - Uzel má dvě černé barvy a bratr je černý a pravý syn červený => levá rotace kolem otce a barva se posune směrem ke kořenu, nový strýc je černý
- Složitost: O(logn)

### Rank

- Pořadí prvku
- Funkce
    - RBRank
        - Najde rank klíče v uzlu x
    - RBSelect
        - Najde klíč ranku i
- Princip
    - Každý uzel dostane atribut size
        - Velikost podstromu

## Haldy

- Kořenový strom
    - Stupeň vrcholu = počet jeho synů
    - Hloubka vrcholu = délka cesty z kořene
    - Výška vrcholu = nejdelší cesta do listu
    - K-tá hladina = množina vrcholů se stejnou hloubkou
- Halda
    - Stromová datová struktura
    - Pro každý užel platí, že hodnata klíče otce je >= hodnotě klíče každého syna
        - => kořen obsahuje největší hodnotu
- Binární halda
    - Úplný binární strom s vlastností haldy
        - Všechny hladiny kromě poslední jsou úplně zaplněny
        - Poslední hladina se zaplňuje zleva
- Reprezentace
    - Objekty s ukazateli
    - Pole
        - Pro uzel na indexu i
            - Levý syn: 2i + 1
            - Pravý syn: 2i + 2
            - Rodič: (i - 1) / 2
- Uspořádání
    - Heapify
        - Postupně vyhazuje vyšší hodnoty do rodiče
        - Postupuje od listů
    - Složitost: 0(h): h = hloubka stromu
