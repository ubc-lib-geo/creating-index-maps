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
Since we only want to keep features that are present in both grids, we will have to delete these non-coincident polygons. To do this, click **Select Features** from the **Selection Toolbar**. Select all of the features on our new grid layer which do not overlap with the original grid. (Click and hold to drag a box around multiple features. Press and hold 'Shift' to select multiple segments.) Once you've selected the non-overlapping features, right click on the new grid layer in the **Layers** box and select **Open Attribute Table**. You should see some features highlighted in blue. Within the attribute table, in the top-left corner, click **Toggle editing mode**, then **Delete selected features** to the right. Click **Save edits**, and minimize the attribute-table popup window.
Your screen should now look similar to this:
![](grid_trimmed.png)
Now that the outline of our grid matches the original, we want to transfer the NTS labels from the features of the original grid to the corresponding features of our new grid. Do to this, we will make use of QGIS' **Join attributes by location** algorithm.
From the **Menu Toolbar**, select **Processing > Toolbox > Vector general > Join attributes by location**.
Within the popup window, select the following three values:
![](join_attributes.png)
Click **Run**, then **Close**.
Open the attribute table for the newly-created layer to verify it contains the attributes from both layers.
To help keep track of things, rename the new layer by right clicking on the layer and selecting **Rename Layer**. In this example, we'll rename the layer to **south_labels**.
We now have the first portion of our label affixed to our grid's features. However, given that we subdivided the original grid's features into quadrants, we now have four features in our new grid that share the same label from the original. Our next task, then, will be to add characters to our labels, so we can uniquely identify each feature within the new grid. In this example, we will distinguish the features by appending either 'SE', 'SW', 'NE', or 'NW' to its label, depending on its relative position.
First, we will select all the 'southern' features for each label. To do this, from the **Attributes Toolbar**, click **Select Features**. (Make sure you have the correct layer selected--"south_labels", in our case.) Click on a feature in the bottom row of features with shared labels and drag the cursor to selct the entire row. Press and hold "Shift" to continue this action and select all of the "southern" rows in the "south_labels" layer. Your screen should now look similar to this:
![](grid_south_rows.png)
Open the Attribute Table for the "south_labels" layer. You should now have half of the layer's features selected--highlighted in blue--which you can verify by looking at the information included on the top ribbon. Close the Attribute Table.
Select **Processing > Toolbox > Vector table > Refactor fields**. Input the displayed values in the following fields:
![](refactor_fields_south.png)
Before clicking **Run** on the **Refactor Fields** popup box, click the **Expressions** button for the "IDENTIF" field:
![](expressions_button.png)
Within the **Expression Dialog** popup box, in the middle column, click **String > rpad**. Follow the documentation in the right column to create an expression in the left column that looks like this:
![](expression_add_S.png)
Click **OK**, then **Run**, and **Close**. Rename the new refactored layer to something more descriptive. In our case, we'll rename in "south_labels_s".
Repeat this process for the "northern" rows.
Next, we will merge the "south_labels_s" and "south_labels_n" layers into a single layer. From the **Processing Toolbox** sidebar, click **Vector general > Merge vector layers**. From the **Merge vector layers** popup window, in the **Input layers** field, select the two layers you'd like to merge, and click **OK**:
![](merge_vectors_selection.png)
Click **Run**, then **close**. (The rest of the default settings are fine.)
Open the Attribute Table and sort by the labels ("IDENTIF") column to verify the merge performed as expected. You should now see two features sharing the same n/s label, as opposed to four after subdividing the original grid.
Rename the merged vector. (We will name it "south_labels_ns".)
Repeat the previous steps, including merging layers, on the "south_labels_ns" layer for the "east" and "west" rows to derive the final layer for the "southern" portion of our Canada grid.
Now that we have unique labels for each feature of the "southern" portion of our Canada grid, we will wrap up our project by creating another subdivided grid for the "High Arctic" portion of the original grid. To do this, simply repeat our earlier steps:
1. Create a grid
2. Trim excess features
3. Transfer labels using **Join attributes by location**
4. Create layers with "north" and "south" labels, using **Refactor fields**
5. Merge "north" and "south" layers into a single layer
6. Create layers with "east" and "west" labels, using the new merged "north-south" layer from the previous step
7. Merge the "east" and "west" layers into a single "High Arctic" layer
It's important to keep in mind, however, that the horizontal spacing will be different--8 degrees, instead of 4. (This is the reason we couldn't create a single grid to begin with.)
![](create_grid_arctic.png)
Once the "High Arctic" layer is complete, merge it with the "southern" layer to create the finished grid.
[Make layer permanent]
-->
