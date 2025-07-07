# QlikTest Repository

## Overzicht

Deze repository bevat de scripts en documentatie voor de Qlik Sense applicatie 'test' die is ge-unbuild vanuit Qlik Cloud. Het doel is om een gestructureerde manier te bieden voor versiebeheer, samenwerking en deployment van Qlik applicaties.

## Repository Structuur

```
QlikTest/
├── README.md                 # Deze documentatie
├── qlik_script.qvs          # Hoofdscript bestand van de Qlik applicatie
├── docs/                    # Aanvullende documentatie (toekomstig)
├── data/                    # Sample data bestanden (toekomstig)
└── config/                  # Configuratie bestanden (toekomstig)
```

## Bestanden

### qlik_script.qvs
Het hoofdscript bestand dat de data loading en transformatie logica bevat voor de Qlik Sense applicatie. Dit bestand is ge-unbuild vanuit de originele 'test' applicatie in Qlik Cloud.

**Belangrijke secties in het script:**
- **Variabelen en configuratie**: Nederlandse lokalisatie instellingen
- **Data loading sectie**: Placeholder voor data bronnen
- **Data transformatie**: Logica voor data cleaning en berekeningen
- **Kalender tabel**: Optionele tijd-dimensie tabel
- **Data kwaliteit controles**: Validatie van geladen data

## Gebruik

### Lokale Development
1. Clone deze repository naar je lokale machine
2. Open het `qlik_script.qvs` bestand in Qlik Sense Desktop of upload naar Qlik Cloud
3. Pas de data bronnen aan naar je specifieke omgeving
4. Test het script en commit wijzigingen terug naar de repository

### Deployment naar Qlik Cloud
1. Gebruik de Qlik CLI om de applicatie te builden vanuit de repository bestanden
2. Deploy naar de gewenste Qlik Cloud omgeving
3. Configureer data connecties en beveiligingsinstellingen

## Qlik CLI Commando's

### App builden vanuit repository
```bash
qlik app build --app "test-from-repo" --script qlik_script.qvs
```

### App unbuilden naar repository
```bash
qlik app unbuild --app "app-id" --dir ./unbuild-output
```

## Data Bronnen

Het script bevat momenteel placeholder code voor data loading. Vervang de volgende secties met je eigen data bronnen:

```qlik
// Vervang deze regel met je eigen data bron
// LOAD * FROM [lib://DataConnection/data.xlsx] (ooxml, embedded labels, table is Sheet1);
```

## Configuratie

### Lokalisatie
Het script is geconfigureerd voor Nederlandse lokalisatie:
- Duizendtal scheidingsteken: punt (.)
- Decimaal scheidingsteken: komma (,)
- Datum formaat: D-M-YYYY
- Nederlandse maand- en dagnamen

### Variabelen
Alle systeem variabelen zijn gedefinieerd aan het begin van het script voor consistente data formatting.

## Ontwikkeling Workflow

1. **Feature Branch**: Maak een nieuwe branch voor elke wijziging
2. **Development**: Ontwikkel en test lokaal
3. **Commit**: Commit wijzigingen met duidelijke commit berichten
4. **Pull Request**: Maak een pull request voor code review
5. **Merge**: Merge naar main branch na goedkeuring
6. **Deploy**: Deploy naar Qlik Cloud omgeving

## Troubleshooting

### Veelvoorkomende Problemen

**Script laadt niet:**
- Controleer data connecties
- Verificeer bestandspaden
- Check toegangsrechten

**Data formatting problemen:**
- Controleer lokalisatie instellingen
- Verificeer datum/tijd formaten
- Check numerieke formaten

**Performance problemen:**
- Optimaliseer data loading
- Gebruik incremental loading waar mogelijk
- Implementeer data filtering

## Bijdragen

1. Fork de repository
2. Maak een feature branch (`git checkout -b feature/nieuwe-functionaliteit`)
3. Commit je wijzigingen (`git commit -am 'Voeg nieuwe functionaliteit toe'`)
4. Push naar de branch (`git push origin feature/nieuwe-functionaliteit`)
5. Maak een Pull Request

## Licentie

Dit project is bedoeld voor interne ontwikkeling en testing doeleinden.

## Contact

Voor vragen of ondersteuning, neem contact op via GitHub issues.

---

**Laatste update**: $(date())  
**Versie**: 1.0  
**Auteur**: AliceLynxx