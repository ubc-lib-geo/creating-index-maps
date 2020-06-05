---
layout: default
title: Clean a UBC inventory
nav_order: 3
parent: Workflows
---
# Cleaning a UBC Inventory

If a digital index map exists for a map series, and UBC Library has an inventory of their holdings on a spreadsheet, then we can connect the two using GIS. However we'll first need to make sure that the inventory spreadsheet is properly formatted.

## Identify OpenIndexMap fields in the UBC inventory

The basic steps to complete this part:
1. Review each column and highlight ones that apply to an OIM elements.
2. Remove columns that are not highlighted.
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

Keep in mind that as the inventory columns are compared to OIM elements, there may be inconsistencies that would prevent a straightforward crosswalk. Using the example above, an OIM <b>location</b> element could be applied to both the "prov" and "Other place" columns. For now, this isn't anything to be concerned about – simply identify columns that can be coverted into an OIM element. In later steps in the process, we will clean up the field names and data, including concatenating two columns if needed.




## 3 - Remove unused fields from UBC inventory

After all fields have been assessed, remove any unused fields.

## 4 - Export/Save the spreadsheet as a plain text

Export the spreadsheet as a plain text document, .csv is preferred.
