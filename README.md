 # evergreen-cemetery-leadville-co

This repository is a companion to a map published/displayed in the several locations. The goal of this repository is to document the steps to recreate the online map. The source files are used to create a QGIS project file related to the Catholic Free section of Evergreen Cemetery in Leadville, CO.

## Map Development: QGIS
- Map development completed with QGIS version 3.34.1-Prizren
- Coordinate reference system:  WGS 84
- Spatial reference system: EPSG:4326


### Data Sources


The following data sources serve as baselayers to the QGIS map & are stored in the '01-sources' folder. Note, a more in-depth description of the data collection methods & processing are at the bottom of the page.

- Base-Ortho.tif
- Evergreen-Lots.geojson
- Graves-multipoint.gpkg
- Evergreen Cemetery - export 6.csv

### QGIS Processing

#### Layer: Blocks & Lots
- Renamed layer "Evergreen-Lots" to "Blocks & Lots"
- Properties -> symbology -> fill in = #efe8bb
- Properties -> symbology -> stroke = #a19b71

#### Layer: Graves
- Renamed layer "Graves-multipoint" to "Graves"
- Properties -> Symbology -> Categorized -> Value=age_category
- Color ramp: Spectral, then customized the colors

| Category | Color in HTML notation |
 | -- | -- |
 | Child | #ec0ee5  |
 | Young Person | #fb7e21  |
 | Adult | #a4fc3c |
 | Other | #bfc3b9  |
		
- this layer shows graves that have been categorized by age group (field=age_category) -> CLASSIFY (button)
 - Joined to " Evergreen Cemetery - export 6."
	
| Field Name 	| Field Value    |
| --- | --- |
|Join Field 	|RefID    |
|Target field |   reference_ID  |
|Custom field name prefix |j_     |          

### Exporting Instructions

- Plug-in required qgis2web (version 3.21.0)  -> https://github.com/qgis2web/qgis2web
- Tab: Layers and Groups
	- Graves 
		- Visible: YES
		- Popups: YES
			- Popup Fields. 
				- Hidden: "fid" & "reference_id"
				- All other fields: "Inline label - visible ith data"
	- Blocks & Lots
		- Visible: YES
		- Popups: NO
	- Base Map
		- Visible: YES
- Tab: Appearance
	- Title: Upper left
	- Layers list: Collapsed
	- Extent: Fit to layers extent
- Export as Leaflet.js

### Updates after exporting

#### index.html
Change the defatul to the following values: 

**Absolute Position:** 
```html
        #map {
            position:absolute;
            width: 100%;
            height: 100%;
        }
```

**Reference Links:** 
```html
map.attributionControl.setPrefix('<a href="https://www.historycolorado.org/healy-house-museum-dexter-cabin" title="Click here for link to Healy House in Leadville, CO">Healy House</a> &middot; <a href="https://github.com/tomchadwin/qgis2web" target="_blank">qgis2web</a> &middot; <a href="https://leafletjs.com" title="A JS library for interactive maps">Leaflet</a> &middot; <a href="https://qgis.org">QGIS</a>');
```

## Publishing/Hosting: GitHub Pages
- Source Code: https://github.com/mrb13/evergreen-cemetery-map
- Displayed: https://mrb13.github.io/evergreen-cemetery-map

## Data Collection & Processing

- Base Map - ortho
    - Data captured on 25-June 2023 at Evergreen Cemetery in Leadville, CO.
    - 270 photos taken with a DJI Mavic 2 drone at 380ft
    - Processed in OpenDroneMap software & exported as orthomosaic photo
- Evergreen-Lots.geojson
    
    - Evergreen Cemetery's Catholic Free (CF) section is comprised of blocks (sections) which are 17 graves long by 4-6 graves wide. Blocks with adult burials are 4 graves wide while blocks with child burials are 6 wie.
    - As of June 2023, the CF section was cordoned off by students of Professor Jim Walsh of University of Colorado Denver (https://clas.ucdenver.edu/polisci/people/james-walsh). Block are approximatly rectangular and the corner of each block had a marking post.
    - The map creator & owner of this repository has amature survey equipment used for precise coordinate collection.
        - 2 C099-F9P application boards with a ZED-F9P GNSS receiver
        - RTK corrections through connecting to UNAVCO NTRIP network (Denver).
        - All coordinates captured while in FLOAT mode
        - Acquisition software: SW Maps
        - Capture device: Android smartphone
    - Coordinate/point data processed on QGIS mapping software by translating points into polygons. Next, polygons were sub-divided into grids of either 17x4 or 17x6 based on records supplied by:
        - Professor Jim Walsh (mentioned above)
        - Lake County Public Library (https://lakecountypubliclibrary.org/localhistory/cemeteryrecords)
    - Based on the above description, the position of burial lots in this dataset are derived from survey (not a licensed surveryor) & data processing on QGIS mapping software
- Graves-multipoint.gpkg
    
    - The Graves-multipoint layer is a combination of 2 data sets:
        - Evergreen-Lots (above)
        - Evergreen Cemetery - export 6.csv (below)
    - This dataset blends/joins the spatial data of each lot & the burial data provided below
- Evergreen Cemetery - export 6.csv
    
    - Data provided by the [Rocky Mountain Irish Roots Collective](https://www.rockymountainirishrootscollective.org)
        
    - Derived fields: Year of Death, Year of Birth, Age at Death
        
    - The "age_category" field uses the following logic/groupings:
        
        | Category | Age At Death |
        | --- | --- |
        | Child | <12 |
        | Young Person | 12-19 |
        | Adult | \>19 |
        | Other | Not enought information, missing DOB or DOD |
        

### References

- [Rocky Mountain Irish Roots Collective](https://www.rockymountainirishrootscollective.org)
- [Lake County Public Library](https://lakecountypubliclibrary.org/localhistory/cemeteryrecords)