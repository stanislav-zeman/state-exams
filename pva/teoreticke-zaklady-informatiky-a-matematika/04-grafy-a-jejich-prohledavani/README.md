# Grafy a jejich prohledávání

Typy grafů, stromy, stupně vrcholů, orientované grafy, reprezentace grafů. Algoritmy prohledávání grafu do hloubky a do šířky a jejich využití. Komponenty souvislosti.

## Grafy

- Speciální případ binárních relací

## Typy grafů

- Neorientovaný
- _G = (V, E)_
    - V: vrcholy
        - Množina vrcholy
    - E: hrany
        - E ⊆ V x V
        - Množina dvouprvkových množin vrcholů

### Kružnice

- _Cn_
- Graf má n+1 vrcholů spojených n hranami

### Cesta

- _Pn_
- Graf má n+1 vrcholů spojených "za sebou" n hranami

### Úplný

- _Kn_
- Graf má všech n vrcholů spojených hranami
    - "Každý s každým"

### Úplný bipartitní

- _Km,n_
- Graf s vrcholy ve dvou skupinách
    - Každý vrchol z jedné skupiny je spojen se všemi z druhé

### Hvězda

- _Sn_ = _K1,n_
- Speciální případ úplného bipartitního grafu

## Stromy

- Souvislý graf bez kružnic
- Les
    - Nemusí být souvislý
- Mezi každými dvě vrcholy vede právě jedna cesta
- Názvosloví:
    - Kořen: vyznačený vrchol kořenového stromu
    - Potomek x: pokud do daného vrcholu vede z kořene cesta přes x
    - List: každý vrchol bez potomků
    - Výška: největší vzdálenost z kořene do listu

## Stupně vrcholů

- Počet hran vycházejících z vrcholu
    - _dG(v)_
        - d: funkce pro vzdálenost
        - G: graf
        - v: vrchol
- Graf je _d_-regulární pokud každý vrchol má stupeň _d_

## Orientované grafy

- _G = (V, E)_
    - V: body
        - Množina vrcholů
    - E: hrany
        - E ⊆ V x V
        - Množina uspořádaných dvojic vrcholů
            - Směr zleva-doprava
- Orientované cesty a kružnice
    - Orientované varianty
- Vrcholy mají vstupní a výstupní stupeň

### Souvislost

- Slabá
    - Tradiční souvislost
    - Zapomenutí směru šipek
- Dosažitelnost
    - Graf je dosažitelný pokud existuje bod, ze kterého jsou všechny ostatní dostupné
- Silná
    - Vyžaduje existenci cest v obou směrech mezi dvojicí vrcholů

## Reprezentace grafů

- Seznam následovníků
    - Vhodné pro řídké grafy
- Matice sousednosti
    - _A = (aij)_
    - 1 pokud mají hranu, 0 jinak
    - Vhodné pro husté grafy

## Prohledávací algoritmy

- Průzkum grafu
    - Projít všechny vrcholy
    - Projít efektivně (neopakovat se)

### Do hlouby (DFS)

- Zásobník
- Atributy:
    - Color: (black, grey, white)
    - Pi: parent
    - d: distance
    - f: finished
- Postup:
```
for v in V:
    v.pi = nil
    v.d = infinity
    v.f = nil
    v.color = white
s.color = grey
s.d = 0
stack = nil
stack.Add(s)
time = 0
while stack not empty:
    u = stack.Pop()
    if existuje (u, v), že v.color = white:
        v.color = grey
        v.pi = u
        v.d = time++
        stack.Add(u)
        stack.Add(v)
    else:
        u.color = black
        u.f = time++
    
```
- Složitost: O(V + E)
- Časové značky určijí uspořádání vrcholů:
    - Preorder: podle d
    - Postorder: podle f
    - Reverse postorder: podle f ale v klesajícím pořadí
- Dosažitelnost v u i:
    - u.d < v.d < v.f < u.f

### Do šířky (BFS)

- Fronta
- Postup:
```
foreach v in V:
    v.visited = false
s.visited = true
queue = empty
queue.Add(s)
while queue not empty:
    u = queue.Pop()
    for v in u.neighbours:
        if v.visited == false:
            v.visited = true
            queue.Add(v)
```
- Složitost: O(V + E)
- Další atributy:
    - Color: (black, grey, white)
    - Pi: parent
    - D: distance
- Postup s délkou:
```
for v in V:
    v.color = black
    v.d = infinite
    v.pi = nil
s.color = grey
s.d = 0
queue = empty
queue.Add(s)
while queue not empty:
    u = queue.Pop()
    for v in u.Neighbours():
        if v.color == white:
            v.pi = u
            v.d = u.d + 1
            v.color = grey
            queue.Add(v)
        u.color = black
```
- Atributy pi definují tzv. BFS strom
    - Není určen jednoznačně záleží na pořadí vrcholů

## Komponenty souvislosti

- Jsou takové podgrafy, ve který se lze libolně pohybovat po jeho hranách mezi všemi jeho vrcholy
    - Tj. pro všechny dvojice vrcholů a, b existuje cesta z a do b
- Graf je souvislý pokud je tvořený nejvýše jednou komponentou souvislosti
