---
title: Static Weather Dashboard
theme: dashboard
---

# Forecast

```js
const forecast = FileAttachment("./data/forecast.json").json();
```

```js
const period = forecast.properties.periods[0];
view(period);

const forecastTable = {
  "Period": period.number,
  "Start Time": period.startTime,
  "End Time": period.endTime,
  "Temperature": period.temperature,
  "Temperature Unit": period.temperatureUnit,
  "Humidity": period.relativeHumidity.value,
  "Wind": period.windSpeed,
  "Wind Direction": period.windDirection,
  "Short Forecast": period.shortForecast,
  "Detailed Forecast": period.detailedForecast
};

display(forecastTable);
```


```js
function temperaturePlot(data, {width} = {}) {
  return Plot.plot({
    title: "Hourly temperature forecast",
    width,
    x: {type: "utc", ticks: "day", label: null},
    y: {grid: true, inset: 10, label: "Degrees (F)"},
    marks: [
      Plot.lineY(data.properties.periods, {
        x: "startTime",
        y: "temperature",
        z: null, // varying color, not series
        stroke: "temperature",
        curve: "step-after"
      })
    ]
  });
}
```
<div class="grid grid-cols-2">
  <div class="card"><h2>Current Temperature</h2><h1>${forecastTable.Temperature}</h1></div>
  <div class="card"><h2>Current Wind</h2><h1>${forecastTable.Wind}</h1></div>
  <div class="card"><h1>C</h1></div>
  <div class="card"><h1>D</h1></div>
</div>

<div class="grid grid-cols-1">
  <div class="card">${resize((width) => temperaturePlot(forecast, {width}))}</div>
</div>
