# Regulární jazyky

Chomského hierarchie formálních jazyků. Regulární jazyky, jejich reprezentace a převody mezi nimi. Varianty konečných automatů. Nedeterminismus a determinizace automatů. Uzávěrové vlastnosti regulárních jazyků.

## Obecné

- Abeceda
    - Σ
    - Množina znaků/symbolů/písmen
- Slovo
    - Libovolná konečná posloupnost znaků abecedy
    - Prázdné slovo: ε
    - Počet výskytů znaku ve slově: #znak(slovo) = x
    - Množina všech slov na Σ značíme Σ*
        - E+ = E* \ { ε }
    - Zřetězení
        - Mocniny slova
            - (abc)^0 = ε 
            - (abc)^2 = abc.abc
    - Podslovo
        - u = x.v.y
            - x = ε: prefix
            - y = ε: sufix
- Jazyk
    - Libovolná množina slov nad abecedou
    - Může být nekonečný
    - Operace:
        - Sjednocení, průnik a rozdíl
        - Iterace
        - Řetězení
        - Doplněk
        - Zrcadlový obraz
- Gramatika
    - Čtveřice
        - N: neprázdná konečná množnina neterminálních symbolů (neterminály)
        - Σ: konečná množina terminálních symbolů (terminály)
        - P: konečná množina pravidel
            - Pravidlo má formu dvojice (A, B)
                - A je slovo, obsahuje aspoň jeden neterminál
        - S: počáteční neterminál (S náleží N)
        - Příklad: G = ( {sigma}, {a,b}, {sigma -> a.sigma.b, sigma -> epsilon}, sigma)
- Regulární výraz
    - Jazyk je popsatelný regulárním výrem právě když je rozpoznatelný konečným automatem
    - Regulární přechodový graf

### Automaty

- Automaty jsou ekvivalentní pokud generují stejná jazyk

- Deterministický konečný automat (DFA)
    - Q: množina stavů
    - Σ: abeceda
    - δ: Q x E -> Q (přechodová funkce)
    - s: počáteční stav
    - F: množina koncových stavů

- Nedeterministický konečný automat (NFA)
    - δ: Q x E -> 2^Q (přechodová funkce)
        - Tj. přiřazuje množinu stavů

- NFA s epsilon kroky
    - δ: Q x (E u {epsilon}) -> 2^Q (přechodová funkce)

## Chomského hierarchie

- Typ 0: Frázové gramatiky
    - Generované jazyky mohou být rozeznatelné nějakým TS
    - Bez omezení
- Typ 1: Kontextové gramatiky
    - Pro pravidla platí:
        - alfa -> beta (alfa,beta je libovolný řetězec terminálů a neterminálů)
    - Generované jazyky rozpoznatelné lineárně ohraničeným TS
- Typ 2: Bezkontextové gramatiky
    - Pro pravidla platí:
        - A -> sigma (sigma je libovolný řetězec terminálů a neterminálů)
    - Generované jazyky rozpoznatelné zásobníkovým automatem (PDA)
- Typ 3: Regulární gramatiky
    - Pro pravidla platí buď:
        - A -> aB (A,B neterminály; a terminál)
        - nebo A -> a
    - Generované jazyky rozpoznatelné konečným automatem (DFA/NFA)
    - Uzavřeny na průnik a sjednocení

## Regulární jazyky

- Jazyk je regulární pokud:
    - Je generován nějakou regulární gramatikou
    - Je akceptovaný nějakým deterministickým konečným automatem
    - Je akceptovaný nějakým nedeterministickým konečným automatem
    - Je popsán nějakým regulárním výrazem

### Převody mezi reprezentacemi

- NFA na gramatiku
- Gramatiku na NFA

## Nedeterminismus

- Přechodové funkce jednoznačně neurčují následující stav
    - Množina stavů
- Slovo je akceptování, pokud alespoň jeden z výpočtů slovo akceptuje

## Determinizace

- Odstranění epsilon kroků (Epsilon na NFA)
    - Next1
        - Pod epsilon kroky
    - Next2
        - Pod symbolem a
    - Next3
        - Pod epsilon kroky
        - Výsledné přechodové funkce
- Determinizace automatu (NFA na DFA)
    - Podmnožinová konstrukce
- Minimalizace (Minimální DFA)
    - Rozklad množiny
        - Stavy rozlišitelní slovy R1 => len(w) = 1 atd.
    - Rozlišitelnost
        - Dva stavy jsou rozlišitelné pokud platí že z a' a b' je právě jeden koncový
- Kanonizace

## Uzávěrové vlastnosti

- Sjednocení, průnik, rozdíl
    - Sychronní paralelní kompozice dvou DFA
         - Q = Q1 x Q2, atd.
    - Doplněk
        - Záměna akceptujících a neakceptujících stavů
    - Zřetězení
        - Spojení dvou DFA
    - Mocniny
        - Řetězení
    - Iterace
        - Nový stav propojených epsilon kroky
