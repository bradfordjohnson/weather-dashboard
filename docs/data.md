---
title: Data
toc: true
---

## Forecast location

<figure class="wide">
  <div id="map" style="height: 400px; margin: 1rem 0; border-radius: 8px;"></div>
  <figcaption>Weather data location.</figcaption>
</figure>


```js
const map = L.map(document.querySelector("#map"));
const tile = L.tileLayer(`https://tile.openstreetmap.org/{z}/{x}/{y}.png`, {attribution: '© <a href="https://www.mapbox.com/feedback/">Mapbox</a> © <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'}).addTo(map);
const geo = L.geoJSON().addData(forecast).addTo(map);
map.fitBounds(geo.getBounds(), {padding: [50, 50]});
invalidation.then(() => map.remove());
```

```js
const forecast = FileAttachment("./data/forecast.json").json();
```

## Raw data object

```js
display(forecast);
```