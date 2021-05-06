---
layout: default
title: Manually create an index
nav_order: 8
parent: Workflows
---
Information about how to manually create a non-rectilinear index is coming soon!
<!--
Open QGIS and select **New Empty Project**.
Click on the data file you want to import and drag it into the **Layers** box in the lower left of the screen.
If applicable, select the appropriate transformation to the desired Coordinate Reference System and click **OK**.
Your screen should look similar to this:
![1:1m index of Canada NTS map series](index_CA_1m.png)
[Set layer and project CRS]
Next, we will create and overlay a spatial grid which subdivides each bounding box into quarters. In order to run the algorithm, we must first determine (1) the extent of the geographic area of interest and (2) the horizontal and vertical spacing between the boundaries of features. For our example, the geographic extent of Canada ranges from -48 to -144 degrees longitude and from 40 to 88 degrees north latitude. While the vertical spacing will remain the same, at 2 degrees latitude, as a result of Canada's far-northern extent, its horizontal spacing changes from 4 degrees longitude to 8 in the High Arctic (80 to 88 degrees north). This means we will have to create two grids--one from 40-80 deg lat, the other from 80-88--and merge them.
First, the "southern" grid:
From the **Menu Toolbar**, select **Processing > Toolbox > Vector creation > Create grid***. The values you input should look like this:
![](create_grid_popup.png)
When you've entered the correct information, select **Run**, then **Close**. You should now see a grid covering all but Canada's High Arctic.
![](grid_overlay_opaque.png)
To make it easier to verify, we'll increase the transparency of our grid layer. Right click the newly-created grid layer within the **Layers** box and select **Properties... > Symbology**. Then, adjust the opacity to, say, 25%. Click **Apply**, then **OK**. (You can also change the color combination of both layers for better visibility.)
![](grid_transparent_colorChange.png)
We can now clearly see three things:
1. Our grid matches the extent (N, S, E, W) that we specified.
2. The grid subdivides the rectangular polygons of the 1:1m index into quadrants.
3. There are features within our new grid that are not conincident with the original (i.e., there is no counterpart within the original grid).
Since we only want to keep features that are present in both grids, we will have to delete these non-coincident polygons. To do this, click **Select Features** from the **Attributes Toolbar**.
[Make layer permanent]
-->
