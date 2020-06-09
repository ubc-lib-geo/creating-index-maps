---
layout: default
title: Creating index maps
nav_order: 1
has_children: yes
has_toc: false
---
# Creating map indexes

This content is meant to help staff at UBC Library understand index maps, and to direct work toward creating digital index maps for some of our map collections using the OpenIndexMap content format standard.

For more information about the what a map index is and their importance in map collections see ["What are index maps?"](content/what-are-index-maps.md)

## Modernizing UBC inventories
We are extending previous work done at UBC to create 'inventories' of large paper map collections. These inventories were assembled over years of work to create complete listings for our unique holdings of maps. In most cases, these inventories - formatted on .xlsx spreadsheets - consist of thousands of items with many attributes. We are first [cleaning these spreadsheets with OpenRefine](content/clean-inventory.md), removing any macros or special characters, and formatting them to meet OpenIndexMap content format standards. Then we will [create new geodata](content/create-virtual-layer-qgis.md) from these files that allow us to spatially query and visualize our holdings. These files can also be shared with other libraries participating in the OpenIndexMaps community such as Stanford, Cornell, UC Berkeley, UC Santa Barbara, and many others.

With standardized, digital map indexes, we can begin to build applications to help us make our paper collections more discoverable through discovery interfaces like GeoBlacklight (see: Geodisy).

Below is an example web map listing all available map sheets for a particular location in Southern BC.
<iframe src="content/available-092g.html" frameborder="0" height="600" width="100%"> </iframe>
