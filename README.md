# Map of visibility overlap from popular destinations in Red River Gorge

This map is designed to show overlapping visibilities from popular hiking destinations within Red River Gorge. While this map is to serve as no replacement to the real experience, it is intended to be supplementary to what hikers can see from these destinations and where overlap from these viewpoints can occur. 

If you would like to view this map, [please click here](Map/RRG_Visibility_600dpi.png).

## Project Contents

- [Background](#background)
- [Purpose](#purpose)
- [Data Source](#data-source)
- [Creating the Map](#creating-the-map)
- [Summary](#summary)
- [Final Map](#final-project-link)

***

### Background

Viewshed analyses give a great understanding of visibility for analysis. Viewshed analyses can be constructed to give an understanding of what is visible from tourist attractions in national parks, such as the [observation tower](https://www.nps.gov/grsm/planyourvisit/clingmansdome.htm) which is constructed atop Clingman's Dome in Smoky Mountains National Park, or the [Grand Canyon West Skywalk](https://grandcanyonwest.com/things-to-do/skywalk/) which hangs over the Grand Canyon. Viewshed analyses can also be performed in multiple locations to give developers an understanding of where might be the best location for such tourist attractions to maximize scenic views. Viewsheds from these locations are analyzed at the respective elevation of the features, which is the additional height above ground level. 

Viewsheds can also be conducted to give the viewer an understanding of what and how far they could see during ideal weather conditions. Interstingly, the type of viewshed analysis conducted for this purpose gives a general understanding of what hiking destination in Red River Gorge could provide the *most* visibility in Red River Gorge. If hikers were wanting to hike to a particular location, or see a particular area within Red River Gorge, they could opt to choose a different hiking trail over others because of this. 

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

There are several steps to make this map with multiple data sources to consider. Firstly, lets start off with the toolset we will need: the visibility analysis plugin. If you are interested in learning more about this plugin, the GitHub repository for it can be found [here](https://github.com/zoran-cuckovic/QGIS-visibility-analysis/). Otherwise, navigate to QGIS, and in the top-most tab selections, click plugin. In the "All" window, search for "Visibility Analysis". 

![visibility analysis plugin window](graphics/VisibilityAnalysisPlugin.JPG)

*Visibility analysis plugin window in QGIS*

After the plugin is added, we need to consider our source for our digital elevation model (DEM). There are several choices that can be made for DEM, but the best and easiest one available to us would be to download SRTM 30-meter DEM tiles. There happens to be an entire webpage to download this information, which can be found here: [30-Meter SRTM Tile Downloader](https://dwtkns.com/srtm30m/). I have found this source to be much easier to use than from the USGS's webpage to download the same data, as you only need to create an account to download any tile you want that covers the entire globe. Neat!

When you navigate to this webpage, you will need to create your own account. Click on your desired tile, and create your account.

![SRTM Tile](graphics/SRTM%20Tile%20Downloader.JPG)

*SRTM Tile for RRG visibility analysis*

![create account for SRTM Tile Download](graphics/URSEarthDataNasa%20Account.JPG)

*Details to create an account to download 30-meter SRTM tiles*

This step is not mandatory, but was performed for this analysis and that was to add KyFromAbove imagery data from their map server to be used directly in QGIS. The KyFromAbove program does a really great job of providing GIS data that is easy to use for the public. As a bonus, the resolution on the imagery for the entire state is offered at 6 inches, allowing for amazing detail for our cartographic use!

To connect to the map server, you will need to navigate in QGIS to the Browser panel, and then right click on XYZ  Tiles -> New Connection. In the resulting window, copy and paste the URL for the KyFromAbove Map server:

 ```html
 https://kyraster.ky.gov/arcgis/rest/services
 ```

 Yes, in QGIS we can link to ArcGIS rest services and use data from those free sources! Great! Now we have all the KyFromAbove imagery and elevation data collected across the entire state to use for mapping. 

 ![KyFromAbove XYZ Conection](graphics/Connect%20to%20KyFromAbove%20Server.JPG)

 *KyFromAbove XYZ Connection window*

 For the toolset to work, after we add the plugin, we have to use a coordinate system whose units are in meters. So all of our data will have to be in meters, as well as our projected coordinate system. Go to the Project tab, and then click on Properties. In the CRS tab, search for EPSG 6346. This the **NAD83 (2011) / UTM zone 17N** projected coordinate system (PCS), and it happens to be a PCS with meters as the unit of measurement. This should be our best option for this analysis as far as PCS goes, but if you find another one is more suitable feel free to use that one  instead.

 This next step is *very* important for the purposes of this analysis. We need to get our DEM file into the same PCS as our project and our overlook shapefile. You **CANNOT** Export this DEM layer and save it as a new layer in the desired PCS. For some reason, when you do this, the viewshed analysis will fail to run and gives an error message of your elevation layer being in the incorrect coordinate system. Even if you do this, and you see that your DEM layer is in the PCS that you want, it will still fail when you use it in the first step of the analysis. You must use the *Warp* geoprocessing tool to get this in the correct projection. Details of this are in the below screenshot.

 ![Warp](graphics/Warp_ReprojectTool.JPG)

 *Warp (Reproject) tool window.* 

 Now we should be able to go ahead and start collecting the points for our viewshed analysis! Now if you are a connoisseur of Red River Gorge and the hiking trails in the Geological Area, you could probably pick out the spots you want with just the imagery alone. But we are going to use a combination of imagery and a great basemap to pick our spots. Feel free to add any topographic basemap layer, but for the purposes of this analysis, I chose OpenStreetMap as my basemap layer to pick the spots I want. The resulting window should look similar to the below:

 ![OSM QGIS window](graphics/OSM_QGIS%20Viewshed.JPG)

 *QGIS workspace after adding OpenStreetMap base layer and navigating to Red River Gorge*

 This is where you will need to create the points to add into your analysis. Find in QGIS the *"Add New Shapefile Layer"* button and fill out the window to be something similar to what you see below.

 ![create new shapefile](graphics/CreateNewShapefile.JPG)

 *New point shapefile with the PCS EPSG 6346*

 If you want to better keep track of the specified overlook points you want to use, add a new field and call it *Name* so you can better keep track of what overlook you want. Now, using the basemap and the added imagery, go ahead and digitize your overlooks!

 ![overlooks](graphics/OverlooksDigitized.JPG)

 *Overlooks digitized*

 As a check up, you should have the following in your QGIS Project:

 1. DEM Downloaded from the SRTM 30-meter Tile Downloader website.
 2. A reprojected DEM *using the Warp tool and **not as a new export***.
 3. Optional Imagery and OpenStreetMap (or other) basemap layer added to reference for the digitizing step.
 4. A point shapefile/layer digitized from the base layer and imagery.

 Now we can create out data for the viewshed! Since you added the *Viewshed Analysis* plugin, you have the geoprocessing tools available to you for this analysis! First, we need to create our viewpoints. In your Processing Toolbox pane, search for "*Create Viewpoints*". Fill out the tool to be similar to the following image. 

 ![Create Viewpoints Window](graphics/Create%20Viewpoints.JPG)

 *Create viewpoints window*

 A couple of things to note: radius of analysis and observer height. The radius of analysis chosen for this was five miles, which turns out is 8047 meters. This was to ensure the analysis was performed in a wide enough radius from each viewpoint so that there is sufficient overlap in the analysis. You can choose to reduce your viewpoint analysis if you'd like. 

 The observer height was chosen to be 1.8 meters, as that is the average adult height. If you were to choose an observation tower, such as the one mentioned previous in Great Smoky Mountains National Park on Clingman's Dome, you would need to set this observer height to be that of the observation tower. You could theoretically play around with this number and figure out what a 3 meter tall adult would be able to see from each viewpoint, or if there were a 15 meter observational tower at each viewpoint! More opportunities for more fun maps! For now, it is best to keep it at the average adult height since there are no towers to climb for the awesome views in Red River Gorge.

 You should have your viewpoints layer created! Feel free to save that as its own layer in your desired location. Now, it is time to create our viewshed!

 The viewshed tool outputs a raster layer that we can use to showcase the visible areas in Red River Gorge. Search for *Viewshed* in the Processing Toolbox pane. Fill in the Observer Location to be the viewpoints layer you just created, and the Digital elevation model as your DEM, in the correct PCS. 

 ![viewshed window](graphics/Viewshed.JPG)

 *Viewshed Tool*

 The *Viewshed* tool allows us to choose a couple of different analysis types, such as Depth below horizon and horizon. For this, we want a binary viewshed which allows us a raster output with the rating of being visible (0) or not visibile (1) from each viewpoint. 

 We also want to combine our multiple outputs using the Addition option. This combines what is visible between viewpoints and adds those binary values together to give a visibility rating for each pixel! The output will generate 30-meter viewshed pixels with varying pixel values. Click *Run* to execute the tool. 

 You should now have a temporary raster layer in your Layers pane! Great! We can style and edit this to be however we'd like. Feel free to choose whatever colors you want, but I would highly recommend having a similar color across a color ramp for your analysis. Below are the colors I chose based on their pixel value. 

 ![Viewshed Raster Symbology](graphics/ViewshedRasterSymbology.JPG)

 *Symbology window for the viewshed raster layer*

 You can see that the colors are all similar in that they are in the same family tree. I stuck with a light color as my first color, and then changed the values for each color to incrementally make them darker. 

 Couple of things to note: because we want to see **only** what is visible, we want to remove any pixel value of "0" from being shown on the map. You will also note that I also have the pixel value of "5" set to 100% transparent. The results I generated only provided me values from 0-4, so there was no need to symbolize 5 on the map. 

 Additionally, feel free to play around with blend modes for your map as well! This is a great way to symbolize and style raster layers in your map and can be used to spice up your maps. I wanted to use an imagery basemap in my final map, so this raster works very well with an Overlay blend mode which combines the colors in the raster with that of the next layer directly below it. The result looks similar to the below screenshot.

 ![Viewshed overlay raster](graphics/ViewshedOverlayBlend.JPG)

 *Viewshed raster with the overlay blend mode applied*

 Time to make the map! Now go to Project -> New Print Layout. Feel free to give this layout a name of your choice. This is your time to style the map how you want! Add a north arrow, label your viewpoints, and you can even add an overview map to give proper context of where your main map is located! Below is the final map for my submission.

 ![final map 300 dpi](Map/RRG_Visibility_300dpi.png)

 You can also find a link to a higher resolution map [here](Map/RRG_Visibility_600dpi.png). 
 

### Summary

Based on the analysis produced, it looks like there is a lot of overlapping visibility in Red River Gorge, no matter which hike you decide to take!

In the western-most portion of the analysis, around Courthouse Rock, Haystack Rock, and Raven Rock, there appears to be a lot of overlapping visibility from those viewpoints. In particular, there is a section west of those points which offers a lot of great views across the Red River valley inside Red River Gorge! not only, that, there are great views as you look North and East from these locations towards the eastern portion of this analysis. 

The eastern-most section, I thought, would provide the more consistent visibility overlap in this area, and it turn sout that might be true! While there does not appear to be a large amount of "4" visibility rating areas, there is a consistent amout of "2" and "3" rated areas. this means that if you decide to hike Hansen's Point, Half Moon Arch, or Chimney Top Rock, you are like to see the same things as hikers on these oppposing trails. It will just be from a different perspective!

Viewpoints from Cloud Splitter and Adena Arch were also added to analyze visibility from these areas and if there are any overlapping visbilities from Hanen's Point, Half Moon Arch, or Chimney Top Rock. Turns out, Adena Arch might only share visibilty ranges with Cloud Splitter, as there is only an overlapping visibility rating of "2" in areas south of Adena Arch. There is shared visibility north of Cloud Splitter with Adena Arch, but there is a shared visibility range with other popular hiking desintations, possibly Chimney Top Rock or Hansen's Point. 

While this is an entirely informational purpose, this gives an interesting perspective of mapping opportunities within Red River Gorge, and where you can expect to see from any one hiking destination. Now is your chance to go out and experience this magical landscape!

## Final Project Link

Here you are linking from the README.md to the index.html.

Please view the [final map online](https://Geodood19.github.io/map671FinalProject).