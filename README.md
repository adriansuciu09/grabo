# Outdoor-Planer 

## Gruppenmitglieder
- Adrian Suciu (35602)
- Emircan Tutar (35606)
- Jonathan Wekesser (35483)

## Projektbeschreibung
Unser Outdoor-Planer kann Ihre Termine wie gewohnt mit Titel, Datum, Uhrzeit und einer Beschreibung gespeichert werden. 
<br> 
Anders jedoch als bei herkömmlichen Terminplanern, werden bei uns live Wetterdaten für den Tag des Termins geladen und können angezeigt werden.
<br>
Dies macht ihn zu einem einzigartigen Planer, der vor allem für Outdoor-Aktivitäten gedacht ist, um einen nassen Abschluss des Termins zu vermeiden. 
<br>
Bitte beachten Sie, dass aufgrund unserer REST-API nur Wetterdaten in einem Zeitraum von zwei Wochen in der Zukunft geladen werden können.
<br>
<br>
Zu unserem Outdoor-Planer geht es hier: [Outdoor-Planer](https://stupendous-sherbet-18f496.netlify.app/) 

## Sources
- REST-API - [Open-Meteo](https://open-meteo.com/)
- REST Errorhandling - [Axio](https://www.npmjs.com/package/axios)
- Icons - [fontawesome](https://fontawesome.com)
- Alert - [Sweetalert2](https://sweetalert2.github.io/)
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
| 66,67    | Freezing Rain: Light and heavy intensity         | cloud-rain+snowflake |
| 71,73,75 | Snow fall: Slight, moderate, and heavy intensity | snowflake            |
| 77       | Snow grains                                      | snowflake            |
| 80,81,82 | Rain showers: Slight, moderate, and violent      | cloud-showers-heavy  |
| 85,86    | Snow showers slight and heavy                    | snowflake            |
| 95       | Thunderstorm: Slight or moderate                 | cloud-bolt           |
| 96, 99   | Thunderstorm with slight and heavy hail          | snowflake+cloud-bolt | 


## Project setup
```
npm install
```
```
npm install axios
```
```
npm install sweetalert2
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
