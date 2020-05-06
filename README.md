# GLOBAL IMAGE COMPOSOSITING AND INDEX CALCULATIONS

Author: Simon Ramsey

Contact: simon.ramsey@unimelb.edu.au

Script: https://code.earthengine.google.com/0728ca635abb9c9e224fb1705cc3beac

### DESCRIPTION

This script for Google Earth Engine (https://code.earthengine.google.com/) can be used to produce cloud-free and atmospherically corrected satellite imagery for Landsat 5, 7, 8 and Sentinel-2 using the median pixel compositing method. This 
method takes the median pixel value across each band for the image collection over the specified
time period. This has the benefit of aiding to remove clouds (which have a high value) and 
shadows (which have a low value).

This script also calculates indices commonly used in vegetation and urban studies:
* NDVI
* EVI
* MSAVI2
* NDWI
* NDSI
* UI
* NDBI

#### NOTES
Exported single band imagery (e.g. indices) will appear greyscale when displayed in a GIS environment. Display settings can be set when opened in external software e.g. QGIS.
 
The Scan Line Corrector (SLC) on board Landsat 7 failed on May 31, 2003. Landsat 7 imagery
after this data may contain data gaps and striping.

If no imagery is produced, check that the selected dates are within the lifespan of the 
satellite platform. For Sentinel-2, top-of-atmosphere imagery has been available longer 
than surface reflectance.

### GETTING STARTED WITH GOOGLE EARTH ENGINE
New users will need to create an account (https://earthengine.google.com/new_signup/)

The Google Earth Engine interface consists of three panels and an interactive map.

The left panel contains three tabs:
* Scripts - For managing user scripts and examples.
* Docs - Documentation for Earth Engine objects and methods.
* Assets - For the upload and management of assets e.g. shapefiles.

The middle panel contains the scripting interface.

The right panel contains three tabs:
* Inspector - For querying map results
* Console - For printing output from within the script.
* Tasks - Manages import and export

#### Earth engine interface
![GEE Interface](Workspace.PNG)

The geometry tools can be used to create point, line and polygon objects.
#### Create geometry
![Create Geometry](geometry.png)

#### Import geometry
Alternatively, geometry objects can be loaded using the Asset tab in the left panel.
![Import Geometry](Assets.png)

### PROCEDURE
The user will need to set the following variables within the script:
1. Select a satellite platform
2. Select atmospheric correction
3. Select a start and end date for compositing
4. Select the polygon defining the study area boundary

#### 1. SATELLITE PLATFORMS

 PLATFORMS | Landsat 5 | Landsat 7 |  Landsat 8   |  Sentinel-2A | Sentinel-2B                             
-----------|-----------|-----------|--------------|--------------|------------
 launched: | 1984-01-01 | 1999-01-01 | 2013-04-11 | 2015-06-23 | 2017-03-28
 returned: | 2012-05-05 | active | active |  active | active
 repetition: | 16 days | 16 days | 16 days |  10 days | 10 days
 resolution: | 30 meters | 30 metres | 30 metres |  10 metres | 10 metres

Note: Sentinel-2 band resolution is 10m for visible and near infrared bands, and 20m for red-edge and short wave infrared bands

The platforms names have been shortened in the script to a letter and number combination e.g. L8 for Landsat-8. 
Enter either L5, L7, L8 or S2 as the value for the variable between the quotations to set a satellite platform. If left blank, the script defaults to Sentinel-2

![Satellite platforms](SatellitePlatform.PNG)

#### 2. SET ATMOSPHERIC CORRECTION

Select whether to use atmospherically corrected imagery.
If left blank top-of-atmosphere reflectance will be selected.

Surface reflectance imagery has been pre-processed to reduce the affects of atmosphere on imagery.
Top-of-atmosphere uses the "at sensor" imagery.
Surface reflectance imagery, if available, should better represent the actual reflectance from the earths surface.

Note: Sentinel-2 surface reflectance data is available from 2017-03-28 onwards.
Sentinel-2 top-of-atmosphere data is available from 2015-06-23 onwards.

Entering SR between the quotations uses surface reflectance imagery, if left blank top-of-atmosphere is used.
![Atmospheric Correction](ATMOS.PNG)

#### SET TIME FRAME

Set start and end dates for the composite. Seasonal or annual time frames are recommended.
Select a time frame appropriate for the satellite platform chosen. Shorter time frames
will contain more cloud cover depending on season and may contain data gaps.

Enter the chosen start and end date between the quoatations for the appropriate variables in the format "YYYY-MM-DD".
![Time Frame](TimeFrame.PNG)

#### SET STUDY AREA

Define a study area using a geometry either created within Earth Engine or uploaded as an asset.
Polygons can be created using the geometry tools in the top-left of the interactive map window. Select the polygon tool and define the corners of the polygon by clicking on the interactive map.
To use a pre-defined geometry, upload it as an asset. 
Ensure the name of the area variable matches the name of the geometry.

![Geometry](Boundary.PNG)

![Region of interest](ROI.png)


Once these four variables are set, click RUN in the top right of the scripting panel, or click Ctrl+Enter on the keyboard.

#### RESULTS
Information about the selected inputs will be displayed in the console, including the satellite platform and start and end dates for the composite imagery.

![Console](Console.PNG)

After running the script, a layers menu will appear in the top right of the interactive map window, which can be expanded by moving the mouse over it. By default, a true-colour image is displayed.

![Composite](layers.png)

Other band combinations and spectral indices can be displayed using the tickboxes and their transparency can be adjusted using the sliders. The first object on the list will be displayed on top of the objects below it.

![NDVI](NDVI.png)

#### EXPORT
To export imagery, click the highlighted tasks tab in the right panel.
![Tasks](Tasks.PNG)

Click an image file and select RUN to export.

The file parameters can be set in the panel that opens. Images can be exported directly to the associated Google Drive account. Ensure that the Scale property matches the platform that was selected.

L5, L7 and L8 = 30
S2 Composite = 10
S2 Indices = 20

The other properties define the file name and export folder.

![Export](Export.PNG)

Once complete, the imagery can be downloaded from Google Drive and opened in a GIS (e.g. QGIS).
