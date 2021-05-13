# Cargar GeoJSON
En programación, como en muchas otras áreas, no existe una solución única; es decir, es muy común encontrar diferentes procedimientos para la misma tarea. Dicho esto, es importante mencionar que hay muchas formas de cargar GeoJSONS a un mapa de Leaflet, sin embargo, creemos que el procedimiento que explicaremos a continuación, es el más amigable para personas que no están tan inmersas en la programación, debido a que es efectivo y sencillo de seguir, por supuesto, alentamos al lector a buscar nuevas formas de hacer este y cualquier otro procedimiento descrito en esta guía. 

## Para cargar nuevos archivos geojson será necesario hacer dos modificaciones en diferentes niveles del código, primero en el encabezado o “head” y segundo, en el mapa directamente, como lo habíamos estado haciendo anteriormente. 

Antes de continuar con el procedimiento, echémosle un vistazo al “encabezado” o head del código.  En la Parte 1, vimos como Cargar las librerías del mapa así como Crear un lienzo para nuestro mapa, en esta parte volveremos a editar el encabezado, justo entre las líneas de código que pertenecen justo a los capítulos antes mencionados. 

``` html
<head>
	<meta charset="utf-8">
	<title>Mapa E14C17_2</title>
	
	<!-- -----LIBRERIAS-------- -->
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css"
	integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
	crossorigin=""/>
	<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js"
	integrity="sha512-gZwIG9x3wUXg2hdXF6+rVkLF/0Vi9U8D2Ntg4Ga5I5BZpVkVxlJWbSQtXPSiUTtC0TjtGOmxa1AJPuV0CPthew=="
	crossorigin=""></script>
	
	
	<!-- -----CAPAS JSON------ -->
	
	
	<script type="text/javascript" src="DATA/json/Geología_PeñaDe Bernal_GCS.js"></script>
	
	
	
	
	<!-- -----ESTILOS DEL MAPA------ -->
	<style>
	#mapDIV {
	height: 100%;
	width: 100%;
	border: solid 2px black;
	}
	</style>
</head>
```

Por cada elemento geojson habrá que declararlo en el encabezado siguiendo la siguiente sintaxis.
1.	Abrimos una nueva etiqueta “script”
2.	En “type=” declararemos el tipo de archivo y su extensión. (siempre es la misma)
3.	En “src=” declararemos la ruta relativa donde se encuentra el archivo, separado por diagonales escribimos cada una de las subcarpetas. Y finalmente el nombre del archivo que convertimos anteriormente, incluyendo su extensión. 

``` html
<script type="text/javascript" src="DATA/json/Geología_PeñaDe Bernal_GCS.js"></script>
```
### Con este primer paso garantizamos que nuestro programa pueda localizar el archivo, en el segundo, cargaremos el archivo al mapa.

El segundo paso solamente consiste en declarar la variable en el código del mapa, siempre después de las líneas de código para las capas base. 
De igual forma, para cada elemento se deberá declarar una nueva variable, con el mismo nombre que le dimos cuando convertimos el archivo, es importante no confundir el nombre del archivo con el nombre de la variable.

Este es el nombre de la variable que usaremos en el mapa, como ves, coincide con el nombre que utilizamos al convertir el archivo, como se puede ver en el cuadro comparativo
En cuanto a la sintaxis, es la que seguimos usualmente para declarar variables.

``` html
<script>
  var geology = L.geoJson(geology).addTo(map);
</script>
```

![screenshot](https://raw.githubusercontent.com/sampach95/CargarGeoJSON/master/img/Imagen1.png )

### El código debería ser similar al siguiente



``` html
<html>
<head>
	<meta charset="utf-8">
	<title>Mapa E14C17_2</title>
	
	<!-- -----LIBRERIAS-------- -->
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css"
	integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
	crossorigin=""/>
	<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js"
	integrity="sha512-gZwIG9x3wUXg2hdXF6+rVkLF/0Vi9U8D2Ntg4Ga5I5BZpVkVxlJWbSQtXPSiUTtC0TjtGOmxa1AJPuV0CPthew=="
	crossorigin=""></script>
	
	
	<!-- -----CAPAS JSON------ -->
	
	
	<script type="text/javascript" src="DATA/json/Geología_PeñaDe Bernal_GCS.js"></script>
	
	
	
	
	<!-- -----ESTILOS DEL MAPA------ -->
	<style>
	#mapDIV {
	height: 100%;
	width: 100%;
	border: solid 2px black;
	}
	</style>
</head>

<body>
<div id="mapDIV"></div>

 <script>	
 var map = L.map('mapDIV', {
		center:[20.83748 , -99.71396],
		zoom:11
	});
	
	var scale = L.control.scale({
		'imperial':false
	});
	scale.addTo(map);
	
	var osm = L.tileLayer('http://a.tile.openstreetmap.org/{z}/{x}/{y}.png',
	{attribution: 'Map Data &copy; OpenStreetMap contributors'
	});
	osm.addTo(map);
	
	var topo = L.tileLayer('https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', {
	maxZoom: 17,
	attribution: 'Map data: &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, <a href="http://viewfinderpanoramas.org">SRTM</a> | Map style: &copy; <a href="https://opentopomap.org">OpenTopoMap</a> (<a href="https://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA</a>)'
	}); 
	topo.addTo(map);
	
	var sat = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
	attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community'
	});

	
	var basemaps = {
		"OSM": osm,
		"Topografía": topo,										
		"Satélite": sat
		};
	L.control.layers(basemaps).addTo(map);
	
	
	var geology = L.geoJson(geology).addTo(map);
	
 </script>
</body>
</html>
```
### Al ejecutar nuestro código en el navegador, deberíamos ver algo como esto.
![screenshot](https://raw.githubusercontent.com/sampach95/CargarGeoJSON/master/img/Imagen2.png )

Nota: Seguramente al cargar nueva información, dependiendo de su extensión será necesario cambiar el centro del mapa o el zoom con el que aparece predeterminadamente el mapa. Procura tener actualizada estos datos para que la visualización del mapa sea la mas adecuada. 


Siguiente Tutorial

Haz click en el siguiente enlace para volver a la pagina inicial https://github.com/sampach95/ComoCrearMapasEnLaWebConLeaflet









































































