# Grafové algoritmy

 Ohodnocené grafy, definice nejkratší cesty, minimální kostry grafu, algoritmy pro hledání nejkratších cest (Dijkstrův, Bellman-Fordův algoritmus) a minimálních koster v grafu.

## Ohodnocené grafy

- Navíc váhová funkce
    - w: E -> R
    - Slouží k ohodnocení hran
- Délka cesty: w(p)
    - Součet délek všech hran

## Nejkratší cesta

- Cesta je posloupnost vrcholů taková, že mezi sousedící vrcholy existuje hrana
    - Jednoduchá cesta: neobsahuje dva stejné vrcholy
- Nejkratší cesta z vrcholu u do v je taková cesta, která má nejkratší délku
- Délka cesty v neohodnoceném grafu = počet hran
- Délka nejkratší cesty: _δ(u, v)_
    - Pokud neexistuje = infinity

## Minimální kostra grafu

- Graj T je kostrou grafu G pokud:
    - T je stromem
    - _V(T) = V(G)_
        - T propojuje všechny vrcholy G
- Váha (délka) kostry je součet váh (délek) hran
- Ohodnocovací funkce
    - _w: E(G) -> reálná čísla_
- Minimální kostra je taková, která má nejmenší váhu

## Algoritmy pro hledání nejkratší cesty

### Generické SSSP

```
func init():
    for v in V:
        v.d = infinity
        v.pi = nil
    s.d = 0

func relax(u, v):
    v.d = u.v + w(u, v)
    v.pi = u

func sssp():
    init()
    M = {s}
    while m not empty:
        u = m.Pop()
        for v in u.Neightbours():
            if u.v + w(u, v) < v.d: 
                relax(u, v)
                m.push(v)
```

### Bellman-Fordův algoritmus

- Postup:
```
func BF():
    init()
    for range i-1:
        for (u, v) in E:
            if u.d + w(u, v) < v.d:
                relax()

    for (u, v) in E:
        if u.d + w(u, v) < v.d:
            return false

    return true
```
- Složitost: O(V*E)

### Dijkstrův algoritmus

- Předpoklad: graf s nezáporným ohodnocením hran
- Prioritní fronta
- Postup:
```
func D():
    init()
    q = empty
    q.Add(s)
    while q not empty:
        u = q.Pop()
        for (u, v) in E:
            if v.d == infinity:
                q.Add(v)
            if v.d > u.d + w(u, v):
                relax()
                q.Rebalance(v)
```
- Složitost:
    - Heap: O(VlogV + ElogV)
- Optimalizace:
    - Předčasné ukončení
    - Dvousměrné hledání
    - Heuristika A*
        - _v.d + h(v)_
        - Přípustnost: _h(u) <= w(u,v) + h(v)_
        - Ohodnocovací funkce: _w'(u, v) = w(u, v) - h(u) + h(v)_

## Algoritmy pro hledání minimálních koster

### Kruskalův

- Hladový postup pro minimální kostru grafu
- Postup:
    - Seřadí všechny hrany podle jejich vah
    - Inicializuje prázdnou kostru
    - Iteruje hrany a pokud hrana nevytvoří kružnici, tak ji přidá do kostry, jinak přeskočí

### Jarníkův (Primův)

- Lokální
- Předpokladem je souvislí ohodnocený graf
- Postup:
    - Inicializuje práznou kostru s jedním libovolným bodem
    - Dokud V(T) != V(G):
        - Vezme hranu _f_ nejmenší váhy s koncem _u_ (náleží V(T)) a druhám _v_ (náleží V(G) - V(T))
        - Přidá _f_ a _v_
