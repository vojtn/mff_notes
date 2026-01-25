# Spatial (linked) data
Questions
- how far is it
- which way to take
- where is the highest moutain
- what bus stip is near my location
- who has the largest farm
- ...

## Terminology

### Geographic information systems (GIS)
Handles everything about the space

### Geomatics
Discipline concerned with collection, distribution, storage, analysis, processing, presentation of geographic data or geographic information.

### Coordinate reference system
Framework used to precisely measure locations on, or relative to, the surface of Earth as coordinates

Reference elipsoid + Datum
+ Projection
- Conical projection
- Planar projection
- cylindrical porjects

- WGS-84
- S-JTSK
- ETRS-89

### Geodata

### Implicit geodata
- coordinates
- distances
- directions

### Explicit geodata
- reference
- address
- geographic name

### Vector/Raster representation

### Geometry objects
- Points
- Lines
- Polygons
- Multipolygons
- Surface

### Geometry representation
How to represent geometry objects in data
- usually format specific -> complicates a lot things
- depends on coordinate reference system and geometry object type

#### Well-Known Text (WKT)
- OGC standard
- Specified in Simple Features Access (https://www.opengeospatial.org/standards/sfa) and ISO 19125
- Well described in https://en.wikipedia.org/wiki/Well-known_text_representation_of_geometry
- Suitable for representation of 2D objects
- Most libraries expects WGS-84, but WKT supports various CRS

object_type(coordinates)
```
POINT (30 10)
POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))
MULTIPOINT (10 40, 40 30, 20 20, 30 10)
```

#### WKB 
Binary equivalent of WKT

#### GML
Defined in OGC standard https://www.ogc.org/standards/gml
- Very robust, supports various CRS, various geometry objects, curves, 3D
objects, coverage, sensor data
- The writing method is rather complicated (see above)

```
<gml:Point gml:id="p21" srsName="http://www.opengis.net/def/crs/EPSG/0/4326">
    <gml:coordinates>45.67, 88.56</gml:coordinates>
 </gml:Point>
```

#### Overiew based on format
| Data format | Geometry representation |
|--|--|
| GML | GML |
| GeoJson | geojson |
| Shapefile | binary |
| GeoPackage | SQLite |
| CSV | any |
| GeoSPARQL | GML/WKT |

## Spatial data formats

### GML
XML based format, described by set of XSD files
- used in the Infrastructure for Spatial INformation in Europe (INSPIRE) as the main format for data
```
<ad:Address gml:id="AD.22547665">
	<ad:inspireId>
		<base:Identifier>
			<base:localId>AD.22547665</base:localId>
			<base:namespace>CZ-00025712-CUZK_AD</base:namespace>
		</base:Identifier>
	</ad:inspireId>
	<ad:alternativeIdentifier>K Pitkovicům 1, Benice, 10300 Praha 10</ad:alternativeIdentifier>
	<ad:position>
		<ad:GeographicPosition>
			<ad:geometry>
				<gml:Point gml:id="P.AD.22547665" srsName="urn:ogc:def:crs:EPSG::5514" srsDimension="2">
					<gml:pos>-731037.56 -1053052.98</gml:pos>
				</gml:Point>
			</ad:geometry>
			<ad:specification xlink:href="http://inspire.ec.europa.eu/codelist/ GeometrySpecificationValue/entrance"
			xlink:title="entrance"/>
			<ad:default>true</ad:default>
		</ad:GeographicPosition>
	</ad:position>
	<ad:component xlink:href="#AA.MOP.108" xlink:title="Praha 10"/>
	<ad:component xlink:href="#AA.MOMC.538078" xlink:title="Praha-Benice"/>
	<ad:component xlink:href="#AA.2585" xlink:title="Benice"/>
	<ad:component xlink:href="#TF.498211" xlink:title="K Pitkovicům"/>
	<ad:component xlink:href="#PD.10300" xlink:title="10300"/>
</ad:Address>
```
### GeoJSON
- JSON based format
- Own geometry representation
- Does not support other CRS than WGS-84 (functionality was removed)
- Geometry objects supported: Point, Multipoint, LineString, MultiLineString,
Polygon, Multipolygon
- http://geojson.io
- Supported visualization in GitHub

```
{ "type": "FeatureCollection",
  "features": [
    { "type": "Feature",
      "geometry": {"type": "Point", "coordinates": [102.0, 0.5]},
      "properties": {"prop0": "value0"}
      },
    { "type": "Feature",
      "geometry": {
        "type": "LineString",
        "coordinates": [
          [102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]
          ]
        },
      "properties": {
        "prop0": "value0",
        "prop1": 0.0
        }
      },
    { "type": "Feature",
       "geometry": {
         "type": "Polygon",
         "coordinates": [
           [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0],
             [100.0, 1.0], [100.0, 0.0] ]
           ]

       },
       "properties": {
         "prop0": "value0",
         "prop1": {"this": "that"}
         }
       }
    ]
  }
```

### Shapefile
Format created by ESRI company, but the format itself is (yet) open
- Native format for most used GIS in Czech Republic
- Consist of multiple files
- Restricted number of characters per column name
- Only one feature type per dataset
- Lot of known issues


### OCG GeoPackage
SQLite database file
- Supports simple and complex geometry structures (as an attribute)
- Supports both vector and raster data (in one file)
- Very fast and very complex

### CSV
- Very easy
- MS Excel friendly
- Does not have recommended geometry (can be WKT)
- Geometry objects usually contain commas – must be escaped

## Spatial linked data formats
### Geo WGS-84
+perfectly represents points in WGS-84
-cant represent anything else

### Geo SPARQL
+Ontology + query language supporting spatial operations, Geometry representation in both GML and WKT
-may be too complicated for beginners, seems overpowered for simple representation

### GeoJSON-LD
```
{
    "@context": https://ofn.gov.cz/umístění/2020-07-
    01/kontexty/umístění.jsonld,
    "typ": "Umístění",
    "název":
    {
        "cs": "Národní park Šumava"
    },
        "geometrie":
    {
        "type": "Point",
        "coordinates": [13.6309462, 48.9720309]
    }
}
{
    "@context":
    {
        "@version": 1.1,
        "locn": "http://www.w3.org/ns/locn#",
        "dcterms": http://purl.org/dc/terms/,
        ...
        "geometrie":
        {
            "@id": "locn:geometry",
            "@context": "https://geojson.org/geojson-
            ld/geojson-context.jsonld"
        }
    }
}
```

## Spatial relations
Relation between two (or more) spatial objects, usually based on location and/or shape:

### Toplogogical
- within(a,b)
- touches(a,b)
- crosses(a,b)
- overlaps(a,b)

### Directional
- left
- right

### Distance
- closer
- further

### Temporal

## Spatial operations
- buffer
- union
- difference
- clip
- intersection
- interpolation
- distance
- convex hull
- Theissen/Voronoi


## GIS software and spatial libraries

QGIS
- very powerful open source project
https://qgis.org/en/site/

PostGIS
- Spatial Extension for PostgreSQL

ESRI ArcGIS
- large commercial project
https://www.arcgis.com/index.html

### Spatial libraries
Leaflet
- https://leafletjs.com/
- Lightweight JS library for maps
- Also as a react component

OpenLayers
- https://openlayers.org/
- JS API for maps

MapServer, GeoServer
- "heavy" solutions
- Data stored in spatial database on the server, supports wide portfolio of operations
- Usually used for serving data (as data or maps)

Geopandas
- https://geopandas.org/
- Spatial extension for wll known python library
- Also as a react component

Ogr2ogr
- https://gdal.org/
- Most used library for spatial operations and transformations
- Used by most listed software
- Runs from terminal, python, java

