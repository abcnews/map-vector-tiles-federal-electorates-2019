map-vector-tiles-federal-electorates-2019
=========================================

2019 Federal Electorate boundaries as vector tiles. 

Compatible with [Mapbox GL JS](https://github.com/mapbox/mapbox-gl-js) and [Maplibre GL JS](https://github.com/MapLibre/maplibre-gl-js).

Files generated with [Tippecanoe](https://github.com/mapbox/tippecanoe) on a geojson file.



Details
-------

* layer: `federalelectorates2019`
* fields:
  * `name` (string, e.g. "Adelaide")
  * `code` (string, e.g. "adel")
* minzoom: `0`
* maxzoom: `9`
* bounds: `[96.816948, -43.658562, 167.998035, -9.219937]` (West, South, East, North)


Example usage
-------------

```javascript
let bounds = new maplibregl.LngLatBounds([[112, -44], [156, -10]]); // Australia
let center = bounds.getCenter();
map = new maplibregl.Map({
  container: 'map',
  center: center,
  zoom: 6,
  style: 'https://www.example.com/style.json'
});
map.fitBounds(bounds, { 'padding': 5 });
map.on('load', () => {
  map.addSource('electorates', {
    'type': 'vector',
    'tiles': [
      'https://www.abc.net.au/res/sites/news-projects/map-vector-tiles-federal-electorates-2019/{z}/{x}/{y}.pbf'
    ],
    'minzoom': 0,
    'maxzoom': 9,
    'bounds': [96.816948, -43.658562, 167.998035, -9.219937]
  });
  map.addLayer({
    'id': 'electorates_fill',
    'type': 'fill',
    'source': 'electorates',
    'source-layer': 'federalelectorates2019',
    'paint': {
      'fill-color': '#009900',
      'fill-opacity': 0.5
    }
  });
  map.addLayer({
  'id': 'electorates_line',
  'type': 'line',
  'source': 'electorates',
  'source-layer': 'federalelectorates2019',
  'paint': {
    'line-color': '#000',
    'line-opacity': 0.2,
    "line-width": {
      'stops': [ 
        [0, 0.5], 
        [6, 0.5], 
        [10, 1], 
        [15, 2] 
      ]
    },
  }
});
```