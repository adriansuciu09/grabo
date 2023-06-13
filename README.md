# Outdoor-Planer 

## Gruppenmitglieder
- Adrian Suciu (35602)
- Emircan Tutar (35606)
- Jonathan Wekesser (35483)
 
## TODO:
- ~~Einträge nach Datum sortieren~~
- ~~Info, dass nur 2 Wochen Wetterdaten verfügbar sind~~
- wir brauchen 4 Komponenten, haben aber 5 ... (Button in Header?)
- Wochentag + dd.mm.YYYY als Datumformat
- ? heutiges Wetter oben beim Header anzeigen?
- ~~Projektbeschreibung schreiben~~
- Warnmeldungen schöner machen (Alert ist hässlich)
- Wetterbericht ist standardmäßig für Weingarten

## Projektbeschreibung
Unser Outdoor-Planer kann Ihre Termine wie gewohnt mit Titel, Datum, Uhrzeit und einer Beschreibung gespeichert werden. 
<br> 
Anders jedoch als bei herkömmlichen Terminplanern, werden bei uns live Wetterdaten für den Tag des Termins geladen und können angezeigt werden.
<br>
Dies macht ihn zu einem einzigartigen Planer, der vor allem für Outdoor-Aktivitäten gedacht ist, um einen nassen Abschluss des Termins zu vermeiden. 
<br>
Bitte beachten Sie, dass aufgrund unserer REST-API nur Wetterdaten aus Weingarten in einem Zeitraum von zwei Wochen in der Zukunft geladen werden können. 

## Sources
- REST-API - [Open-Meteo](https://open-meteo.com/)
- REST Errorhandling - [Axio](https://www.npmjs.com/package/axios)
- Icons - [fontawesome](https://fontawesome.com)
- AI support - [ChatGPT](https://chat.openai.com/)

## Wetterdaten (Weathercode)
| Index    | Beschreibung                                     | Icon                 |
|----------|--------------------------------------------------|----------------------|
| 0,1      | Clear Sky, Mainly clear                          | sun                  |
| 2,3      | Mainly clear, partly cloudy, and overcast        | cloud-sun            |
| 45,48    | Fog and depositing rime fog                      | smog                 |
| 51,53,55 | Drizzle: Light, moderate, and dense intensity    | cloud-rain           |
| 56,57    | Freezing Drizzle: Light and dense intensity      | snow                 |
| 61,63,65 | Rain: Slight, moderate and heavy intensity       | cloud-rain           |
| 66,67    | Freezing Rain: Light and heavy intensity         | cloud-rain           |
| 71,73,75 | Snow fall: Slight, moderate, and heavy intensity | snowflake            |
| 77       | Snow grains                                      | snowflake            |
| 80,81,82 | Rain showers: Slight, moderate, and violent      | cloud-showers-heavy  |
| 85,86    | Snow showers slight and heavy                    | snowflake            |
| 95       | Thunderstorm: Slight or moderate                 | cloud-bolt           |
| 96, 99   | Thunderstorm with slight and heavy hail          | cloud-bolt           | 


## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
