---
title: "Coding"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is QGIS Python Console?
- How to automate geospatial tasks with QGIS?
  
::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Demonstrate how to use QGIS Python Console.
- Demonstrate how to automate QGIS tasks with Python coding.

::::::::::::::::::::::::::::::::::::::::::::::::

## QGIS Python Console

- The QGIS Python Console is an interactive shell for Python command executions.
- It also has a Python file editor that allows you to edit and save your Python scripts.
- Modules from QGIS (analysis, core, gui, server, processing, 3d) and Qt (QtCore, QtGui, QtNetwork, QtWidgets, QtXml) as well as Python’s math, os, re and sys modules are already imported and can be used directly.

  The screenshots below show how to open QGIS Python Console, and how it looks like.

<img width="595" alt="Screenshot 2025-03-04 at 10 58 51 AM" src="https://github.com/user-attachments/assets/3157328b-18c8-43bf-b0a7-a434496de234" />


<img width="1048" alt="Screenshot 2025-03-04 at 11 00 04 AM" src="https://github.com/user-attachments/assets/79248436-7123-46cc-814c-d09074375c7f" />

Replace trainXX with your training account

```sh
mkdir -p /scratch/negishi/trainXX/project/code_output
```

```python
# change work directory
path ="/scratch/negishi/trainXX/project/code_output"
os.chdir(path)
```

## Load Data

There are two ways to load the data. 

#### The first way

There are two steps to load data. 
* First, data is loaded in memory.
* Second, the data is added to QGIS map canvas. This is not necessary.

##### (1) Load Vector Data

```python
vectorfile ="/scratch/negishi/liu4201/project/output/stream10_6.geojson"

# The format is:
# vlayer = QgsVectorLayer(data_source, layer_name, provider_name)

vlayer = QgsVectorLayer(vectorfile, "stream10_6", "ogr")
```

:::::::::::::::::::::::: spoiler 

When you create a QgsVectorLayer or QgsRasterLayer object, it's just a layer in memory. It doesn't automatically get added to the QGIS map canvas.
You have more control over the layer's properties and how it's loaded. You can even choose to not load it. You can also set things like the layer's CRS, geometry type, and other options before adding it to the map.

:::::::::::::::::::::::::::::::::

```python 
if not vlayer.isValid():
    print("Layer failed to load!")
else:
    QgsProject.instance().addMapLayer(vlayer) # load the layer
```
:::::::::::::::::::::::: spoiler 

Now it get added to the QGIS map canvas.

:::::::::::::::::::::::::::::::::

##### (2) Load Raster Data

```python
# use the firt way to load rasterfile 1
# load raster to memory
path_to_tif = rasterpath + "USGS_1M_16_x50y448_IN_Indiana_Statewide_LiDAR_2017_B17.tif"
rlayer = QgsRasterLayer(path_to_tif, "dem")
```

```python
# added raster to the QGIS map canvas
if not rlayer.isValid():
    print("Layer failed to load!")
else:
    QgsProject.instance().addMapLayer(rlayer) # load the layer
```

#### The second way

##### (1) Load Vector Data
It loads a vector or raster layer and immediately adds it to the map canvas

```python
vlayer = iface.addVectorLayer(vectorfile, "stream10_6", "ogr")
if not vlayer:
  print("Layer failed to load!")
```

##### (2) Load Raster Data

```python
#use the second way to load rasterfile 2
path_to_tif2 = rasterpath + "USGS_1M_16_x50y449_IN_Indiana_Statewide_LiDAR_2017_B17.tif"   
iface.addRasterLayer(path_to_tif2, "dem2")
```

## Merge DEM Data

```python
rlayer = QgsRasterLayer(path_to_tif, "dem")
rlayer2 = QgsRasterLayer(path_to_tif2, "dem2")

# Merge rasters
processing.run("gdal:merge", {"INPUT": [rlayer, rlayer2], "OUTPUT": "merged_dem.tif"})

#check the merged_dem
iface.addRasterLayer("merged_dem.tif","merged_dem")
```

## Calculate Slope

```python
# Calcualting slope
processing.run("qgis:slope", {"INPUT": "merged_dem.tif", "OUTPUT": "slope.tif"})

#check it 
iface.addRasterLayer("slope.tif","slope")
```


## Calculate Hillshade


## Analyze Hydrology

## Calculate Topograhic Index

