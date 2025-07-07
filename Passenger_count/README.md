# Passenger Count v3 - Project Directory

## Overzicht
Deze directory bevat alle bestanden gerelateerd aan de "Passenger count v3" Qlik Sense applicatie die is geëxtraheerd uit Qlik Cloud.

## Bestanden in deze Directory

### script.qvs
Het hoofdscript bestand van de Qlik Sense applicatie. Dit bestand bevat:
- Configuratie-instellingen voor de applicatie
- Data loading logica
- Automatisch gegenereerde code voor tabel management

### SCRIPT_DOCUMENTATION.md
Uitgebreide documentatie van het script.qvs bestand, inclusief:
- Gedetailleerde uitleg van elke sectie
- Beschrijving van alle velden in de data model
- Technische opmerkingen en aanbevelingen
- Changelog en contact informatie

## Bron Applicatie
- **Naam**: Passenger count v3
- **Bron**: Qlik Cloud
- **App ID**: 6824567dcb27cb24cbe1cfb5
- **Extractie Datum**: Januari 2025
- **Extractie Methode**: Qlik CLI unbuild operatie

## Data Model
De applicatie werkt met financiële mutatie data uit het bestand `Mutaties_jaarbudget_en_SA.qvd` en bevat informatie over:
- Jaarbudget mutaties
- Situatieanalyse gegevens
- Functiegebieden en fondsen
- Financiële bedragen en categorieën

## Gebruik
1. Het script.qvs bestand kan worden gebruikt om de applicatie te rebuilden in een andere Qlik omgeving
2. De documentatie helpt bij het begrijpen van de applicatie structuur
3. Bestanden kunnen worden gebruikt voor backup, migratie of ontwikkeling

## Technische Vereisten
- Qlik Sense (Cloud of On-Premise)
- Toegang tot DataFiles library met Mutaties_jaarbudget_en_SA.qvd
- Qlik CLI voor rebuild operaties (optioneel)

## Onderhoud
- Controleer regelmatig of de data bron nog beschikbaar is
- Update documentatie bij wijzigingen aan het script
- Maak backups voordat je wijzigingen aanbrengt

## Volgende Stappen
1. Valideer dat alle benodigde data bronnen beschikbaar zijn
2. Test het script in een ontwikkelomgeving
3. Documenteer eventuele omgevingsspecifieke aanpassingen
4. Overweeg het opzetten van een geautomatiseerde deployment pipeline