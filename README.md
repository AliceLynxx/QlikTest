# QlikTest Repository

Deze repository bevat de unbuild versie van de Qlik app 'test' voor versiebeheer en ontwikkeling.

## Doel

Deze repository maakt het mogelijk om:
- Qlik app componenten te beheren via Git
- Samenwerking tussen ontwikkelaars te faciliteren  
- Wijzigingen te tracken en te reviewen
- Deployment naar verschillende omgevingen te automatiseren

## Structuur

```
qlik-app-components/
├── script/          # Data load scripts (.qvs bestanden)
├── dimensions/      # Master dimensies (JSON)
├── measures/        # Master measures (JSON)
├── objects/         # Visualisatie objecten (JSON)
├── variables/       # App variabelen (JSON)
├── bookmarks/       # Bookmarks (JSON)
└── app-properties/  # App eigenschappen (JSON)
```

## Gebruik

### App rebuilden
```bash
qlik app build --app "rebuilt-test" --script qlik-app-components/script/main.qvs
```

### Wijzigingen maken
1. Bewerk de relevante JSON/QVS bestanden
2. Test lokaal met qlik app build
3. Commit en push wijzigingen
4. Maak pull request voor review

## Qlik App: test

Deze repository bevat de unbuild componenten van de Qlik app genaamd 'test'.