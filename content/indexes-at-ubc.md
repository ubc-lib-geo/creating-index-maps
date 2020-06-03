---
layout: default
title: Spatial indexes at UBC Library
nav_order: 3
---

We have a couple of map indexes in GitHub, 1 for digital collection, one for physical. However, we have MANY paper map indexes for series in our collection.

We have inventories for superceded collections, which need to be cleaned up for OIM.

Project 1: clean inventories, and crosswalk to OIM endorsed headers. For inventories with existing spatial index, relate using common field in GIS. In QGIS we'll [create a one-to-many relationship](https://docs.qgis.org/3.10/en/docs/user_manual/working_with_vector/attribute_table.html#creating-one-or-many-to-many-relations), since there could be multiple editions of the same map, causing one grid section to be tied to many features (maps, or rows in a spreadsheet).

Project 2: create spatial indexes totally in GIS.
Someone skilled in GIS, and has access to maps can do this.
  1. create fishnet or grid
  2. populate attribute table, create duplicate rows for each map edition

Project 3: create inventories, relate in QGIS
Doesn't need GIS to progress, but need maps.
  1. create paper inventories with OIM column headers
  2. relate with common field in QGIS later (project 1)


Example indexes that can start being created:

Project 1:
NTS 1:50k
NTS 1:250k

Project 2:
Columbia River Maps
Railway Belt
A-series
127k and 253k series
