# evergreen-cemetery-leadville-co
GIS files related to the Catholic Free section of Evergreen Cemetery in Leadville, CO. 

## Development: QGIS

### Data Sources
The following data sources serve as baselayers to the QGIS map & are stored in the '01-sources' folder.  Note, a more in-depth description of each data source is at the bottom of the page. 

* Base-Ortho.tif
* Evergreen-Lots.geojson
* Graves-multipoint.gpkg
* Evergreen Cemetery - export 6.csv

### QGIS Updates 
* Layer: Blocks & Lots 
	* properties -> symbology -> fill in = #efe8bb
	* properties -> symbology -> stroke = #a19b71
* Layer:  Graves
	* properties -> symbology -> categorized -> value=age_category
	* this layer shows graves that have been categorized by age group (field=age_category) -> CLASSIFY (button)

### Exporting Instructions 

* qgis2web plug-in required -> https://github.com/qgis2web/qgis2web
* export as Leaflet 

### Updates after exporting -> index.html

```html
        #map {
			position:absolute;
            width: 100%;
            height: 100%;
        }
```


```html
map.attributionControl.setPrefix('<a href="https://www.historycolorado.org/healy-house-museum-dexter-cabin" title="Click here for link to Healy House in Leadville, CO">Healy House</a> &middot; <a href="https://github.com/tomchadwin/qgis2web" target="_blank">qgis2web</a> &middot; <a href="https://leafletjs.com" title="A JS library for interactive maps">Leaflet</a> &middot; <a href="https://qgis.org">QGIS</a>');
```



## Publishing/Hosting: GitHub Pages



# Additional Information on Data Source Creation
* Base Map - ortho
	* Location: <project-directory>\01-sources\Base-Ortho.tif
* Evergreen-Lots.geojson  - 
	* a
* Graves-multipoint.gpkg
	* a
* Evergreen Cemetery - export 6.csv

	|Category|Age At Death|Color|
	|--|--|--|
	|Adult|>19|--|
	|Child|<12|--|
	|Young Person|12-19|--|
	|Other|Not enought information, missing DOB or DOD|--|