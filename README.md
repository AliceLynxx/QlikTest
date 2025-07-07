# QlikTest Repository

## Overzicht

Deze repository bevat de scripts en documentatie voor Qlik Sense applicaties. Het doel is om een gestructureerde manier te bieden voor versiebeheer, samenwerking en deployment van Qlik applicaties.

## Repository Structuur

```
QlikTest/
├── README.md                 # Deze documentatie
├── qlik_script.qvs          # Hoofdscript bestand van de originele Qlik applicatie
├── script.qvs               # Financiële mutaties script (nieuw toegevoegd)
├── SCRIPT_DOCUMENTATION.md  # Gedetailleerde documentatie voor script.qvs
├── TECHNICAL_DOCS.md        # Technische documentatie
├── docs/                    # Aanvullende documentatie (toekomstig)
├── data/                    # Sample data bestanden (toekomstig)
└── config/                  # Configuratie bestanden (toekomstig)
```

## Bestanden

### qlik_script.qvs
Het hoofdscript bestand dat de data loading en transformatie logica bevat voor de originele Qlik Sense applicatie. Dit bestand is ge-unbuild vanuit de 'test' applicatie in Qlik Cloud.

**Belangrijke secties:**
- **Variabelen en configuratie**: Nederlandse lokalisatie instellingen
- **Data loading sectie**: Placeholder voor data bronnen
- **Data transformatie**: Logica voor data cleaning en berekeningen
- **Kalender tabel**: Optionele tijd-dimensie tabel
- **Data kwaliteit controles**: Validatie van geladen data

### script.qvs ⭐ **NIEUW**
Een gespecialiseerd script voor het laden van financiële mutatie data. Dit bestand is gekopieerd van de lokale locatie `C:\Users\Alice Achterstraat\FilesLocal\script.qvs`.

**Kenmerken:**
- **Lokalisatie**: Engels-Amerikaanse instellingen (en-US)
- **Data bron**: QVD bestand met financiële mutaties
- **Tabel**: Mutaties_jaarbudget_en_SA met 12 velden
- **Functionaliteit**: Data Manager integratie voor tabel beheer

**Belangrijke velden in de data:**
- Jaar, Versie, Mutatie categorie
- Resultatenrekening en functiegebied informatie
- Financiële bedragen en beschrijvingen

Voor gedetailleerde informatie, zie: [SCRIPT_DOCUMENTATION.md](SCRIPT_DOCUMENTATION.md)

### SCRIPT_DOCUMENTATION.md
Uitgebreide documentatie voor het `script.qvs` bestand, inclusief:
- Volledige script analyse
- Data model beschrijving
- Implementatie instructies
- Troubleshooting gids
- Mogelijke uitbreidingen

## Gebruik

### Lokale Development
1. Clone deze repository naar je lokale machine
2. Kies het juiste script bestand voor je use case:
   - `qlik_script.qvs`: Voor algemene Qlik applicaties
   - `script.qvs`: Voor financiële mutatie data
3. Open het script bestand in Qlik Sense Desktop of upload naar Qlik Cloud
4. Pas de data bronnen aan naar je specifieke omgeving
5. Test het script en commit wijzigingen terug naar de repository

### Deployment naar Qlik Cloud

#### Voor qlik_script.qvs:
```bash
qlik app build --app "test-from-repo" --script qlik_script.qvs
```

#### Voor script.qvs:
```bash
qlik app build --app "financiele-mutaties" --script script.qvs
```

**Vereisten voor script.qvs:**
- Data connectie 'DataFiles' moet geconfigureerd zijn
- QVD bestand `Mutaties_jaarbudget_en_SA.qvd` moet beschikbaar zijn
- Toegangsrechten voor de data locatie

## Data Bronnen

### qlik_script.qvs
Bevat placeholder code voor data loading. Vervang met je eigen data bronnen:

```qlik
// Vervang deze regel met je eigen data bron
// LOAD * FROM [lib://DataConnection/data.xlsx] (ooxml, embedded labels, table is Sheet1);
```

### script.qvs
Laadt data uit een specifiek QVD bestand:

```qlik
FROM [lib://DataFiles/Mutaties_jaarbudget_en_SA.qvd] (qvd);
```

**Setup vereist:**
1. Configureer data connectie 'DataFiles'
2. Plaats QVD bestand in de juiste locatie
3. Controleer veld mapping en data kwaliteit

## Configuratie

### qlik_script.qvs - Nederlandse Lokalisatie
- Duizendtal scheidingsteken: punt (.)
- Decimaal scheidingsteken: komma (,)
- Datum formaat: D-M-YYYY
- Nederlandse maand- en dagnamen

### script.qvs - Amerikaanse Lokalisatie
- Duizendtal scheidingsteken: komma (,)
- Decimaal scheidingsteken: punt (.)
- Datum formaat: M/D/YYYY
- Geld formaat: Dollar notatie
- Engelse maand- en dagnamen

## Ontwikkeling Workflow

1. **Feature Branch**: Maak een nieuwe branch voor elke wijziging
2. **Development**: Ontwikkel en test lokaal
3. **Script Keuze**: Bepaal welk script bestand geschikt is voor je use case
4. **Data Setup**: Configureer benodigde data connecties
5. **Testing**: Test script uitvoering en data kwaliteit
6. **Commit**: Commit wijzigingen met duidelijke commit berichten
7. **Pull Request**: Maak een pull request voor code review
8. **Merge**: Merge naar main branch na goedkeuring
9. **Deploy**: Deploy naar Qlik Cloud omgeving

## Troubleshooting

### Veelvoorkomende Problemen

**Script laadt niet:**
- Controleer data connecties (vooral 'DataFiles' voor script.qvs)
- Verificeer bestandspaden en QVD beschikbaarheid
- Check toegangsrechten en authenticatie

**Data formatting problemen:**
- Controleer lokalisatie instellingen (NL vs EN-US)
- Verificeer datum/tijd formaten
- Check numerieke en geld formaten

**Performance problemen:**
- Optimaliseer data loading
- Gebruik incremental loading waar mogelijk
- Implementeer data filtering
- Overweeg QVD optimalisatie

**script.qvs specifieke problemen:**
- Controleer of DataFiles connectie bestaat
- Verificeer QVD bestand locatie en toegang
- Check veldnamen en data structuur

## Bijdragen

1. Fork de repository
2. Maak een feature branch (`git checkout -b feature/nieuwe-functionaliteit`)
3. Kies het juiste script bestand voor je wijzigingen
4. Commit je wijzigingen (`git commit -am 'Voeg nieuwe functionaliteit toe'`)
5. Push naar de branch (`git push origin feature/nieuwe-functionaliteit`)
6. Maak een Pull Request

## Documentatie

- **README.md**: Dit overzichtsdocument
- **SCRIPT_DOCUMENTATION.md**: Gedetailleerde script.qvs documentatie
- **TECHNICAL_DOCS.md**: Technische implementatie details

## Licentie

Dit project is bedoeld voor interne ontwikkeling en testing doeleinden.

## Contact

Voor vragen of ondersteuning, neem contact op via GitHub issues.

---

**Laatste update**: Toegevoegd script.qvs met financiële mutatie data loading  
**Versie**: 1.1  
**Auteur**: AliceLynxx