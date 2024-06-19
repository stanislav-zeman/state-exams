# Rozhodnutelnost

Pojem algoritmického problému a algoritmu. Turingův stroj a problém zastavení. Rozhodnutelnost a částečná rozhodnutelnost, nerozhodnutelnost. Metoda redukce.

## Algoritmický problém a algoritmus

- Problém
    - Dvojice
        - Input (kolekce matematických objektů; doména)
        - Output (funkce s očekávaným chování)
- Rozhodovací problém
    - Out(x) = True/False
        - Pozitivní a negativní instance

## Turingův stroj

- Sedmice
    - Q: konečná množina stavů
    - Σ: vstupní abeceda
    - Γ: pásková abeceda
        - Obsahuje navíc od vstupní abecedy
            - Levou koncovou zarážku: |>
            - Prázdné pole: _
    - δ: Q x Γ -> Q x Γ x {+1, -1, 0, _|_}
    - s: počáteční stav
    - qacc: akceptující stav
    - qrej: zamítající stav
- Slova jsou
    - Akceptována
        - Výpočet je konečný a poslední konfigurace je ve stavu qacc
    - Zamítána
        - Výpočet je konečný a poslední konfigurace je ve stavu qrej
    - Nebo TS cyklí
        - Výpočet je nekonečný
- Konfigurace (stav stroje)
    - s: aktulání stav (s in Q)
    - alfa: posloupnost symbolů z paskové abecedy (stav pásky)
    - i: přirozené čislo (aktuální pozice čtecí hlavy)
- Počáteční konfigurace
    - (s, |>w_*, 0)
- Terminální konfigurace
    - (t, alfa, i): t in {qacc, qrej} nebo nelze přejít do žádné konfigurace
- Výpočet
    - Posloupnost konfigurací (i nekonečná)
- Church-Turingova teze
    - Každý proces, který lze nazvat algoritmem se dá realizovat na Turingově stroji
- Rozšíření:
    - Nedeterministický
    - K-páskový
- Funkce počítaná TS je funkce taková, že pro libovolné slovo:
    - Pokud TS zastaví na slově, tak f(slovo) je zapsáno na pásce
    - Pokud TS cyklí na slově, f(slovo) = _|_

## Problém zastavení

- Nerozhodnutelný problém
- HALT
    - INPUT: TS a slovo w
    - OUTPUT: True pokud TS zastaví nad w

## Rozhodnutelnost

- Problém je rozhodnutelný, jestliže existuje TS, který ho rozhoduje
- TS rozhoduje problém v případě, že:
    - Slovo je buď zamítnuto
    - Nebo je akceptováno

## Částečná rozhodnutelnost

- Jestliže existuje TS který:
    - Pokud slovo patří do jazyk, tak ho TS akceptuje
    - Pokud slovo nepatří do jazyka, tak je buď zamítnuto nebo TS cyklí
- HALT je částečně rozhodnutelný
- Jeli jazyk a jeho doplněk částečně rozhodnutelný, pak je rozhodnutelný

## Nerozhodnutelnost

- Problém je nerozhodnutelný právě když není rozhodnutelný
- Kromě HALTU
    - CFG-EQUIVALENCE
        - Dvě bezkontextové gramatiky generují stejný jazyk
    - GRAMMAR-EMPTINESS
        - Gramatika typu 0 generuje prázdný jazyk

## Redukce

- Dva problémy P1(INPUT1, OUTPUT1), P2(INPUT2, OUTPUT2)
- Funkce je redukcí P1 na P2, pokud f: INPUT1 -> INPUT2 a platí:
    - Funkce f je počítána algoritmem který vždy zastaví
    - Pozitivní instance se mapujou na pozitivní instance
    - Negativní instance se mapujou na negativní instance
- Problém P1 se redukuje na P2 (P1 <= P2), pokud existuje redukce problému P1 na P2
- Když P1 <= P2:
    - P2 je rozhodnutelný => pak P1 je rozhodnutelný
    - P2 je částečně rozhodnutelný => pak P1 je částečně rozhodnutelný
    - P1 není rozhodnutelný => pak P2 není rozhodnutelný
    - P1 není částečně rozhodnutelný => pak P2 není částečně rozhodnutelný
- Problém L:
    - Chceme ukázat rozhodnutelnost L => L zredukujeme na nějaký rozhodnutelný problém
    - Chceme ukázat nerozhodnutelnost L => nějaký nerozhodnutelný problém zredukujeme na L
