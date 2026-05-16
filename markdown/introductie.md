# Introductie

Dit gedeelte beschrijft welke documenten de documentatieset bevat en hoe de RDF-ontologie is afgeleid van het MDTO metagegevensschema.

## Inhoud documentatieset
De documentatieset bestaat uit een zip met de volgende bestanden:

- mdto-rdf-1.0.ttl: De RDF-ontologie in Turtle formaat.
- mdto-rdf-1.0-shacl.ttl: SHACL validatie Shapes in Turtle formaat.
- mdto-rdf-1.0-voorbeeldset.ttl: Een bestand met voorbeeld data in Turtle formaat. 

Aanwijzing voor gebruik:

- Sla het .zip bestand op op uw computer
- Pak het .zip bestand uit en sla daarbij het bestand op op uw computer
- Open het bestand met de juiste applicatie vanuit de bestandenmap op uw computer

> **Documentatieset RDF**\
 [Download RDF ZIP (20 kB)](https://github.com/NationaalArchief/MDTO-XSD/raw/refs/heads/main/downloads/mdto-xml-voorbeelden-v1.0.1.zip)


## Toelichting op de voorbeelden
Het doel van het voorbeeld is dat de lezer zich een voorstelling kan maken hoe een bestand conform de RDF-ontologie in Turtle-formaat er uit kan zien. Het voorbeeld is zo realistisch mogelijk, maar om alle mogelijkheden te demonstreren zijn er soms waarden en combinaties van waarden gekozen die in de praktijk niet zo snel voor zullen komen. 

De volgende objecten zijn opgenomen in het voorbeeld:

- ex:InformatieobjectSerie001
Metagegevens voor de serie “Vergunningen van de gemeente 's-Gravenhage vanaf 1980”.
- ex:InformatieobjectDossier001
Metagegevens voor het dossier “Kapvergunning Hooigracht 21 Den Haag”.
- ex:InformatieobjectArchiefstuk001
Metagegevens voor het informatieobject “Verlenen kapvergunning Hooigracht 21 Den Haag” in het dossier “Kapvergunning Hooigracht 21 Den Haag”. 
- ex:Bestand001
Metagegevens voor het bestand “20090101KapvergunningHooigracht.pdf” dat de representatie is van “Verlenen kapvergunning Hooigracht 21 Den Haag”.

De hiërarchische relaties tussen de voorbeelden staan weergegeven in het hieronder getoonde schema.

![image](images/hierarchische-relaties.png)

## Verhouding MDTO metagegevensschema en de MDTO RDF-ontologie
De RDF-ontologie is op de volgende manier afgeleid van het metagegevensschema:

- Bij het beschrijven van de RDF-ontologie is ervoor gekozen om dit in Terse RDF Triple Language (Turtle) te doen. Zie hier voor meer informatie. Dit formaat wordt door veel toepassingen ondersteund en is het standaard formaat in o.a. TopBraid Composer.
- De specificatie van de ontologie maakt gebruik van een aantal andere vocabulaires met de volgende namespaces  (zie de links voor meer toelichting over de inhoud en structuur van deze vocabulaires):
  - dcterms: http://purl.org/dc/terms/
  - owl: http://www.w3.org/2002/07/owl#
  - rdf: http://www.w3.org/1999/02/22-rdf-syntax-ns#
  - rdfs: http://www.w3.org/2000/01/rdf-schema#
  - skos: http://www.w3.org/2004/02/skos/core#
  - xsd: http://www.w3.org/2001/XMLSchema#
  - sh: http://www.w3.org/ns/shacl#

- Elke klasse en gegevensgroep uit het metagegevensschema is omgezet naar een owl:Class.
- Elk attribuut is omgezet naar een owl:ObjectProperty of een owl:DatatypeProperty.  Een owl:ObjectProperty heeft altijd als bereik een andere klasse. Een owl:DatatypeProperty verwijst altijd naar een datatype.
- In RDF is het mogelijk om de specificatie van de klassen en attributen op te nemen in de ontologie. De volgende specificatie elementen (owl:annotationProperty) binnen RDF zijn gebruikt:
  - Naam: rdfs:label
  - Definitie: skos:definition
  - Domein: rdfs:domain
  - Bereik: rdfs:range
  - Doel: mdto:doel (een door mdto gedefinieerd owl:annotationProperty)
  - Regels: mdto:regels (een door mdto gedefinieerd owl:annotationProperty)
  - Toelichting: skos:scopeNote
  - Voorbeelden: skos:example

- In RDF worden de XML Schema Datatypen gebruikt, zoals bijvoorbeeld xsd:string. 
- Bij sommige elementen worden via rdfs:seeAlso links aangelegd met andere ontologieën, zoals bijvoorbeeld Dublin Core of NEN3610. Deze links hebben vooralsnog geen status binnen de ontologie. 
- Naast de RDF-ontologie is ook een bestand met SHACL Shapes beschreven. Zie hier voor meer informatie over de [Shapes Constraint Language (SHACL)](https://www.w3.org/TR/shacl/). De Shapes kunnen gebruikt worden om RDF-data te valideren. Zo wordt er o.a. gecontroleerd op de kardinaliteit (minCount, maxCount) en of een waarde het juiste bereik (bv. naam is van type xsd:string) heeft.