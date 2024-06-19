# Moderní značkovací jazyky

Základní standardy rodiny XML. Aplikace XML pro dokumenty a data. Objektový model dokumentu (DOM). Jazyky schémat (XML Schema). Navigace a dotazování v XML datech (XPath, XQuery). Transformace XML (XSLT).

## Značkovací jazyky

- Slouží k obohacení textu
    - Význam, struktura, způsob zobrazování
- XML, HTML (XHTML), TeX, LaTeX Markdown

## Standardy XML

- XML je standard popisující obecný značkovací jazyk
    - Spravován W3C
    - Předchůzcem je SGML
- XML
    - Pomocí specifikace definuje sadu pravidej pro validní dokumenty
        - Lidsky čitelné
        - Strojové zpracovatelné
- Standardy
    - DOM
    - Namespaces (Jmenné prostory)
    - XSL/XSLT
    - XLink
    - XPath
    - XML Schema

## Aplikace XML pro dokumenty a data

- Struktura
    - Logická
        - Dokument je rozdělený do elementů, atributů atd. (uzly)
    - Fyzická
        - Entity
            - Jednotlivé symboly, řetězce a soubory
- XML dokumenty být "well-formed":
    - Jeden kořenový element
    - Splňuje všechny omezení definované standardem
    - Všechny entity odkazované v dokumentu jsou opět "well-formed"
- Hlavním účel je serialiace dat
    - Ukládání, výměně a rekonstruování dat
- Uzly
    - Element (tag)
        - _<p> </p>_
    - Atribut
        - _style="xd"_
    - Text
        - _omegalul_
    - Instrukce pro zpracování
        - _<?xsl-stylesheet href="mystyle.xsl"?>_
    - Komentáře
        - _<!-- komentář -->_

## Objektový model dokumentu (DOM)

- Standard pro manipulaci s objekty
    - Opět pod W3C
- Multiplatformní a jazykové nezávislý model
    - Reprezentuje HTML/XML data jako stromovou strukturu
    - Každý uzel je objektem reprezentující část dokumentu
- Jednotlivé verze (levely)
    - Poslední 4

## Jazyky schémat (XML Schema)

- XSD (XML Schema Definition)
    - Slouží k popisu XML dokumentů
        - Verifikace
    - W3C
- Umožňuje
    - Specifikovat sadu pravidel
- Schéma
```
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    .../...
</xs:schema>
```
- Elementy
```
<xs:element name="element_name">
    <!-- here comes the type definition --
    placed either right here (so called "local")
    or as a referenced one (so called "global") -->
</xs:element>
```
- Jednoduché typy
    - Lze použít `<xs:union>` pro groupování
```
<xs:simpleType name="isbnType">
    <xs:restriction base="xs:string"> 
        <xs:pattern value="[0-9]{10}"/> 
    </xs:restriction>
</xs:simpleType>
```
- Komplexní typy
    - `<xs:sequence>` pro vydefinování pořadí elementů
    - `<xs:choice>` maximálně pouze jeden z elementů
    - `<xs:all>` všechny elementy musejí být specifikovány 
    - `<xs:group>` pro shlukování pravidel k jejich znovupoužití
    - `<xs:any>` jakékoliv elementy
- Anotace
```
<xs:annotation>
    <xs:documentation xml:lang="en">Top level element.</xs:documentation>
    <xs:documentation xml:lang="fr">Element racine.</xs:documentation>
    <xs:appinfo source="http://example.com/foo/">
        <bind xmlns="http://example.com/bar/">
            <class name="Book"/>
        </bind>
    </xs:appinfo>
</xs:annotation>
```
- Reference
```
<xs:include schemaLocation="character.xsd"/>
```

## Navigace a dotazování v XML

### XPath

- Jazyk pro adresaci XML dokumentů
    - Lze vybírat jednotlivé elementy
- W3C
- Syntax
    - Path expression
        - Posloupnost přechodů mezi sadami uzlů oddělených lomítky
            - Podobně jako cesta v adresáři
    - Context node (CN)
        - Momentálně element dotazu
    - Osy
        - `child`
            - Direct children of CN
        - `descendant` or `//`
            - All descendats
        - `parent` or `..`
            - Direct parent
        - `ancestor`
            - All ancestor nodes
        - `attribute` or `@`
        - `following`
            - All following elements
        - `preceding`
            - All preceding elements
        - `namespace`
            - All namespace nodes
        - `self` or `.`
            - The CN
    - Predikáty
        - Mohou filtrovat elementy
            - Hranaté závorky
            - `//item[@price > 2*@discount]`

### XQuery

- Dotazovací a funkcionální jazyk
    - Dotazuje a transformuje strukturovaná data
        - Nejčastěji XML
    - Spojuje XPath s operacemi známými z SQL
        - FOR
        - LET
        - WHERE
        - ORDER BY
        - RETURN
    - W3C
- Příklad
```
<html><body>
 {
   for $act in doc("hamlet.xml")//ACT
   let $speakers := distinct-values($act//SPEAKER)
   return
     <div>
       <h1>{ string($act/TITLE) }</h1>
       <ul>
       {
         for $speaker in $speakers
         return <li>{ $speaker }</li>
       }
       </ul>
     </div>
 }
 </body></html>
```

## Transformace XML (XSLT)

- XSLT = Extensible Stylesheet Language Transformations
    - Slouží k převodu dat v XML formátu do XML či jiných
- Input
    - Data v XML
    - Předpis transformace (šablona)
- Output
    - Transformovaná data
- Převod se provádí XSLT procesory
- Syntax
    - `xsl:stylesheet`
        - Root, top-level element
    - `xsl:output`
        - Child of stylesheet
        - Specifies output format etc.
    - `xsl:template`
        - Processing template
            - Body of the element contains the output
        - `match` specifies when it should be used
        - Can also be named and reused by `xsl:apply-templates`
    - `xsl:param`
        - Parameter declaration with initial value
    - `xsl:import` and `xsl:include`
        - Includes other XSLT
    - `xsl:if`
        - `test` predicate attribute
    - `xsl:choose`
        - Switch case
        - `xsl:when`
            - `test`
    - `xsl:for`
        - `select` element name
