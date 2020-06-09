---
layout: default
title: Creating index maps
nav_order: 1
has_children: yes
has_toc: false
---
<html>
<head>
<meta charset="utf-8" />
<title>Available maps 092G</title>
<meta name="viewport" content="initial-scale=1,maximum-scale=1,user-scalable=no" />
<script src="https://api.tiles.mapbox.com/mapbox-gl-js/v1.6.1/mapbox-gl.js"></script>
<link href="https://api.tiles.mapbox.com/mapbox-gl-js/v1.6.1/mapbox-gl.css" rel="stylesheet" />
<style>
	body { margin: 0; padding: 0;}
	#map { height: 400px; width: 100%;}
	#map canvas {cursor: crosshair;}
	#features {
			position: absolute;
			top: 0;
			left: 0;
			bottom: 0;
			width: 20%;
			overflow: auto;
			background: rgba(255, 255, 255, 0.8);}
</style>
</head>
<body>
# Creating map indexes

This content is meant to help staff at UBC Library understand index maps, and to direct work toward creating digital index maps for some of our map collections using the OpenIndexMap content format standard.

For more information about the what a map index is and their importance in map collections see ["What are index maps?"](content/what-are-index-maps.md)

## Converting UBC inventories
We are extending previous work done at UBC to create 'inventories' of large paper map collections. These inventories were assembled over years of work to create complete listings for our unique holdings of maps. In most cases, these inventories - formatted on .xlsx spreadsheets - consist of thousands of items with many attributes. We are first cleaning these spreadsheets with OpenRefine, removing any macros or special characters, and formatting them to meet OpenIndexMap content format standards. Then we will create new geodata from these files that allow us to spatially query and visualize our holdings. These files can also be shared with other libraries participating in the OpenIndexMaps community such as Stanford, Cornell, UC Berkeley, UC Santa Barbara, and many others.

With standardized, digital map indexes, we can begin to build applications to help us make our paper collections more discoverable through discovery interfaces like GeoBlacklight (see: Geodisy).

Below is an example web map listing all available map sheets for a particular location in Southern BC.

<div id="map"></div>
<pre id="features"></pre>
<script>
	mapboxgl.accessToken = 'pk.eyJ1IjoiZWN0MTIzIiwiYSI6ImNqeGY4aDUyYzA0aGwzem9qdnNmcjdnMm0ifQ.ecFxH-JpYwPn4x3rKNs6Fg';


var map = new mapboxgl.Map({
		container: 'map',
		zoom: 6,
		center: [-125.193328, 50.506185],
		style: 'mapbox://styles/ect123/ck4ym048y4upi1cmzoq53immx'
});
map.scrollZoom.disable();
map.addControl(new mapboxgl.NavigationControl());
map.on('load', function() {

  map.addLayer({
    'id': '092poly',
    'type': 'fill',
    'source': {
      'type': 'geojson',
      'data': '092-50k-available.geojson'
      },
    'layout': {},
		'paint': {
			'fill-color': '#FF8484',
			'fill-opacity': 0,
			'fill-outline-color': 'black'
		},
	});

	map.addLayer({
    'id': '092poly-line',
    'type': 'line',
    'source': {
      'type': 'geojson',
      'data': 'content/092-50k-available.geojson'
      },
    'layout': {},
		'paint': {
			'line-color': 'black',
			'line-color': 'black',
			'line-width': .75
		},
	});

});
map.on('mousemove', function(e) {
var features = map.queryRenderedFeatures(e.point, {layers: ['092poly']});

var displayProperties = ['properties'];

var displayFeatures = features.map(function(feat) {
		var displayFeat = {};
			displayProperties.forEach(function(prop) {
				displayFeat[prop] = feat[prop];
				});
			return displayFeat;
				});

document.getElementById('features').innerHTML = JSON.stringify(displayFeatures, null, 2)
});
</script>

</body>
</html>
