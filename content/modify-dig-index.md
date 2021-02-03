---
layout: default
title: Modify an existing digital map index
nav_order: 2
parent: Workflows
---

# Downloading from Colorado School of Mines' Clearinghouse of Indexes to Paper Map Sets
## For Using QGIS

**Step 1** Download index .mpk files from [the clearinghouse](https://www.arcgis.com/home/group.html?id=427f021a56f9449dbba24fbb4b915f55&view=list#content) for map series in UBC's collections. Save them in a temporary location on your computer so they can be deleted later. 

.mpk files are Esri-formatted packages of data. They are essentially compressed (zipped) files containing all the data and file paths needed to open a map project directly into ArcMap or ArcGIS Pro. Instead of manually unzipping these files and looking for the data in folders, we will first open them in ArcMap, then export the index features as .geojson files. Then later we'll format the .geojson via OpenIndexMaps best practices.

**Step 2** Open a blank ArcMap project, and drag the .mpk file into the blank map document. If a map index opens, move on to step 4.

**Step 3** We'll now use ArcMap to extract the .mpk contents into new folder and open them as an uncompressed .mxd project file. Click on the ArcToolbox and select **Data Management Tools -> Package -> Extract Package**. In the new window you will be prompted to enter an input and output location. 
- Input Package = the .mpk file you want to extract
- Output Folder = Home - Documents\ArcGIS
Save your file using the same name it was downloaded as, something like **China_50k_L783**. Now you can open the map document (ctrl + o) to view the content. Choose the latest version folder of content.

**Step 4** Now we'll extract the features as GeoJSON. Open the ArcToolbox and navigate to **Conversion Tools -> JSON -> Features to JSON**. 
- Input features = from the dropdown, choose the layer containing the index.
- Output JSON = Any folder for safe keeping. I choose my Desktop or a Flash Drive. Save as the same file name as before (**China_50k_L783**).
Select the option to save as GeoJSON, then press OK.



