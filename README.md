# fbcolocation
Tutorials, projects, and more about Facebook colocation map

# A tutorial on visualizing FB Data for Good Colocation Map

## Get started

Colocation map data from Facebook Data for Good consist of two CSV file
1. The number of users popped up in the designated date for every level 3 geographical unit (e.g. colocation_alpha_[REGION NAME]_pop_[yyyymmdd].csv)
2. Link strength between level 3 geographical units

### Understanding the geographical unit indicator in colocation data (tabular version)
[Pitney Bowes](https://www.pitneybowes.com/us/data/boundary-data/global-boundaries.html)
[Chun Wan](https://www.map.gov.hk/gm/map/s/dce2019/district/A)
[Central & Western District](https://www.eac.hk/en/distco/2019dc_elect_map.htm)
[Hong Kong SAR](https://www.eac.hk/pdf/distco/2019dc/final/map_dc2019x_index.pdf)
[GADM](https://gadm.org/download_country_v3.html)
[ESRI Living Atlas](https://livingatlas.arcgis.com/en/browse/)
[Hong Kong Constituency](https://services.arcgis.com/P3ePLMYs2RVChkJx/arcgis/rest/services/HKG_Boundaries_2018/FeatureServer)
[Text to Columns](https://support.office.com/en-us/article/split-text-into-different-columns-with-the-convert-text-to-columns-wizard-30b14928-5550-41f5-97ca-7a3e9c363ed7)


Facebook now uses level 3 geographical boundaries from [Pitney Bowes], which means the 3rd level of administrative boundary of a country (a level 1 administrative unit),  For example, the level 3 geographical unit of Hong Kong SAR is constituency. [Chun Wan] (A01) is a constituency (level 3 unit) of [Central & Western District] (A) (level 2 unit, **district**). [Central & Western District] is a district of [Hong Kong SAR] (level 1 unit, region or country).

Please note that some geographical boundary data provider defines the country level as **level 0**, such as [GADM]. In this case, Hong Kong SAR is a **level 0** unit and [Central & Western District] is a **level 1** unit.

### Attach the tabular colocation data to an existing file of geographical boundary for mapping
The current version of colocation maps do not contain geographical coordinates of the centroid for the level 3 geographical unit. Users need to apply a table join to connect the tabular colocation data to an existing geographical dataset, usually by the **names** of the geographical unit. This requires **consistency** in the format of the geographical unit names between the two tables.

### Some geographical boundary dataset:
..* [GADM] provides free geographical boundary data for most countries and regions in the world in multiple formats (e.g. R, KMZ, ESRI Shapefile). It defines country level geographical unit as level 0 unit (level 1 for [Pitney Bowes] data). So please make sure you are referring to the right geographical level.

..* [ESRI Living Atlas] provides detailed level 1-3 geographical boundary for most countries and regions in the world, some even include a level 4 layer. This is an example of [Hong Kong Constituency] feature layer from Esri Living Atlas. This item requires an ArcGIS Online organizational subscription or an ArcGIS Developer account and does not consume credits. You should be able to find level 1 to 3, sometimes even level 4 boundaries from Esri Living Atlas for your **online** visualization and analysis use.

A quick checklist before joining FB colocation map to any geographical layers
..* Are the names of geographical unit provided in the **SAME FORMAT** in both tables?
...* If one table includes the type of geographical unit as a part of the name and the other is not, you won't be able to join the two tables. For example, your colocation map refer to [Chun Wan] as **Chun Wan** but your geographcial layer refer to [Chun Wan] as **Chun Wan Constituency**, they are NOT in the same format and should be fixed before applying table join.
..* Are the names of geographical unit using the **SAME DELIMINTER** to separate words if multiple words are involved in one name?
...* For example, Chun Won and ChunWon do not match and need to be fixed.
...* [Text to Columns] tool from Microsoft Excel will help trim the unwanted part. Or you can simply use any string trimming function in your preferred tools.
..* Compare the geographical unit names to make sure there is no misspelled names
...* The misspelled names will make you lose some geographical units after applying table join.

Perform table join using ArcGIS and QGIS


### Mapping after attaching FB colocation data to a geospatial dataset
After completing the previous steps, you now have a geospatial dataset
