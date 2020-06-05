---
layout: default
title: Clean a UBC inventory
nav_order: 3
parent: Workflows
---
# Cleaning a UBC Inventory

If a digital index map exists for a map series, and UBC Library has an inventory of their holdings on a spreadsheet, then we can connect the two using GIS. However we'll first need to make sure that the inventory spreadsheet is properly formatted.

## Identify OpenIndexMap fields in a UBC inventory

The basic steps to complete this part:
1. Review each column and highlight ones that apply to an OIM elements.
2. Remove columns that are not highlighted.
3. Export as a .csv.

This part requires a spreadsheet application like Microsoft Excel or MacOS Numbers.
{: .note}

First we'll need to make sure that any information contained in the inventories can be cross-walked to the OpenIndexMap (OIM) format standard. Since each UBC inventory spreadsheet is unique, to do this we will need to manually inspect each one and look for applicable column headers which match OIM elements:

| Element      | Description                                      | Example |
|--------------|--------------------------------------------------|---------|
| <b>label</b> | Alphanumeric code identifying the sheet. <b>Mandatory if applicable</b>.| 092G    |
| <b>labelAlt</b> | Alphanumeric code for the sheet that was used in previous or subsequent editions, or for when there are multiple labels| 092G14 East    |
| <b>datePub</b> | Date the sheet was published or made available <b>Mandatory if applicable</b>.| 1981-09    |
| <b>dateSurvey</b> | Date the map sheet was surveyed | 1954    |
| <b>datePhoto</b> | Date the map sheet was photocorrected | 1990    |
| <b>dateReprint</b> | Date the map sheet was reprinted | 1978    |
| <b>date</b> | Use when no other date field is relevant | 1922-08-23    |
| <b>location</b> | Geographic place name identifying the area covered by the map sheet. <b>Separate with pipe character</b>. | British Columbia   |
| <b>scale</b> | Scale statement (representative fraction and qualifiers) of the individual sheet | approximately 1:12000    |
| <b>title</b> | Title of the map sheet <b>Mandatory if available</b>.| Riviere Embarrassee    |
| <b>titleAlt</b> | Alternate title, previous title, or subsequent title | Beaver Pond    |
| <b>edition</b> | Statement indicating the edition <b>Mandatory if available</b>.| 3rd edition    |
| <b>publisher</b> | Publisher of the sheet | Conselho Nacional de Geografia    |
| <b>projection</b> | Information about the map sheet's projection, coordinate system, or datum | UTM 14    |
| <b>lcCallNo</b> | The Library of Congress call number | G3700 s24 .U5    |
| <b>contLines</b> | Indication of whether or not there are contour lines on the map (<b>boolean</b>) | true    |
| <b>contInt</b> | Contour interval, including units | 20 m    |
| <b>bathLines</b> | Indication of whether or not there are bathymetric lines on the map (<b>boolean</b>) | false    |
| <b>bathInt</b> | Bathymetric contour interval, including units| 400 ft    |
| <b>inst</b> | Local institution holding the material | University of British Columbia Library    |
| <b>sheetId</b> | Local institution's unique identifier for the sheet | 630cba sheet 14    |
| <b>available</b> | Indication if the institution holds the sheet (<b>boolean</b>). <b>Mandatory</b>. | true    |
| <b>physHold</b> | Link to information about the physical object <b>Mandatory if applicable</b>.| http://resolve.library.ubc.ca/cgi-bin/catsearch?bid=3711482    |
| <b>digHold</b> | Link to information about the digital object | https://open.library.ubc.ca/collections/ifcsm/items/1.0387689    |
| <b>instCallNo</b> | Call number used locally | G3700 sVAR .U5    |
| <b>recId</b> | Local unique identifier for the digital object | 1.0387689    |
| <b>download</b> | Link to direct download of the item | https://open.library.ubc.ca/media/download/pdf/ifcsm/1.0387689/0    |
| <b>websiteUrl</b> | Link to a website with metadata or other information | https://open.library.ubc.ca/collections/ifcsm    |
| <b>iiifUrl</b> | iiif Manifest URL | https://iiif.library.ubc.ca/presentation/cdm.ifcsm.1-0387689/manifest    |
| <b>notes</b> | Free text for comments and other information | In poor physical condition    |

As columns in the UBC inventories are identified, highlight them or make a note. We will delete the unused columns at the end. For example, the UBC inventory for this Canadian topographic map series has several columns that match OIM elements. The screenshot below shows a selection of inventory column headers, with associated OIM elements in red.

![250k example inventory with OIM elements](example250k.png "250k example inventory with OIM elements")

Keep in mind that as the inventory columns are compared to OIM elements, there may be inconsistencies that would prevent a straightforward crosswalk. Using the example above, an OIM <b>location</b> element could be applied to both the "Prov" and "Other place" columns. For now, this isn't anything to be concerned about – the task at hand is to simply identify columns that can be converted into an OIM element. In later steps in the process, we will clean up the field names and data, including concatenating two columns if needed.

Once all unused columns are deleted, the next step is to transform our columns/values to match the OIM standard.

## Transform columns using OpenRefine

The basic steps to complete this part:
1. Start a new project in OpenRefine with your UBC inventory with OIM columns.
2. Use common OpenRefine functions to transform and clean your columns.
3. Export as a .csv.

This part requires [OpenRefine](https://openrefine.org/) to transform and clean your inventory.
{: .note}

Working toward having an OIM standardized inventory, the next step will transform the UBC inventory columns and values using functions in OpenRefine. Here are some common OpenRefine functions that will be useful for cleaning up inventories:

### Mass edit a column
<b>Use this if you need to change a common value of a cell from one thing to another, for instance if you would like to change "Koerner Library" to "true"</b>.
- Click on a column and select Facet > Text facet. On the left you should see:
![UBC has, before](ubc-has-before.png "UBC has, before")

The window above is showing all values listed in the column, with the number of occurrences of that value in gray. In this case there are 32 occurrences of values that are nothing but whitespace. Delete any whitespace by hovering over the value and selecting <b>edit</b>. Now delete the whitespace and click <b>Apply</b>. This shoudl remove the 32 occurrences of whitespace.

- For the term that you would like to mass edit, hover the value and select <b>edit</b>, then type the term that should replace it and click <b>Apply</b>. In this example I would like any occurrence of the value "k2 sup." to be "true", since this column will eventually become my OIM "location" element. I will also change "(blank)" to the value "false", since this means that the item is not physically available.
![UBC has, after](ubc-has-after.png "UBC has, after")

Mass editing a column may also reveal inevitable occurrences of human error when manually creating spreadsheets. For instance a column with values meant to represent scale:
![Human error](human-error.png "Human error")
It's recommended to fix columns to correct any major instances of human error *with reasonable effort*. This column can be cleaned to fix human error and align with OIM standards:
![No human error](no-human-error.png "No human error")

### Replace a term or value
<b>Use this is you would like to change all of the occurrences of a term into something else, like changing "BC" to "British Columbia" in an entire column with other values. This is different than mass editing cell values, because this will edit a specific term within a cell, and not the entire cell value.</b>
- Click on a column with values that need to be replaced, then select Edit cells > Transform.
- In the new window's "Expression" box, the expression should read <b>value.replace('[term]','[replacement]')</b>. For example, if you would like to replace "NL" with "Newfoundland and Labrador", this would be the expression:
```
value.replace('NL','Newfoundland and Labrador')
```
- Click <b>OK</b> to execute the changes.

### Add a term or value
<b>use this if you would like to insert a term in the cell value for the entire column, like adding the term "UTM" to a column with just a value for the zone number.</b>
- Click on a column with values that need to be replaced, then select Edit cells > Transform.
In the new window's "Expression" box, the expression should read <b>'[term]' + '[space]' + value</b>. For example:
```
'UTM' + ' ' + value
```
This expression will turn a column with only the values of UTM zones into one with <b>UTM 10</b>.
- Click <b>OK</b> to execute the changes.

### Concatenate / merge columns
<b>use this if you would like to join two columns together, like two different columns with geographic location values.</b>
- Click one column that you would like to join with another, and select Edit columns > Join columns.
- On the left, select the second column (and any additional columns) to join.
- For the content separator, refer to the OIM elements in case values need specific separators. For example, the <b>location</b> element requires a pipe character as a separator between values. So, for joining two columns with location values, this will need to be <code>' | '</code>.
- Select skip nulls.
- Select Delete joined columns.
![Join columns](join-columns.png "Join columns")
- Click <b>OK</b> to execute changes.

### Trim leading and trailing whitespace

This should be done to all columns, but at a minimum, for columns representing OIM elements 'label'
- Click on a column with values that need to be replaced, then select Edit cells > Common transforms > Trim leading and trailing whitespace.

## Rename columns representing OIM elements in OpenRefine

This part requires [OpenRefine](https://openrefine.org/) to rename columns.
{: .note}

Once columns are cleaned, they are ready to be renamed as OIM elements. If there are any columns that are not ready for an OIM name, continue transforming in OpenRefine.







then export the spreadsheet as a .csv. The naming convention should be something like: [identifier]-[scale]-inventory.csv. For example, the Canadian NTS 1:250,000 scale map series inventory would be <b>nts-250k-inventory.csv</b>.
