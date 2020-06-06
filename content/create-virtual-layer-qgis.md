---
layout: default
title: Create a virtual layer in QGIS
nav_order: 1
parent: Workflows
---
# Create a virtual layer in QGIS
Once both an OIM compatible spreadsheet and a digital map index exist, we will join the two using QGIS. The main idea is that we will link the two files with a primary key value contained in both. In most cases this will be the OIM element "label" which holds a value for an alphanumeric sheet ID, but it may also be another sheet-specific element such as "title".

Because spreadsheets likely contain many rows for one single index grid section (sometimes individual map sheets had many editions!), we will need to treat this 'join' as a 1-to-many relationship. In other words, each grid section on the digital map index will need to be connected with many spreadsheet rows. Ideally, the complete OIM digital map index will have "stacked" grid sections - one for each existing map edition - so that eventually we can programmatically query values from each stacked feature.

Below shows semi-transparent grid sections, with darker colours illustrating where more grid sections are stacked.
![250k stacked](stacked250k.png "250k stacked")

To do this, we will [use QGIS to create a virtual layer](https://docs.qgis.org/3.10/en/docs/user_manual/managing_data_source/create_layers.html#creating-virtual-layers).

The basic steps to complete this part:
1. Add your digital map index and inventory .csv to a QGIS project.
2. Add a new virtual layer from the two using the primary key value.
3. Export as a .geojson

This part requires use and some knowledge of [QGIS v3.10](https://qgis.org/en/site/).
{: .note}
