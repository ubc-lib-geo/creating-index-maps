---
layout: default
title: Modify an existing digital map index
nav_order: 2
parent: Workflows
---
# Converting MPKs to GeoJSON from Colorado School of Mines' "Clearinghouse of Indexes" for paper map sets

**Step 1:** Download index .mpk files from [the clearinghouse](https://www.arcgis.com/home/group.html?id=427f021a56f9449dbba24fbb4b915f55&view=list#content) for map series in UBC's collections. Save them in a temporary location on your computer, so they can be deleted later. 

.mpk files are Esri-formatted packages of data. They are essentially compressed (zipped) files containing all the data and file paths needed to open a map project directly in ArcMap or ArcGIS Pro. Instead of manually unzipping these files and looking for the data in folders, we will first open them in ArcMap, and then export the index features as .geojson files. Later, we'll format the .geojson via OpenIndexMaps best practices.

**Step 2:** Open a blank ArcMap project, and drag the .mpk file into the blank map document. If a map index opens, move to step 4.

**Step 3:** We'll now use ArcMap to extract the .mpk contents into a new folder and open them as an uncompressed .mxd project file. Click on the **ArcToolbox** and select **Data Management Tools > Package > Extract Package**. In the new window, you will be prompted to enter an input and output location.
- Input Package = the .mpk file you want to extract
- Output Folder = Home - Documents\ArcGIS
Save your file using the same name it was downloaded as, something like "China_50k_L783". Now, you can open the map document (Ctrl+O) to view the content. Choose the latest version folder of content.

**Step 4:** Now, we'll extract the features as a GeoJSON. Open the **ArcToolbox** and navigate to **Conversion Tools > JSON > Features to JSON**. 
- Input features = from the dropdown, choose the layer containing the index
- Output JSON = Any folder for safe keeping. (I choose my Desktop or a Flash Drive.) Save as the same file name as before ("China_50k_L783").
Select the option to save as GeoJSON, then press **OK**.    

# Editing Colorado School of Mines (CSM) GeoJSON files in QGIS

**Step 1:** Fire up QGIS and add one of the GeoJSONs converted from CSM.

**Step 2:** Open the **Refactor fields** tool: **Processing > Toolbox > Vector table > Refactor fields**.

### Rename existing fields
**Step 3:** Now, we'll want to rename any existing fields to OIM standards. OIM uses camelCase for field names. For example:
- `Sheet_no` should be renamed to `label`
- `Sheet_name` should be renamed to `title`
- `Publisher` should be renamed to `publisher`
- `Date` should be renamed to `datePub`
To change the names of the fields in the **Refactor fields** tool, simply double click the **Field name** and type the new OIM replacement name.

### Refactor field values with an expression
**Step 4:** Some fields might require the use of an expression to conform to OIM best practices. For example, the "scale" value may be different between OIM and CSM:

|     | scale           |
|-----|-----------------|
| OIM | 1:250,000       |
| CSM | Scale 1:250,000 |

To remove "Scale" using the **Refactor fields** tool, click on the `∑` symbol to build an expression. 
  - In the middle panel, double-click **String > replace**. This should add `replace(` to your expression on the left.
  - After the first parenthesis, add the *before* and *after* string, separated by a comma--in this case, `"Scale ", ""`. Your field expression should ultimately be: `replace("Scale ", "")`
  - Click **OK** to submit this expression. 👌 

### Add new/remove unused OIM fields
**Step 5:** Now, we'll add the remaining OIM fields that were not already recycled from CSM. Altogether, we must include these "mandatory, if applicable" fields:

`label`, `datePub`, `title`, `edition`, `available`, `physHold`

Other fields should be added where all (or almost all) items in the set have the same value, such as:

`scale`, `publisher`, `lcCallNo`, `contLines`, `contInt`, `inst`, `recId`

Add any other fields, as needed.

**Step 6:** Once all the fields are ready to be refactored, click **Run** in the **Refactor fields** tool.

### Add data from map sheets
This will require you to add data to the fields using the maps themselves.
