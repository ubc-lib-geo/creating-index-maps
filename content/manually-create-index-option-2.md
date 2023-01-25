---
layout: default
title: Manually Create an Index (Option 2)
nav_order: 9
parent: Workflows
---
# Manually create a map index for a map set with a potentially irregular grid
This tutorial uses ArcGIS Pro. QGIS also supports python scripts but this tutorial makes use of the easy usage of them in ArcGIS.
{: .note}

This guide assumes you have a map set where layers have coordinates in decimal degrees, map sheets are rectangular in shape, and are not rotated in the plane. Any of these changes will cause the scripts used to not work properly. Coordinates can be manually converted to decimal degrees or the projection can be changed in ArcGIS Pro.

1. The first step in this process is to manually enter the coordinates for the layers. Using this spreadsheet as a template, enter the coordinate pairs of the NW and SE corners of each layer in the second sheet, "Layer Coordinates"


2. Dragging down the formulas in the first sheet, **"OIM Attribute Table"**, for the fields **"label", "title", "west", "north", "east",** and **"south"** for the number of layers in the set, the entries will populate. Repeat this step for the third sheet "Array Strings for ArcGIS". Then after adding the relevant information to the OIM specification sheet, both this and the arrays needed for creation of the polygon layer are ready.

3. Following this, we must download the first and third sheets separately as **.csv** files. 

4. Now, we are ready to use ArcGIS Pro. Download the project file (!!! update link- need to upload zipped folder to github) [here](https://www.nrcan.gc.ca/earth-sciences/geography/topographic-information/maps/national-topographic-system-maps/9767), and then open it.

5. Following the steps in the "**Polygon Creation**" notebook, the first step is running the script that imports the necessary packages. For this, you have to make sure you have identified the correct location of the project folder.

6. To run the next script in the notebook, you first have to copy the values from the third sheet and paste them into empty array, "**coord_sets**"

7. The second script can now be run and should produce a polygon layer called "**polygons**"

8. Now, we must join the "**OIM Attributes Table.csv** to the polygons layer. The process for this is outlined in the notebook.

9. With the information added to the polygons layer, it is ready to export. This can either be done in ArcGIS Pro or using a combination of ArcGIS Pro and QGIS, depending on any errors ArcGIS may produce. Errors are sometimes produced when attempting to export a file to GeoJSON, and in this case, JSON should be used and then converted to GeoJSON using QGIS.
* To convert a **.json** file to **.geojson** using qgis, load the file into a new QGIS project, and then select **export** after right clicking on the layer. 

10. Following the creation of a geojson, the field names must be cleaned up. This can either be done using QGIS or [GeoJSON.io](geojson.io). 							
* In QGIS, to change the field names to their appropriate OIM specification names, rather than the ones created by ArcGIS Pro, the tool can be found by going to the **Processsing Toolbox --> Vector Table --> Rename field**.
* In GeoJSON.io, you first open the GeoJSON, then toggle to the "**table**" view and rename each field name. 




## Finished product
Once the field names have been renamed, the GeoJSON is complete! You now have a GeoJSON file with polygons representing the extent of each layer and the associated attribute information.