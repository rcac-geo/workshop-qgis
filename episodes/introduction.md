---
title: "Introduction"
teaching: 10
exercises: 3
---

:::::::::::::::::::::::::::::::::::::: questions 

- Why QGIS?
- How to start QGIS on HPC Clusters?
- How to load and visualize data in QGIS?
- How to process and export data in QGIS?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain why we should use QGIS
- Demonstrate how to start QGIS on HPC Clusters
- Demonstrate how to load and visualize data in QGIS
- Demonstrate how to process and export data in QGIS

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction to QGIS

GIS stands for ‘Geographical Information System’. We can use a GIS application, such as ArcGIS and QGIS to manipulate spatial information. 

QGIS is a free and open-source software that runs on various operating systems. It offers a wide range of functionality, such as vector and raster analysis, geoprocessing, geocoding, georeferencing, web mapping, and 3D visualization. QGIS also supports many data formats and standards, such as Shapefile, GeoTIFF, GeoJSON, WMS, WFS, and PostGIS.

Why QGIS? It's free and flexible.

 1. Cost-free: Enjoy QGIS without any financial burden. It's completely free, no hidden fees.
 2. Free as in "Do It Your Way": You could extend QGIS to meet your specific needs, sponsor development or contribute your own code.
 3. Works where you work: Run QGIS on macOS, Windows, and Linux (so available for HPC Clusters). 
 4. Always getting better: Benefit from rapid development because anyone can add new features and improve on existing ones.
 6. Never get stuck: Access extensive documentation and a large and active supportive community is there for help. 
 7. Easily integrate Artificial Intelligence (AI) and GeoAI.

## Open QGIS on Clusters

We can start QGIS via ThinLinc Client or Gateway. 

#### 1. Start QGIS via ThinLinc

Follow up with [the Setup page](https://rcac-geo.github.io/workshop-qgis/index.html#software-setup), and connect with ThinLinc. There are two ways to start QGIS via ThinLinc. The two ways are fundamentally the same but one is interactive, and the other is typing code.

##### (1) Interactive Way

To open QGIS as an interactive job, we could go to "Cluster Software" and select "QGIS", as the figure below:

<img width="391" alt="Picture1" src="https://github.com/user-attachments/assets/1df48747-d717-442e-9af5-c25d4dc9f78d" />

Then select the "workshop" queue as below:

<img width="406" alt="Screenshot 2025-02-24 at 4 15 16 PM" src="https://github.com/user-attachments/assets/72d72419-4484-4e6e-9fed-3ec2fdf4920d" />

Then hit "No":

<img width="529" alt="Screenshot 2025-02-24 at 4 15 41 PM" src="https://github.com/user-attachments/assets/e3ea5e98-e83e-4d77-ba9c-bba7c62fbea3" />

Now input two cores and five minutes and hit Okay. You don't need to specifically request memory because memory will be relocated proportional with cores. But if you do, include unit such as "4G".

<img width="608" alt="Screenshot 2025-02-24 at 4 16 10 PM" src="https://github.com/user-attachments/assets/55a2b0be-3bc1-447c-a44d-04c4ec6a7e60" />

##### (2) Typing Code Way

We could start the Terminal as below:

<img width="186" alt="Screenshot 2025-02-25 at 9 51 03 AM" src="https://github.com/user-attachments/assets/c06429f8-15b6-4242-b416-080085cf8f23" />

To look up QGIS module, we could do:

```sh
module spider qgis
```

To start an interactive job and open QGIS:

```sh
sinteractive -A workshop -N1 -c8 -t8:00:00
module load qgis
qgis
```



#### 2. Start QGIS via Gateway

Gateway, also named Open OnDemand, is a Web interface includes file explorer, interactive apps including QGIS.​ We have to use our own accounts to login Gateway, not the training accounts we used for this workshop. 
Go to [Negishi Gateway](https://gateway.negishi.rcac.purdue.edu), login with our purdue accounts (when we have account on Clusters) and connect QGIS as the figure below.

<img width="911" alt="Screenshot 2025-02-25 at 10 05 05 AM" src="https://github.com/user-attachments/assets/f575bf3a-e6bd-468b-92ad-4a3b93405788" />


::::::::::::::::::::::::::::::::::::: callout

We could also open QGIS with Gateway, in the [Typing Code Way](https://rcac-geo.github.io/workshop-qgis/introduction.html#typing-code-way). We could start a terminal as below.

![Start Terminal in Gateway](https://github.com/user-attachments/assets/aac3d529-c726-4793-b3db-e90e55a260fc)


::::::::::::::::::::::::::::::::::::::::::::::::


## View Spatial Data

In Geographic Information Systems (GIS), data is primarily represented in two fundamental formats: vector and raster.

#### Vector Data

* Representation:
   - Vector data uses geometric objects—points, lines, and polygons—to represent spatial features.
   - Points represent individual locations (e.g., a city, a tree).
   - Lines represent linear features (e.g., roads, rivers).
   - Polygons represent areas (e.g., lakes, buildings, administrative boundaries).   
* Characteristics:
  - Precision: Vector data is excellent for representing discrete features with clear boundaries, offering high precision.
  - Scalability: Vector data can be scaled up or down without losing quality.
  - Data Storage: Typically, vector data requires less storage space than raster data for representing discrete features.
  - Use Cases: Best suited for representing features with distinct boundaries, such as roads, property lines, and political boundaries.
* Vector File Types:
  - Shapefile (.shp): A very common geospatial vector data format for GIS software. It actually consists of several files (.shp, .shx, .dbf, etc.)
  - GeoJSON (.geojson): A popular open standard format that uses JavaScript Object Notation (JSON) to represent geographic features.
  - KML/KMZ: Used by Google Earth for displaying geographic data.
  - File format is handled by GDAL/OGR package with a [full list](https://gdal.org/en/stable/drivers/vector/)



#### Raster Data

* Representation:
  - Raster data represents spatial information as a grid of cells (pixels). Each cell contains a value representing a specific attribute (e.g., elevation, temperature, land cover).   
* Characteristics:
  - Continuous Data: Raster data is ideal for representing continuous attributes, such as elevation, temperature, and satellite imagery.
  - Data Storage: Raster data can require significant storage space, especially at high resolutions.
  - Analysis: Raster data is well-suited for spatial analysis involving calculations and modeling.
  - Use Cases: Best suited for representing continuous surfaces, such as elevation models, satellite imagery, and aerial photographs.
* Raster File Types:
  - TIFF: Basic image format, no geographic information.
  - GeoTIFF: A TIFF file with added geospatial metadata, enabling it to be used in GIS applications.
  - COG (Cloud Optimized GeoTIFF): A type of GeoTIFF with a specific data structure optimized for fast access in cloud environments, often using tiled data storage.
  - File format is handled by GDAL/OGR package with a [full list](https://gdal.org/en/stable/drivers/raster/)
 
#### Key Differences 

* Structure: Vector data uses geometric shapes, while raster data uses a grid of cells.
* Data Type: Vector is for discrete features, raster is for continuous phenomena.
* Precision: Vector is generally more precise, while raster's precision depends on cell size.
* Storage: Vector often uses less storage for discrete features. Raster data storage size is heavily dependant on resolution.

#### Load Spatial Data
##### (1) Load vector data from files
* Step1: Layer -> Add Layer -> Add Vector Layer
  
<img width="554" alt="Picture2" src="https://github.com/user-attachments/assets/58bc28a8-7fe8-4dfd-8a54-495dbbfe1e6d" />

* Step2: Input your path of "alaska.shp" and hit "add"
  
![](https://github.com/user-attachments/assets/b68a9319-68f0-4502-9bb5-d3d6b87b33d0)

* Step 3: You will see the shapefile has been added to Layers as below.

![](https://github.com/user-attachments/assets/c5ba1734-88ee-4cc8-a79c-dd2f2b0cb1fb)


::::::::::::::::::::::::::::::::::::: challenge 
## Challenge 1: Try yourself
try yourself to add airports.shp to layers.

:::::::::::::::::::::::: solution 

<img width="613" alt="Picture3" src="https://github.com/user-attachments/assets/f4d958c0-3acb-42a9-855e-4505cbca2c04" />

:::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

When adding a data source, QGIS attempts to identify its Coordinate Reference System (CRS) from sources like a shapefile's .prj file. If no CRS information is found, QGIS prompts you to specify it. You can modify this behavior in Settings -> Options -> CRS to automatically assign either the project's CRS or a designated default CRS. (Graser et al., 2017)

::::::::::::::::::::::::::::::::::::::::::::::::

##### (2) Load CSV files
* Step 1: Layer -> Add Layer -> Add Delimited Text Layer 
* Step 2: Make changes as the red box in the picture below.

<img width="893" alt="Screenshot 2025-02-25 at 2 41 23 PM" src="https://github.com/user-attachments/assets/4ccee5c6-a3d0-4292-8751-04b044d875b0" />


* Step 3: You will see the shapefile has been added to Layers as below.
  
<img width="612" alt="Picture4" src="https://github.com/user-attachments/assets/db0dd043-5c42-48c2-b929-c48f24f010b6" />

##### (3) Load Raster files
* Step1: Layer -> Add Layer -> Add Raster Layer
* Step2: Input your path of "landcover.img" and hit "add"

![](https://github.com/user-attachments/assets/6566ea7f-8ca9-4def-96b3-ae16671039bf)

* Step 3: You will see the raster has been added to Layers as below.

<img width="428" alt="Picture5" src="https://github.com/user-attachments/assets/a849f162-7ad8-473b-a1e3-d6ad34a82e31" />

::::::::::::::::::::::::::::::::::::: challenge 
## Challenge 1: Try yourself
try yourself to add SR_50M_alaska_nad.tif (Hillshade GeoTiff) to layers.

:::::::::::::::::::::::: solution 

![](https://github.com/user-attachments/assets/e10386e9-d1c0-4736-8b9e-6618cf1a5db4)

:::::::::::::::::::::::::::::::::
## Challenge 2: A Question?

Did you find anything weird about the Hillshade image showing above?

:::::::::::::::::::::::: solution 

Yep, the hillshade should be in the North instead of the South. Let's check data Properties and change looking.

![](https://github.com/user-attachments/assets/ff8ff053-8a82-4335-a06d-e4086adb8986)

![](https://github.com/user-attachments/assets/67208203-a4ac-40c6-838f-8fe9d0a3ae10)

:::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

## Process Spatial Data
#### Filter Vector Data

Scenario: My Grandma wants to have a trip in Alaska but doctor said she shouldn't go to places with high elevation due to the heart problem. So I will find airports with low elevantion for her. For example, I found the airport with elevation lower than 1000 ft.

Solution: 

* Step1: Right click the data "airports" and select "Filter"

![](https://github.com/user-attachments/assets/b330ca5e-42e5-4d01-b587-4e74762b0375)


* Step2: Select "ELEV" from "Fields", and input the Specific Filter Expression as below:

![](https://github.com/user-attachments/assets/98e26b3a-6329-41eb-b769-3cb38434cce5)

* Step3: Hit "OK" and now only airport with elevation lower than 1000 ft show up.
* Step4-Export data: right click the data and selelct "Export" -> "Save Features As". Input information as figure below and hit "OK".

![](https://github.com/user-attachments/assets/5be55894-3ede-42bd-a888-36efda92b202)
  
#### Raster Calculation

Scenario: I'd like find some sunny slope where my Grandma and I can go skiing. So I found the places where Hillshade is smaller than 100, for example.

Solution:

* Step1: Turn on the Processing Toolbox if it's off, and Search "Raster Calculator".

![](https://github.com/user-attachments/assets/fb3965b0-0754-4f43-b7af-d9f30a4c1ac4)
![](https://github.com/user-attachments/assets/26b8ed3a-0484-4c83-be15-a50e89d9c5b9)


* Step2: Input the "Input Layers", "Expression", "Output CRS", and "Calculated" as the Output file.

![](https://github.com/user-attachments/assets/50d49743-2cb9-466a-806e-a077f31629d0)


* Step3: Hit "Run" and change the looking of output.

![](https://github.com/user-attachments/assets/a6e51da6-479c-4008-ad97-05333452897d)

* You have already written out the output file. But if you didn't, you could always export the data via right clicking it and select "Export" -> "Save As". Then input information as figure below and hit "OK".

![](https://github.com/user-attachments/assets/8074e204-dc55-4533-af9b-0dc1e85fc0d0)

  
::::::::::::::::::::::::::::::::::::: keypoints 

- QGIS is a free and open-source software that runs on various platforms, such as Windows, Mac, and Linux.
- QGIS has a large and active community of users and developers who contribute to its features, plugins, documentation, and support. 
- We can use QGIS via ThinLinc Client or Gateway on HPC Clusters. 
- We learned how to load and visualize vector and raster data.
- We learned how to process data and export them.

::::::::::::::::::::::::::::::::::::::::::::::::
