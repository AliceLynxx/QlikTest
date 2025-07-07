# Passenger Count v3 - Script Documentatie

## Overzicht
Dit document bevat uitgebreide documentatie voor het Qlik Sense script van de "Passenger count v3" applicatie. Het script is geëxtraheerd uit Qlik Cloud en bevat configuratie-instellingen en data-laadlogica voor het analyseren van passagiersaantallen.

## Script Structuur

### Tab 1: Main
Deze sectie bevat de hoofdconfiguratie-instellingen voor de Qlik Sense applicatie.

#### Numerieke en Datum Formaten
```qvs
SET ThousandSep=',';
SET DecimalSep='.';
SET MoneyThousandSep=',';
SET MoneyDecimalSep='.';
SET MoneyFormat='$ ###0.00;-$ ###0.00';
```
**Doel**: Definieert hoe getallen, decimalen en valuta worden weergegeven
- Duizendtalscheidingsteken: komma (,)
- Decimaalscheidingsteken: punt (.)
- Valutaformaat: Dollar notatie met 2 decimalen

#### Tijd en Datum Configuratie
```qvs
SET TimeFormat='h:mm:ss TT';
SET DateFormat='M/D/YYYY';
SET TimestampFormat='M/D/YYYY h:mm:ss[.fff] TT';
```
**Doel**: Standaardisatie van tijd- en datumweergave
- Tijdformaat: 12-uurs notatie met AM/PM
- Datumformaat: Amerikaanse notatie (MM/DD/YYYY)
- Timestamp: Combinatie met optionele milliseconden

#### Kalender Instellingen
```qvs
SET FirstWeekDay=6;
SET BrokenWeeks=1;
SET ReferenceDay=0;
SET FirstMonthOfYear=1;
```
**Doel**: Configuratie van kalender logica
- Eerste dag van de week: Zaterdag (6)
- Gebroken weken toegestaan
- Referentiedag: Zondag (0)
- Eerste maand van het jaar: Januari (1)

#### Lokalisatie
```qvs
SET CollationLocale='en-US';
SET CreateSearchIndexOnReload=1;
```
**Doel**: Taal- en zoekfunctionaliteit
- Lokalisatie: Engels (Verenigde Staten)
- Zoekindex wordt automatisch aangemaakt bij reload

#### Maand- en Dagnamen
```qvs
SET MonthNames='Jan;Feb;Mar;Apr;May;Jun;Jul;Aug;Sep;Oct;Nov;Dec';
SET LongMonthNames='January;February;March;April;May;June;July;August;September;October;November;December';
SET DayNames='Mon;Tue;Wed;Thu;Fri;Sat;Sun';
SET LongDayNames='Monday;Tuesday;Wednesday;Thursday;Friday;Saturday;Sunday';
```
**Doel**: Definieert korte en lange namen voor maanden en dagen in het Engels

#### Numerieke Afkortingen
```qvs
SET NumericalAbbreviation='3:k;6:M;9:G;12:T;15:P;18:E;21:Z;24:Y;-3:m;-6:μ;-9:n;-12:p;-15:f;-18:a;-21:z;-24:y';
```
**Doel**: Definieert hoe grote getallen worden afgekort (k=duizend, M=miljoen, etc.)

### Tab 2: Auto-generated section
Deze sectie bevat automatisch gegenereerde code voor het beheren van tabelnamen en het laden van data.

#### Tabel Naam Management
```qvs
Set dataManagerTables = '','Mutaties_jaarbudget_en_SA';
```
**Doel**: Definieert welke tabellen door de Data Manager worden beheerd

#### Conflict Resolutie Logic
```qvs
For each name in $(dataManagerTables) 
    Let index = 0;
    Let currentName = name; 
    Let tableNumber = TableNumber(name); 
    Let matches = 0; 
    Do while not IsNull(tableNumber) or (index > 0 and matches > 0)
        index = index + 1; 
        currentName = name & '-' & index; 
        tableNumber = TableNumber(currentName) 
        matches = Match('$(currentName)', $(dataManagerTables));
    Loop 
    If index > 0 then 
            Rename Table '$(name)' to '$(currentName)'; 
    EndIf; 
Next;
```
**Doel**: Voorkomt naamconflicten door automatisch tabelnamen te hernoemen
- Controleert of tabelnaam al bestaat
- Voegt numerieke suffix toe indien nodig (-1, -2, etc.)
- Hernoemt conflicterende tabellen

#### Data Loading
```qvs
Unqualify *;

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

## Data Model Beschrijving

### Tabel: Mutaties_jaarbudget_en_SA
Deze tabel bevat financiële mutaties gerelateerd aan jaarbudget en situatieanalyse.

#### Velden Beschrijving:

| Veld | Type | Beschrijving |
|------|------|-------------|
| Jaar | Numeriek | Het jaar waarop de mutatie betrekking heeft |
| Versie_id | Numeriek | Unieke identifier voor de versie |
| Versie | Tekst | Versie beschrijving |
| Mut_cat_sort | Numeriek | Sorteervolgorde voor mutatie categorieën |
| Mut_categorie | Tekst | Categorie van de mutatie |
| Omschrijving | Tekst | Gedetailleerde beschrijving van de mutatie |
| Resultaat_rek_id | Numeriek | Identifier voor resultatenrekening |
| Effect_resultatenanalyse | Tekst | Effect op de resultatenanalyse |
| Fonds | Tekst | Fonds waarop de mutatie betrekking heeft |
| Functie_gebied_ID | Numeriek | Identifier voor functiegebied |
| Functie_gebied_omschrijving | Tekst | Beschrijving van het functiegebied |
| Bedrag | Numeriek | Financieel bedrag van de mutatie |

### Data Bron
- **Bestand**: Mutaties_jaarbudget_en_SA.qvd
- **Locatie**: lib://DataFiles/
- **Formaat**: QVD (Qlik View Data)

## Technische Opmerkingen

### Performance Optimalisatie
- Gebruik van QVD bestanden voor snelle data loading
- Unqualify * statement voor eenvoudige veldnamen
- Automatische zoekindex creatie ingeschakeld

### Onderhoud
- Script is gedeeltelijk auto-generated door Qlik Data Manager
- Handmatige wijzigingen in de "Auto-generated section" kunnen worden overschreven
- Configuratie-instellingen in de "Main" tab kunnen veilig worden aangepast

### Aanbevelingen
1. **Backup**: Maak altijd een backup voordat je wijzigingen aanbrengt
2. **Testing**: Test wijzigingen in een ontwikkelomgeving
3. **Documentatie**: Documenteer handmatige wijzigingen
4. **Versioning**: Gebruik versiebeheer voor script wijzigingen

## Changelog
- **Versie 1.0**: Initiële extractie uit Qlik Cloud "Passenger count v3" applicatie
- **Datum**: Januari 2025
- **Bron**: Qlik Cloud unbuild operatie

## Contact
Voor vragen over dit script, neem contact op met de Qlik ontwikkelaar of data analist verantwoordelijk voor de "Passenger count v3" applicatie.