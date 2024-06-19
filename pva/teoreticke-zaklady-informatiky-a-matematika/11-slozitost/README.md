# Složitost

Složitost algoritmu versus složitost problému. Složitostní třídy (P, NP) a vztahy mezi nimi, příklady problémů z jednotlivých tříd. Těžkost a úplnost problému v dané třídě, polynomiální redukce problémů, NP-úplné úlohy.

## Složitost algoritmu versus složitost problému

- Složitost algoritmu
    - Funkce délky vstupu
        - U TS délka slova na vstupu
    - Počet kroků algoritmu
- Časová složitost
    - Funkce délky vstupu
        - TimaA(n) = max {stepsA(x) | |x| = n}
        - Nejhorší počet kroků, který algoritmus vykoná na nějakém vstupu délky n
    - Nejhorší
    - Nejlepší
    - Průměr
- Prostorová složitost (paměťová)
    - Funkce délky vstupu
        - SpaceA(n) = max {cellsA(x) | |x| = n}
        - Funkce cellsA vrací počet políček pracovní pásky, které algoritmus během výpočtu modifikoval
    - Zajímá nás extrasekvenční prostorová složitost
- Asymptotická notace
    - Ο(g): horní hranice
        - f in O(g): funkce f roste asymptoticky nejvýše rychle jako funkce g
        - Pokud existuje limita podílů funkcí a je konečná, tak f in O(g)
    - Ω(g): dolní hranice
    - Θ(g): horní i dolní hranice
- Složitost problému
    - Dána složitostí nejefektivnějšího algoritmu, která problém rozhoduje

## Složitostní třídy

### P

- Algoritmus A má nejvýše polynomiální časovou složitost (A je polynomiální), pokud existuje k in N, že TimeA(n) in O(n^k)
    - Pak problém, která tento algoritmus řeší, patří do P/PTIME
- Problémy:
    - Nejkratší cesty
    - Minimální kostra
    - Test prvočíselnosti

### NP

- Nedeterministický polynomiální čas
    - Uhádni a ověř
    - Problémy lze rychle verifikovat
        - Ale pravděpodobně nelze rychle řešit
- Definice:
    - Mějme nedeterministický algoritmus A se vstupem x
    - Počet kroků = délká nejdelšího výpočtu A nad x = stepsA(x)
- SUBSET-SUM
    - INPUT: Množina čísel a číslo
    - OUTPUT: Množina čísel jejich součet = číslo

### EXP

- Algoritmus A má nejvýše exponenciální časovou složitost, pokud existuje k in N, že TimeA(n) in O(2^n^k)
    - Pak problém, která tento algoritmus řeší, patří do EXPTIME

- P <= NP <= EXP

## Těžkost a úplnost

- C = nějaká složitostní třída (N, NP, ...)
- Těžkost
    - Problém je C-těžký, jestliže se na něj polynomiálně redukuje každý problém náležící do třídy C
- Úplnost
    - Problém je C-úplný, jestliže je C-těžký a zároveň patří do C

## Polynomiální redukce problémů

- Redukce s omezením pro výpočet TS
- Definice
    - L1 a L2
    - f: E1* -> E2*
        - f je počítana nějakým TS s polynomiální časovou složitostí
        - pro libovolné w z E1* pro které platí w in L1 => f(w) in L2
        - pro libovolné w z E1* pro které platí w not in L1 => f(w) not in L2
    - L1 <=p L2

## NP-úplné úlohy

- SAT (3-SAT)
    - Rozhodnout zda je výroková formule splnitelná
- KNAPSACK
    - INPUT: Konečná posloupnost dvojic přirozených čísel (váha, hodnota), kapacitu a threshold
    - OUTPUT: True, pokud existuje množina indexů taková, že součet vah je menší jak kaapcita a součet hodnot je větší jak threshold
- VERTEX-COVER:
    - INPUT: neorientovaný graf, přirozené číslo k
    - OUTPUT, True, pokud existuje množina vrcholů taková, že její velikost je menší než k a každá hrana je incidentní nějakému vrcholu množiny
- CLIQUE:
    - INPUT: neorientovaný graf, přirozené číslo k
    - OUTPUT: True, pokud existuje množina vrcholů taková, že její velikost je menší než k a každé dva různé vrcholy v množině jsou propojeny hranou
- Problém obchodního cestujícího
    - INPUT: orientovaný graf
    - OUTPIT: minimální kružnice v grafu, který jde přes všechny vrcholy
