# Terminplaner 

## Groupmembers
- Adrian Suciu (35602)
- Emircan Tutar (35606)
- Jonathan Wekesser (35483)
 
## Sources
- REST-API - Open-Meteo (https://open-meteo.com/)
- REST Errorhandling - Axio (https://www.npmjs.com/package/axios)
- Icons - fontawesome (https://fontawesome.com)
- AI support - ChatGPT (https://chat.openai.com/)

## REST-API
- Open-Meteo (https://open-meteo.com/)
- Beispiel für Wetterabfrage (https://api.open-meteo.com/v1/forecast?latitude=47.81&longitude=9.64&daily=weathercode,temperature_2m_max,temperature_2m_min,rain_sum,snowfall_sum&forecast_days=1&start_date=2023-06-12&end_date=2023-06-12&timezone=Europe%2FBerlin)

## Weather-Data
| Index    | Beschreibung                                     | Zeichen              |
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
