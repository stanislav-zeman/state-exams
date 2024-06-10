# Databáze

Relační model dat, relační schéma, klíče relačních schémat, relační algebra (projekce, selekce, agregace, přejmenování), spojování relací. Funkční závislosti, normální formy (1NF, 2NF, 3NF, Boyce-Coddova NF), vztahy mezi normálními formami. Dekompozice relačních schémat, normalizace schématu.

## Databáze

- Organizovaná kolekce dat
- Database Management System (DBMS) slouží k interakci s daty
    - Ukládání, procesování, získávaní, atd.

## Relační model dat

- Založený na predikátové logice
- Data jsou reprezentována jako n-ární relace
- Atributy popisují jednotlivé vlastnosti objektů (sloupce tabulek)
    - _A1, A2, ... An_
- Domény jsou množiny hodnot jednotlivých atributů
    - _D1, D2, ... Dn_
    - `null` hodnota je součástí každé domény
    - Relace je pak podmožina kartézského součinu domén

## Relační schéma

- Definuje schéma pro relaci
    - _R = (A1, A2, ... An)_
- Formálně je pak relace podmnožinou kartézského součinu hodnot domén
    - _R ⊆ D1 x D2 x ... Dn_
    - I.e. relace je množina n-tic
        - Nezáleží na jejich pořadí

## Klíče relačních schémat

- _K ⊆ R_

### Superklíč

- Atributy obsažené v klíči jednoznačně identifikují každý záznam relace

### Kandidátní klíč

- Takový superklíč, který je minimální
    - Tj. neobsahuje menší superklíč

### Primární klíč

- Vybraný (v ideálním případě) kandidátní klíč

### Cizí klíč

- Referencuje záznam jiné tabulky

## Relační algebra

- Formální nástroj pro dotazování a operace s relačnimi daty
- Jednotlivé dotazy se můžou vnořovat a řetězit

### Projekce

- Slouží k výběru atributů
- Π A1, A2, ... An (r)
    - A1, A2, ... An: vybrané atributy
    - r: relace
- Generalizované projekce umožňuje navíc provádět aritmetické operace nad atributy
    - Součástí rozšířené algebry

### Selekce

- Slouží v filtrování záznamů relace
- σ p (r)
    - {t | t ∈ r and p(t)}
    - p: selection predicate
        - Skládá se jednotlivých termů s operátory _<_, _=_, _>=_ atd.
        - Spojenými _and_, _or_ nebo _not_
    - r: relace

### Agregace

- Operace která z množiny hodnot vyrobí jednu
- Agregační funkce algebry:
    - avg
    - min
    - max
    - sum
    - count
- G1, ... Gn 𝒢 F1(A1), ... Fn(An) (E)
    - G1, ... Gn: atributy podle kterých záznamy shlukují
    - F1, ... Fn: agregační funkce
    - A1, ... An: atributy
- Pro jednoduchost se v rámci agregace dají výsledky agregačních funkci pojmenovat
    - Např.: _mix(salary) as min_salary_

### Přejmenování

- ρ x(A1, A2, ... An) (E)
    - E: výchozí relace nebo výraz relační algebry
    - x: jméno nové relace
    - A1, A2, ... An: nová jména atributů

### Množinové operace

- Sjednocení
    - Relace musejí mít stejnout aritu
        - Tj. stejný počet atributů
    - Domény atributů musí být kompatibilní
- Rozdíl
    - Stejné podmínky jako u sjednocení
- Průnik
    - Stejné podmínky jako u sjednocení
- Kartézský součin
    - V případě že relace obsahují stejnojmenné atributy se musejí přejmenovat
        - Tj. R ∩ S != ∅

### Přirazení

- Slouží k mazání, vkládá a aktualizaci záznamů
    - mazání: r <- r - E 
    - vkládání: r <- r ∪ E 
    - aktualizace pomocí generalizované projekce

## Spojování relací

- K spojování relací stačí kartézský součin
- Každopádně existují dodatečné operace, které v tomto ohledu snižují výřečnost:

### Přirozené spojení

- = Natural-join = Inner-join = Join
- r ⋈ s
    - r, s: relace
    - Π r.A, r.B, ... s.X (σ r.C=s.C (r x s)) 
- Vrací výsledek kartézského součinu takových záznamů, jejichž stejnojmené atributy se v obou tabulkách rovnají
- Komutativní, asociativní
- Theta join je generalizací přirozeného spojení s podmínkou
    - r ⋈θ s

### Vnější spojení

- Jde o rozšíření přirozeného spojení, které zahrnuje i nespárované záznamy
- Několik variant:
    - Levé
    - Pravé
    - Plné

## Funkční závislosti

- Definuje závislosti (omezení) mezi atributy
- α ⊆ R, β ⊆ R
- α -> β
    - Platí pro relaci právě tehdy, když hodnoty atributu alfa určují hodnoty atributu beta
        - Musí platít pro všechny záznamy relace
- Slouží k testování relací pro platnost pravidel a definování omezení
- Další závislosti lze odvozovat pomocí Armstrongových axiomů
    - Uzávěra funkčních závislostí

## Normální formy

- Popisují pravidla, která by měla jednotlivé relace splňovat

### 1NF

- Pro všechny domény relace platí, že jsou atomické
    - Tj. dále nedělitelné
    - Např.: adresa
- Pomáhá eliminovat redundanci dat

### 2NF

- Data závisí na celém klíči
- Pro všechny atributy platí, že jsou buď:
    - Součástí nějakého kandidátního klíče
    - Nebo nejsou částečně závislé na nějakém kandidátním klíči

### 3NF

- Slabší forma BCNF
- Neklíčové atributy jsou zavislé jen na klíčí a ne mezi sebou
- Pro všechny funkčí závislosti platí (α -> β), že jsou buď:
    - Triviální
    - Nebo že alfa je superklíčem relace
    - Nebo že všechny atributy v beta - alfa je součástí nějakého kandidátního klíče

### Boyce-Coddova NF

- Všechny atributy jsou zavislé jen na klíčí a ne mezi sebou
- Pro všechny funkčí závislosti platí (α -> β), že jsou buď:
    - Triviální
    - Nebo že alfa je superklíčem relace
- Ne vždy lze vytvořit tak, aby zachovala bezztrátovost i všechny závislosti

## Vztahy mezi normálními formami

- BCNF ⊂ 3NF ⊂ 2NF ⊂ 1NF

## Dekompozice relačních schémat

- Rozkládá schéma na menší
    - R = R1 ⋃ R2 ... ⋃ Rn
- Bezeztrátovost
    - Právě když r = Π R1 (r) ⋈ ... Π Rn (r) 
- Zachovává funkční závislosti
    - Právě když F+ = (F1 ⋃ F2 ... ⋃ Fn)+

## Normalizace schématu

- Proces při kterém se relace rozkládá ne menší s cílem zabránění redundance data lepší konzistence dat
- Pravidla:
    - Každá relace je v "dobré" formě
    - Dekompozice je bezeztrátová
    - Ideálně zachovává závislosti
