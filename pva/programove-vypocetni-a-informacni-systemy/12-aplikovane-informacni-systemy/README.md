# Aplikované informační systémy

Definice AIS, oblasti použití IS: Státní správa, Výroba, Zdravotnictví, Sklady a obchod. Architektury rozsáhlých informačních systémů. Metody vedení rozsáhlých projektů. Řízení provozu IS.

## Definice aplikovaných informačních sytémů (AIS)

### Informační systém (IS)

- Soubor lidí, technických prostředků a programů
- Zabezpečují sběr, přenos, zpracování a uchovávání dat za účelem prezentace informací pro potřeby uživatelů
- Vlastnosti:
    - Sada programů intergrovaných do jednoho celku
    - Slouží pro celou organizaci
    - Všichni pracují se stejnými daty
        - Důsledky
    - Obvykle software běží centrálně na serveru
        - Klient-server

### Aplikační Software

- Programové vybavení počítače, které umožňuje uživatelskou činnost
- Využívá grafické nebo textové rozhraní
- Může se skládát z několika programů

## Oblasti

### Státní správa (Veřejné zakázky)

- Zadávací dokumentace
    - Přílohy
        - Specifikace
        - Ceník
        - Návrhy smluv
- Části:
    - Vykonavatel a zadavatel (Kdo)
    - Předmět (Co)
    - Časové vymezení (Kdy)
    - Kvalifikační požadavky
        - Základní způsobilost
            - Firma platí daně
        - Profesní způsobilost
            - Živnostenský rejstřík
        - Technická kvalifikace
            - Praxe
    - Hodnotící kritéria

### Zdravotnictví

- Podsystémy
    - Péče (hospitalizace, ambulance, patologie)
    - Statistiky a přehledové systémy
    - Výkazy (pojišťovny, úřady)
    - Import dat (obrazová, laboratorní)
    - Administrace

### Sklady a obchod

- Podsystémy
    - Zboží
    - Sklad (evidence zboží, expedice)
    - Obchod (prodej, eshop)
    - Administrativa

### Životní prostředí

- Časoprostorová data
    - Senzory
    - GIS
- Agentury
    - CENIA (pod Ministerstvem životního prostředí)
    - EEA (EU)
        - Reporting směrem k EU
        - MDIAR
            - Monitoring
            - Data
            - Information
            - Assesment
            - Reporting
- Analýza
    - Legislativní předpisy
    - Reportingové povinnosti
    - Signifikantní datové zdroje

## Smlouvy

- Vývoj
- Provoz

### Smlouva na vývoj SW

- Obsah:
    - Úvodní ustanovení
        - Kontext
    - Předmět smlouvy
        - Smluvní požadavky
            - Systém
            - Tým
    - Místo a doba plnění
        - Harmonogram
    - Cena díla
    - Práva a povinnosti
        - Kontrola zákazníkem
        - Informování
    - Licenční ujednání
        - Výhradní
        - Nevýhradní
    - Ochrana informací
        - Klasifikace informací
        - Publikovatelnost
    - Záruka
    - Ostatní a závěrečná ujednání
        - Sankce
- Přílohy:
    - Definice požadavků
    - Technické požadavky

### Service-LeveL Aggreement (SLA)

- Strukturou podobná jako smlouva na vývoj
- Incident Management
    - Zajistit co nejrychlejší obnovení dostupnosti služeb
    - Minimalizovat následky výpadku
    - Odstranění provozních problémů
    - Specifikuje:
        - Servisní okna
        - Reakční doby
        - Cenu
- Change Management
    - Rozšíření nebo změny v systému
- Help-desk (Konzultace)
    - Způsoby komunikace
    - Časová okna
- Profylaxe
    - Preventivní prohlídka systému
    - Délka: dny až týdny

## Architektury rozsáhlých informačních systémů

- Požadavky:
    - Být v souladu se strategickým cíli podniku
    - Uspokojit potřebu uživatelů
    - Integrace s externími službami
    - Otevřenost ke změnám a rozšířením
    - Efektivnost
- Architektury:
    - Procesní
    - Datová:
        - ERD
    - Softwarová:
        - LL:
            - Vrstvená (MVC)
        - HL:
            - Monolitická
            - SOA
            - Microservices
    - Hardwareová

## Metody vedení rozsáhlých projektů

- Inkrementální
    - Jasně definované fáze
        - Inkrementy
    - Vodopád
    - Pros:
        - Řízení
        - Šetří čas a cenu
        - Jednodušší testování
    - Cons:
        - Potřebuje rozplánovat
        - Dobrý design
        - Změny
- Iterativní
    - V cyklech
    - Agile (SCRUM)
    - Pros:
        - Kvalita
        - Flexibilní
        - Řížení rizik
        - Spolupráce
    - Cons:
        - Plánovatelnost
        - Časová náročnost
        - Prioritizování
- Work Breakdown Structure (WBS)
    - Levely
- PERT (Program evaluation and review technique)
    - Optimistická (1)
    - Očekávaná (4)
    - Pesimistická (1)

## Řízení provozu IS

- Viz SLA
