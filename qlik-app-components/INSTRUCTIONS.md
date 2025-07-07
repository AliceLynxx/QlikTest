# Instructies voor Qlik App Componenten

## Overzicht

Deze directory bevat de unbuild componenten van de Qlik app 'test'. De app is opgedeeld in verschillende componenten die afzonderlijk kunnen worden bewerkt en beheerd via Git.

## Directory Structuur

- **script/**: Data load scripts (.qvs bestanden)
- **dimensions/**: Master dimensies (JSON bestanden)
- **measures/**: Master measures (JSON bestanden)
- **objects/**: Visualisatie objecten zoals charts, tabellen, etc. (JSON bestanden)
- **variables/**: App variabelen (JSON bestanden)
- **bookmarks/**: Bookmarks (JSON bestanden)
- **app-properties/**: App eigenschappen en metadata (JSON bestanden)

## Workflow

### 1. Wijzigingen maken
- Bewerk de relevante JSON of QVS bestanden in de juiste directory
- Test wijzigingen lokaal door de app te rebuilden

### 2. App rebuilden voor testen
```bash
# Rebuild de app met alle componenten
qlik app build --app "test-rebuild" \\
  --script qlik-app-components/script/main.qvs \\
  --dimensions qlik-app-components/dimensions/*.json \\
  --measures qlik-app-components/measures/*.json \\
  --objects qlik-app-components/objects/*.json \\
  --variables qlik-app-components/variables/*.json \\
  --bookmarks qlik-app-components/bookmarks/*.json
```

### 3. Wijzigingen committen
```bash
git add .
git commit -m "Beschrijving van wijzigingen"
git push
```

### 4. Pull Request maken
- Maak een pull request voor code review
- Test de wijzigingen in een test omgeving
- Merge na goedkeuring

## Tips

- **Backup**: Maak altijd een backup van de originele app voordat je grote wijzigingen doorvoert
- **Testing**: Test wijzigingen altijd in een aparte app voordat je ze naar productie brengt  
- **Documentatie**: Documenteer belangrijke wijzigingen in commit messages
- **Samenwerking**: Gebruik branches voor feature development om conflicten te voorkomen

## Troubleshooting

Als de rebuild niet werkt:
1. Controleer of alle benodigde bestanden aanwezig zijn
2. Valideer JSON syntax met een JSON validator
3. Controleer of de script syntax correct is
4. Zorg dat je de juiste Qlik context gebruikt

Voor meer informatie over qlik-cli commando's:
```bash
qlik app build --help
qlik app unbuild --help
```