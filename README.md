# Map of visibility overlap from popular destinations in Red River Gorge

This map is designed to show overlapping visibilities from popular hiking destinations within Red River Gorge. While this map is to serve as no replacement to the real experience, it is intended to be supplementary to what hikers can see from these destinations and where overlap from these viewpoints can occur. 

If you would like to view this map, [please click here](https://...).

## Project Contents

If you wanted to include a table of contents to sections, and then links to each section.

- [Background](#background)
- [Purpose](purpose)
- [Data Source](#data-source)
- [Creating the Map](#creating-the-map)
- [Summary](#map-summary)
- [Final Map](#final-project-link)

***

### Background

Viewshed analyses give a great understanding of visibility for analysis. Viewshed analyses can be constructed to give an understanding of what is visible from tourist attractions in national parks, such as the [observation tower](https://www.nps.gov/grsm/planyourvisit/clingmansdome.htm) which is constructed atop Clingman's Dome in Smoky Mountains National Park, or the [Grand Canyon West Skywalk](https://grandcanyonwest.com/things-to-do/skywalk/) which hangs over the Grand Canyon. Viewshed analyses can also be performed in multiple locations to give developers an understanding of where might be the best location for such tourist attractions to maximize scenic views. Viewsheds from these locations are analyzed at the respective elevation of the features, which is the additional height above ground level. 

Viewsheds can also be conducted to give the viewer an understanding of what they could see during ideal weather conditions and how far they could potentially see. Interstingly, the type of viewshed analysis conducted for this purpose gives a general understanding of what hiking destination in Red River Gorge could provide the *most* visibility in Red River Gorge. If hikers were wanting to hike to a particular location, or see a particular area within Red River Gorge, they could opt to choose a different hiking trail over others because of this. 

More information about viewshed analyses can be found [here](https://landscapearchaeology.org/2020/viewshed-tutorial/), as well as [here](https://dges.carleton.ca/CUOSGwiki/index.php/Conducting_a_Viewshed_Analysis_in_QGIS).

### Purpose

This project was intended to give the viewer an understanding of visibilities from various overlooks throughout Red River Gorge. These destinations were chosen based on popular hiking destinations as well as with the intent to show overlapping visibilities. While some locations were chosen that do not necessarily share similar visibilities, this choice was intended to provide the reader with multiple options based on the popular choice of hiking destinations in Red River Gorge. 

### Data Source

* Initial Data projection: WGS 84, NAD83 (2011) Kentucky Single Zone (EPSG 3089)
* Final Map projection: NAD83 (2011) / UTM Zone 17N (EPSG: 6346)
* County data: US Census Bureau TIGER Lines: [County TIGER Lines](https://www2.census.gov/geo/tiger/TIGER2023/COUNTY/)
* © OpenStreetMap contributors (basemap, overlook data)
* Imagery: KyFromAbove Partners [KyFromAbove webpage](https://kyfromabove.ky.gov/)

### Creating the Map

There are several steps to make this map with multiple data sources to consider. Firstly, lets start off with the toolset we will need: the visibility analysis plugin. Navigate to QGIS, and in the top-most tab selections, click plugin. In the "All" window, search for "Visibility Analysis". 

![visibility analysis plugin window](graphics/VisibilityAnalysisPlugin.JPG)
*Visibility analysis plugin window in QGIS

After that data is collected, we need to consider our source for our digital elevation model (DEM). There are several choices that can be made for DEM, but the best and easiest one available to us would be to download SRTM 30-meter DEM tiles. There happens to be an entire webpage to download this information, which can be found here: [30-Meter SRTM Tile Downloader](https://dwtkns.com/srtm30m/). I have found this source to be much easier to use than from the USGS's webpage to download the same data, as you only need to create an account to download any tile you want that covers the entire globe. Neat!

When you navigate to this webpage, you will need to create your own account. Click on your desired tile, and create your account.

![SRTM Tile](graphics/SRTM%20Tile%20Downloader.JPG)
*SRTM Tile for RRG visibility analysis*

![create account for SRTM Tile Download](graphics/URSEarthDataNasa%20Account.JPG)
*Details to create an account to download 30-meter SRTM tiles*

This step is not mandatory, but was performed for this analysis and that was to add KyFromAbove imagery data from their map server to be used directly in QGIS. The KyFromAbove program does a really great job of providing GIS data that is easy to use and download for the public. As a bonus, the resolution on the imagery for the entire state is offered at 6 inches, allowing for amazing detailf or our cartographic use!

To connect to the map server, you will need to navigate in QGIS to the Browser panel, and then right click on XYZ  Tiles -> New Connection. In the resulting window, copy and paste the URL for the KyFromAbove Map server:

 ```html
 TEST
 ```

1. **Example bold**
2. *Example italics*
3. 
4. 

### Summary

What are the key findings to take from your map and the overall mapmaking process?

## Final Project Link

Here you are linking from the README.md to the index.html.

Please view the [final map online](www.github...)