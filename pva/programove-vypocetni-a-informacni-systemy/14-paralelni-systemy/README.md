# Paralelní systémy

Základní metody v návrhu paralelních algoritmů - dekompozice, mapování, komunikační primitiva. Výkonnostní analýza paralelních algoritmů. Paralelní algoritmy v prostředí se sdílenou pamětí. OpenMP standard. POSIX Threads. Lock-free přístup. Paralelní algoritmy v prostředí s distribuovanou pamětí. Message Passing Interface (MPI).

## Návrh paralelních algoritmů

### Dekompozice

- Proces rozdělení úlohy na podúlohy
    - Podúlohy je poté možné provádět paralelně
- Graf závislostí
    - Orientovaný acyklický
    - Zachycuje závislosti prováděných úloh
    - Definuje relativní pořadí úloh
- Granularita
    - Jemnost dekompozice
- Stupeň souběžnosti
    - Maximální počet úloh proveditelných souběžně
- Kritický cesta
    - Cesta grafem
    - Součet prací je na ní maximální
- Průměrný stupeň souběžnosti
    - Podíl celkového množství práce a práce na kritické cestě
- Techniky:
    - Obecné:
        - Rekurzivní (Quicksort)
        - Datová (Matice po částech)
    - Specializované:
        - Průzkumová
            - Prohledávací úlohy
            - Rozdělení podle směru hledání
            - Úloha končí v momentu nalezení
        - Spekulativní
            - Odhaduje výsledek předchozí závislé úlohy
    - Hybridní:
        - Kombinace ostatních

### Mapování

- Přiřazování úloh k jednotlých vláknům/procesům
- Ovlivňuje výkon
- Cíle:
    - Minimalizovat čas řešení
    - Maximalizovat souběžnost
    - Redukovat režii, zátěž a prodlevy
- Zadání parametrů
    - Statické
    - Dynamické

### Komunikační primitiva

- Komunikace (interakce)
    - Předávání informací mezi procesy
- Cena
    - latence + objem dat * propustnost
- Latence
    - Prodleva před doručením prvního bitu
- Přenosová rychlost
    - Objem dat za jednotku času
- Optimalizace:
    - Spojování malých zpráv
    - Komprese
    - Minimalizace vzdálenosti
    - Paketování
- Topologie:
    - Sběrnice
    - Kliky (Úplné sítě)
    - Prsten
    - Hvězdice
    - Hyperkostka (log2n-rozměrná kostka)
- Primitiva:
    - OTA Vysílání
    - ATO Redukce
    - ATA Vysílání
    - ATA Redukce
    - ATA individuální vysílání
    - ATA individuální redukce
    - Scatter
    - Gather

## Výkonnost

- Metriky
    - Čas výpočtu
        - Zrychlení
            - Tserial / Tparalel
            - Teoretická hranice (n-krát)
        - Efektivnost
            - (Tserial / Tparalel) / n
    - Cena
        - n * Tparalel

## Paralelní algoritmy se sdílenou pamětí

- Systémy SMP (Simultaneous multithreading)
    - Více procesorů
    - Více-jaderný procesor
- Procesy
    - Skrávání prostředků
    - Meziprocesová komunikace (IPC)
        - Sdílená paměť, sockety, roury
- Vlákna
    - Kontext jednoho procesu
    - Vlastní zásobkín, registry a signály
- Cache
    - Kohorence
    - Paměťové bariéry
- Problémy
    - Zamykání
        - Kritická sekce
    - Deadlock
    - Livelock (hladovění)
    - Race condition

## OpenMP

- C, C++, Fortran
- Higher-level makra pro paralelizaci
    - Pragma direktivy
```
#pragma omp direktiva [klauzule]
```

## POSIX Threads

- POSIX
    - Standard pro operační systémy
- Umožňuje správu vláken a jejich synchronizaci
- Objekty:
    - Thread
    - Mutex
    - Conditional variable
- Atributové objekty
    - `_attr_t`
- Vlákna
    - Mohou spawnovat další vlákna
        - `pthread_create`
    - Ukončení
        - `pthread_exit`
        - `pthread_cancel`
    - Dá se měnit velikost stacku
- Rozšíření POSIX
    - Bariéra
    - RWMutex

## Lock-free přístup

- Programování paralelních aplikace bez použítí zamykání
- Jedna atomická intrukce
    - HW podpora
- Compare and swap

## Paralelní algoritmy s distribuovanou pamětí

- Paradigma předávání zpráv
    - Send
    - Receive
- Operace:
    - Blokující
        - Nebufferované
            - Send skončí po přečtení receivem
        - Buffrované
            - Send skončí po kopírování do buffru
    - Neblokující
        - Nebufferované
            - Send skončí ihned, pouze se odešle požadavek na komunikaci
        - Buffrované
            - Send skončí po inicializaci přenosu

## Message Passing Interace (MPI)

- Stardard pro syntax a sémantiku komunikačních primitiv
- C, C++, Fortran
- Přes 120 funkcí
    - Inicializace
        - `MPI_Init`
    - Finalizace
        - `MPI_Finalize`
    - Komunátory
```
MPI_Send
MPI_Recv
```
- Komunikační domény
    - `MPI_Comm`
