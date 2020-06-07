---
layout: default
title: Create a virtual layer in QGIS
nav_order: 1
parent: Workflows
---
# Create a virtual layer in QGIS
Once both an OIM compatible spreadsheet and a digital map index exist, we will join the two using QGIS. The main idea is that we will link the two files with a primary key value contained in both. In most cases this will be the OIM element "label" which holds a value for an alphanumeric sheet ID, but it may also be another sheet-specific element such as "title".

Because spreadsheets likely contain many rows for one single index grid section (sometimes individual map sheets had many editions!), we will need to treat this 'join' as a 1-to-many relationship. In other words, each grid section on the digital map index will need to be connected with many spreadsheet rows. Ideally, the complete OIM digital map index will have "stacked" grid sections - one for each existing map edition - so that eventually we can programmatically query values from each stacked feature.

Below is a map of Canada represented by semi-transparent grid sections, with darker colours illustrating where more grid sections are stacked. In those darker areas, more editions of the Canadian 1:250k NTS maps were printed and are available in Koerner Library.
![250k stacked](stacked250k.png "250k stacked")

To do this, we will [use QGIS to create a virtual layer](https://docs.qgis.org/3.10/en/docs/user_manual/managing_data_source/create_layers.html#creating-virtual-layers).

The basic steps to complete this part:
1. Add your digital map index and inventory .csv to a QGIS project.
2. Add a new virtual layer from the two using the primary key value.
3. Export as a .geojson

This part requires use and some knowledge of [QGIS v3.10](https://qgis.org/en/site/).
{: .note}

### Open QGIS and start a new projection

Start QGIS, then open a new project. Either select a new project template on opening QGIS, or Project > New.
![start a new project](img/start-new-proj.png "start a new project")

### Open a digital map index file
Click the Open Data Source Manager button (Win: Crtl + L) (Mac: Command + L). In the new Data Source Manager window, select Vector from the left, and make sure Source Type is File. For the Source vector file, navigate to and select the digital map index file from your system. Click Add and then Close. You may have to quickly transform your layer to a new projection.
![open data window](img/data-win.png "open data window")

### Add the spreadsheet inventory
In a new Data Source Manager Window, select Delimited Text from the left, and browse to the file using the File name field. For File Format, be sure that CSV is selected. For Geometry Definition, select No Geometry. Other settings can be left as default, then click Add and then Close.
![add the csv](img/add-csv.png "add the csv")

### Rename the layers
Because in a few steps we'll be using SQL to query our files, we first have to be sure that the names of our two layers do not contain any spaces, /, or -. To do this rename the layer without those characters. Right-click your layers' name and select Rename. Now rename your layers using _ , or use [camelCase](https://simple.wikipedia.org/wiki/CamelCase).

If you do not see the names of your layers anywhere, you may need to add your Layers Panel by selecting View > Panels > Layers.
{: .warn}

You should now see something like this:
![layers added](img/layers-added.png "layers-added")

### Determine each layer's primary key
We will need to link the two layers together using a common value (aka primary key, or PK). In most cases this will be the sheet's alphanumeric identifying number (example: 092G), but it may also occasionally be a sheet title. Each layer *should* contain these values.

For each layer, right-click their name in the Layers Panel, and select Open Attribute Table. You should now see a table showing all of the attribute values for each feature (a row in the table). Attribute names are contained in the column headers.

For each layer, find the column header that represents the layer's primary key, and make a note (a mental one, or write it down).

### Add a new virtual layer
Now we will relate the two files together using a virtual layer. Select Layer > Create Layer > New Virtual Layer...  

In the new Virtual Layer window, we will add an SQL query in the Query field. The query will need to use the following format:
```SQL
SELECT * FROM [layer1], [layer2] where [layer1 PK] = [layer2 PK]
```
<br>
For example, these layers would use the following query:

| Layer name           | Column containing primary key values |
|----------------------|--------------------------------------|
| canada250k_nts       | IDENTIF                              |
| canada250k_inventory | label                                |

```SQL
SELECT * FROM canada250k_nts, canada250k_inventory where IDENTIF = label
```
<br>
Once you have assembled your query, select Test to identify any potential errors. If no errors, select Add and then Close. This process could take a moment or two.

![new virtual layer](img/new-virt-layer.png "new virtual layer")

After your query runs, you will see a new layer in your Layers Panel named virtual_layer or something similar. Right-click that new virtual layer, and select Open Attribute Table to confirm that the inventory attributes appear.

### Remove extra attributes
You may need to remove some unnecessary fields from your new virtual layer, especially anything that is not an OIM element.
