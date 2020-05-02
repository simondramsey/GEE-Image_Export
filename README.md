# GLOBAL IMAGE COMPOSOSITING AND INDEX CALCULATIONS

## DESCRIPTION

This script for Google Earth Engine can be used to produce cloud-free and atmospherically corrected satellite 
imagery for Landsat 5, 7, 8 and Sentinel-2 using the median pixel compositing method. This 
method takes the median pixel value across each band for the image collection over the specified
time period. This has the benefit of aiding to remove clouds (which have a high value) and 
shadows (which have a low value).

This script also calculates indices commonly used for vegetation and urban studies:
* NDVI
* EVI
* MSAVI
* NDWI
* NDSI
* UI
* NDBI

### NOTES
Exported single band imagery (e.g. indices) will appear greyscale when displayed in a GIS environment. Display settings can be set when opened in external software e.g. QGIS.
 
The Scan Line Corrector (SLC) on board Landsat 7 failed on May 31, 2003. Landsat 7 imagery
after this data may contain data gaps and striping.

If no imagery is produced, check that the selected dates are within the lifespan of the 
satellite platform. For Sentinel-2, top-of-atmosphere imagery has been available longer 
than surface reflectance.

## INPUTS
The user will need to:
1. Select a satellite platform
2. Select atmospheric correction
3. Select a start and end date for compositing
4. Define an area of interest using a polygon
5. Click "Run"

### SATELLITE PLATFORMS

 PLATFORMS | Landsat 5 | Landsat 7 |  Landsat 8   |  Sentinel-2A | Sentinel-2B                             
-----------|-----------|-----------|--------------|--------------|------------
 launched: | 1984-01-01 | 1999-01-01 | 2013-04-11 | 2015-06-23 | 2017-03-28
 returned: | 2012-05-05 | active | active |  active | active
 repetition: | 16 days | 16 days | 16 days |  10 days | 10 days
 resolution: | 30 meters | 30 metres | 30 metres |  10 metres | 10 metres

Note: Sentinel-2 band resolution is 10m for visible and near infrared bands, and 20m for red-edge and short wave infrared bands

### SET ATMOSPHERIC CORRECTION

Select whether to use atmospherically corrected surface reflectance imagery.
If left blank top-of-atmosphere reflectance will be selected.

Note: Sentinel-2 surface reflectance data is available from 2017-03-28 onwards.
Sentinel-2 top-of-atmosphere data is available from 2015-06-23 onwards.

### SET TIME FRAME

Set start and end dates for the composite. Seasonal or annual time frames are recommended.
Select a time frame appropriate for the satellite platform chosen. Shorter time frames
will contain more cloud cover depending on season and may contain data gaps.

### SET STUDY AREA

Define a study area using a polygon.
Polygons can be created using the geometry tools in the top-left of the map window
The polygon can be renamed (default is geometry). Doing so will require 
that the variable in brackets below is changed accordingly.
Otherwise the values below do not need to be modified.
