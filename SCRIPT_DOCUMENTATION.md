# Script.qvs Documentatie

## Overzicht

Het `script.qvs` bestand bevat een Qlik Sense data loading script dat is gekopieerd van de lokale locatie `C:\Users\Alice Achterstraat\FilesLocal\script.qvs`. Dit script is geconfigureerd voor het laden van financiële mutatie data uit een QVD bestand.

## Script Structuur

### 1. Main Tab - Systeem Configuratie

Het script begint met uitgebreide systeem instellingen voor data formatting:

```qlik
SET ThousandSep=',';
SET DecimalSep='.';
SET MoneyThousandSep=',';
SET MoneyDecimalSep='.';
SET MoneyFormat='$ ###0.00;-$ ###0.00';
```

**Configuratie Details:**
- **Lokalisatie**: Engels-Amerikaanse instellingen (en-US)
- **Numeriek formaat**: Komma als duizendtal separator, punt als decimaal
- **Geld formaat**: Dollar notatie met 2 decimalen
- **Datum formaat**: M/D/YYYY (Amerikaanse stijl)
- **Tijd formaat**: 12-uurs formaat met AM/PM
- **Week instellingen**: Week begint op zaterdag (FirstWeekDay=6)

### 2. Auto-generated Section - Data Manager

Deze sectie bevat automatisch gegenereerde code voor het beheren van tabel namen:

```qlik
Set dataManagerTables = '','Mutaties_jaarbudget_en_SA';
```

**Functionaliteit:**
- Voorkomt naam conflicten tussen tabellen
- Hernoemt bestaande tabellen indien nodig
- Ondersteunt de Qlik Sense Data Manager functionaliteit

### 3. Data Loading - Mutaties Tabel

Het hoofdgedeelte van het script laadt financiële mutatie data:

```qlik
[Mutaties_jaarbudget_en_SA]:
LOAD
    [Jaar],
    [Versie_id],
    [Versie],
    [Mut_cat_sort],
    [Mut_categorie],
    [Omschrijving],
    [Resultaat_rek_id],
    [Effect_resultatenanalyse],
    [Fonds],
    [Functie_gebied_ID],
    [Functie_gebied_omschrijving],
    [Bedrag]
FROM [lib://DataFiles/Mutaties_jaarbudget_en_SA.qvd]
(qvd);
```

## Data Model

### Tabel: Mutaties_jaarbudget_en_SA

**Doel**: Bevat financiële mutaties voor jaarbudget en structurele aanpassingen

**Velden:**

| Veld | Type | Beschrijving |
|------|------|--------------|
| Jaar | Numeriek | Boekjaar van de mutatie |
| Versie_id | ID | Unieke identifier voor de budgetversie |
| Versie | Tekst | Naam/beschrijving van de budgetversie |
| Mut_cat_sort | Numeriek | Sorteervolgorde voor mutatie categorieën |
| Mut_categorie | Tekst | Categorie van de mutatie |
| Omschrijving | Tekst | Gedetailleerde beschrijving van de mutatie |
| Resultaat_rek_id | ID | Identifier voor resultatenrekening |
| Effect_resultatenanalyse | Tekst | Impact op resultatenanalyse |
| Fonds | Tekst | Fonds waarop de mutatie betrekking heeft |
| Functie_gebied_ID | ID | Identifier voor functiegebied |
| Functie_gebied_omschrijving | Tekst | Beschrijving van het functiegebied |
| Bedrag | Numeriek | Financieel bedrag van de mutatie |

## Data Bron

**Bestand**: `Mutaties_jaarbudget_en_SA.qvd`
**Locatie**: `lib://DataFiles/`
**Formaat**: QVD (Qlik View Data)

**Vereisten:**
- Data connectie 'DataFiles' moet geconfigureerd zijn
- QVD bestand moet toegankelijk zijn via de data connectie
- Bestand moet alle verwachte velden bevatten

## Gebruik en Implementatie

### 1. Data Connectie Setup

Zorg ervoor dat de data connectie 'DataFiles' is geconfigureerd:

```qlik
// Voorbeeld data connectie configuratie
LIB CONNECT TO 'DataFiles';
```

### 2. Script Uitvoering

Het script kan worden uitgevoerd via:
- Qlik Sense Desktop: Load script functie
- Qlik Cloud: App reload
- Qlik CLI: `qlik app build` commando

### 3. Data Validatie

Na het laden van de data, controleer:
- Aantal geladen records
- Aanwezigheid van alle verwachte velden
- Data kwaliteit en consistentie

## Mogelijke Uitbreidingen

### 1. Data Transformaties

```qlik
// Voorbeeld: Datum dimensies toevoegen
[Kalender]:
LOAD
    Jaar,
    'Q' & Ceil(Month(MakeDate(Jaar,1,1))/3) as Kwartaal,
    Jaar & '-Q' & Ceil(Month(MakeDate(Jaar,1,1))/3) as JaarKwartaal
RESIDENT [Mutaties_jaarbudget_en_SA];
```

### 2. Data Kwaliteit Controles

```qlik
// Voorbeeld: Controleer op ontbrekende waarden
[DataKwaliteit]:
LOAD
    'Mutaties_jaarbudget_en_SA' as Tabel,
    Count(*) as TotaalRecords,
    Count(Bedrag) as RecordsMetBedrag,
    Count(*) - Count(Bedrag) as OntbrekendeBedraging
RESIDENT [Mutaties_jaarbudget_en_SA];
```

### 3. Berekende Velden

```qlik
// Voorbeeld: Voeg berekende velden toe
[Mutaties_jaarbudget_en_SA_Enhanced]:
LOAD
    *,
    If(Bedrag > 0, 'Positief', 'Negatief') as BedragType,
    Abs(Bedrag) as AbsoluutBedrag,
    Year(Today()) - Jaar as JarenGeleden
RESIDENT [Mutaties_jaarbudget_en_SA];

DROP TABLE [Mutaties_jaarbudget_en_SA];
```

## Troubleshooting

### Veelvoorkomende Problemen

**1. Data connectie niet gevonden**
```
Error: Connection 'DataFiles' not found
```
**Oplossing**: Configureer de DataFiles connectie in de Qlik omgeving

**2. QVD bestand niet gevonden**
```
Error: File not found: Mutaties_jaarbudget_en_SA.qvd
```
**Oplossing**: Controleer of het QVD bestand bestaat in de DataFiles locatie

**3. Veld niet gevonden**
```
Error: Field 'Bedrag' not found
```
**Oplossing**: Controleer de veldnamen in het QVD bestand

### Debug Tips

1. **Gebruik Table Viewer**: Controleer de geladen data structuur
2. **Log bestanden**: Bekijk reload logs voor gedetailleerde foutmeldingen
3. **Data profiling**: Analyseer data kwaliteit en distributie
4. **Incremental loading**: Overweeg voor grote datasets

## Versie Informatie

- **Aangemaakt**: $(date())
- **Bron**: C:\Users\Alice Achterstraat\FilesLocal\script.qvs
- **Versie**: 1.0
- **Laatst bijgewerkt**: $(date())

## Gerelateerde Bestanden

- `qlik_script.qvs`: Alternatief script bestand
- `README.md`: Algemene repository documentatie
- `TECHNICAL_DOCS.md`: Technische documentatie