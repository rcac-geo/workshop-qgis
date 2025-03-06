---
title: "Project"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is DEM?
- What types of downstream information can be derived from a DEM?
- What is the topographic landscape around Purdue?
- What are the hydrological features around Purdue?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Define and explain the preliminary knowledge.
- Show how to install plugins with QGIS.
- Identify the types of downstream information that can be derived from a DEM.
- Demonstrate how to analyze topographic landscape and hydrological features with QGIS.
- Explain the process of converting raster data to vector data.

::::::::::::::::::::::::::::::::::::::::::::::::

## Preliminary Knowledge 

#### 1. DEM (Digital Elevation Model):

A DEM is essentially a 3D representation of a terrain's surface. It's a raster dataset, meaning it's made up of a grid of cells (pixels), where each cell contains an elevation value.

* Think of it as a digital map that shows the height of the land at every point.
* DEMs are the foundation for creating slope, hillshade maps and analyzing hydrology.
* The DEM we used today is LiDAR (Light Detection and Ranging) data with one meter resolution from [USGS](https://apps.nationalmap.gov/downloader/), which uses laser pulses from aircraft or drones to measure terrain elevation accurately. 

#### 2. Slope:

Slope refers to the steepness or gradient of the terrain. It's typically expressed in degrees (0 to 90) or as a percentage. A slope of 0 degrees indicates a flat surface, while a slope of 90 degrees represents a vertical surface.

Slope maps are derived from DEMs and are useful for analyzing things like:

* Erosion risk
* Water runoff
* Suitability for construction

#### 3. Hillshade:

Hillshade refers to simulating how sunlight would illuminate the terrain. It enhances the visualization of landforms by showing how light and shadow interact with the surface. The hillshade effect is created by setting an azimuth and vertical angle for a light source. The Azimuth is the direction the light is coming from, and the vertical angle is the angle of the light source above the horizon.

<img width="535" alt="Screenshot 2025-02-28 at 12 45 44 PM" src="https://github.com/user-attachments/assets/6ee78881-4395-4197-a73f-3c88d1245fbe" />

Hillshade maps are also derived from DEMs and are valuable for:

* Visualizing terrain features and creating visually appealing maps
* Identifying subtle topographic details
  
#### 4. Analyzing hydrology

The workflow: DEM Input → Fill Sinks → Flow Direction → Flow Accumulation → Stream Extraction -> Watersheds

* Before calculating flow, the DEM needs to be preprocessed to remove any small depressions (sinks) that may trap water. These are often errors in the data or natural terrain features that disrupt continuous flow.
* The flow direction represents the direction in which water will move from each cell based on elevation. The most common method assigns flow using the D8 algorithm, where water moves to the steepest downward slope among the eight neighboring cells.
* The flow accumulation raster represents the number of upstream cells contributing flow to each cell. This helps identify areas with higher accumulated flow, which can indicate potential stream paths.
  - Low accumulation values: Represent hilltops or ridges.
  - High accumulation values: Represent valleys or stream networks.
* Streams are extracted by applying a threshold to the flow accumulation raster. A threshold defines the minimum number of contributing cells required to form a stream.
  - Higher thresholds result in fewer, larger streams.
  - Lower thresholds detect smaller streams, but may introduce noise.
* Last step is to extract Watersheds, an area of land that drains all precipitation and surface runoff to a common outlet(such as a river, lake, or ocean).
  - It is defined by topographic divides (ridges or hills) that separate it from adjacent watersheds.
  - Watersheds can be small (for example, a stream watershed) or large (covering multiple rivers).
  - Same concept as Catchments and Basins, but they are in different scales:
    
    **Basin** → contains multiple → **Sub-Basins** → made up of → **Watersheds** → includes smaller → **Catchments**

::::::::::::::::::::::::::::::::::::: challenge 
Load Data:

Let's first load the two rasters in data directory.

:::::::::::::::::::::::: solution 

<img width="1003" alt="Screenshot 2025-03-04 at 2 21 14 PM" src="https://github.com/user-attachments/assets/c6e10ffc-1d6c-458d-aa8e-b415181acd22" />

:::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

## Install Plugins

#### Install QuickMapServices

QuickMapServices (QMS) is a valuable plugin for QGIS that simplifies the process of adding and using a vast array of online basemaps and web mapping services. 

* Go to Plugins | Manage and Install Plugins
* Search "QuickMapSevices" and click "Install Plugin"
* Now click "Search QMS" and search "Google Maps", as below.
  
<img width="1355" alt="Screenshot 2025-03-04 at 12 11 27 PM" src="https://github.com/user-attachments/assets/07c1ee52-da62-4c9f-8918-4f1b6f234117" />

<img width="257" alt="Screenshot 2025-03-04 at 12 11 54 PM" src="https://github.com/user-attachments/assets/d7f3ddf9-624e-46a8-9267-120d63e56d5c" />

<img width="278" alt="Picture6" src="https://github.com/user-attachments/assets/098c0340-c254-4bbd-ad98-21ca9cf31849" />

#### Install WhiteboxTools

WhiteboxTools is a powerful, open-source geospatial data analysis platform that offers a wide range of geospatial analysis tasks including DEM analysis, hydrological modeling and more.

* Step 1: Install WhiteboxTools for QGIS
  - go to Plugins | Manage and Install Plugins
  - search "WhiteboxTools for QGIS" and click "Install Plugin"
* Step 2: Install Whitebox Executables
  - option 1: go to [WhiteboxTools](https://www.whiteboxgeo.com/download-direct/) and download.
  - option 2: run the command below:
    
  ```sh
  wget https://www.whiteboxgeo.com/WBT_Linux/WhiteboxTools_linux_amd64.zip
  ```
* Step 3: Unzip it by running
  
  ```sh
  unzip WhiteboxTools_linux_amd64.zip
  ```
* Step 4: Configurate it
  - go to Settings | options | Processing | providers | WhiteboxTools
  - go to WhiteboxTools executable and double click the content and click "..." to set it as "whitebox_tools" in your unzipped directory(the executable).
    
    your executable should be as below (you can also copy and paste):
    ```sh
    /home/trainXX/WhiteboxTools_linux_amd64/WBT/whitebox_tools
    ```
<img width="1031" alt="Screenshot 2025-03-04 at 11 57 25 AM" src="https://github.com/user-attachments/assets/ca8d085c-05a4-4a2d-98b6-9cad9050bff5" />

* Step 5: Now you could see WhiteboxTools show up at the bottom of the Processing Toolbox as below.
  
  <img width="256" alt="Screenshot 2025-03-04 at 12 07 08 PM" src="https://github.com/user-attachments/assets/bd000367-0013-4d19-b994-a1dd6e744a52" />

  
## Merge DEM Data

* Search "merge" in Processing Toolbox as below
  
  <img width="151" alt="image" src="https://github.com/user-attachments/assets/eb21a3ec-5ba2-4c53-94c1-dc26097bf189" />
  
* Select the two rasters as input
  
<img width="612" alt="image" src="https://github.com/user-attachments/assets/0a29fa99-1799-4d19-91a6-2262bdcc324e" />

* Type the output name in your scratch directory and hit "Run".

![Output file will be added to layers if you check "Open outputfile after running algorithm"](https://github.com/user-attachments/assets/3cc82073-b091-41d1-a955-c0aa40df1747)

* Now you could merged DEM in your Layers as below

<img width="337" alt="image" src="https://github.com/user-attachments/assets/384ea49d-923c-4a0a-8f2b-b6e91bc217d4" />


## Calculate Slope

Search "Slope" in Processing Toolbox, select the elevation layer, type the output file, and hit "Run" as below.

  ![](https://github.com/user-attachments/assets/631190c2-30e9-4fff-944a-7618c4f670ad)

::::::::::::::::::::::::::::::::::::::: callout

Spend two minutes to explore the slope where your are familar and see if it makes sense.
For example, I used it to find a nice slope to snow sled.

<img width="613" alt="image" src="https://github.com/user-attachments/assets/8984ebc8-b8ea-45d2-8af8-90af9132a639" />

:::::::::::::::::::::::::::::::::::::::::::::::::::

## Calculate Hillshade

Search "Hillshade" in Processing Toolbox, and input the elevation layer, parameters, and output as the figure below.

![](https://github.com/user-attachments/assets/fcddfdc5-0859-405d-873d-913f2ee6c1db)

## Analyze Hydrology

#### (1) Fill Sinks

* Step 1: type a few words to search "FillDepressionsWangAndLiu" as below
  
  ![](https://github.com/user-attachments/assets/f6123400-3abe-4265-a011-9ef0cf7f0404)
  
* Step 2: select dem, type output file, and hit "Run"
  
  ![](https://github.com/user-attachments/assets/fff8333b-59e8-4d56-9b81-8413314747d9)
  
* Step 3: hit close after the progress reach 100%, as below

  ![](https://github.com/user-attachments/assets/7c4bdd9f-7902-460c-bbd9-2f6af9c0bd6e)

#### (2) Flow Direction

* Step 1: search "d8" to find "D8Pointer" in the Processing Toolbox.
* Step 2: select "fillsinks" outputed from above procedure as the input DEM file and type the output as below

![](https://github.com/user-attachments/assets/16a3ccc4-a910-4c55-a812-94ab3bbe66a0)

* Step 3: hit close after the progress reach 100%; you will see the flowdirection layer has been added to Layers.

#### (3) Flow Accumulation

* Step 1: type a few words to search "D8FlowAccumulation" in the Processing Toolbox.
* Step 2: select "flowdirec" outputed from above procedure as the input and type output

![check "Is input the D8 flow pointer"](https://github.com/user-attachments/assets/5ff0050b-f064-46ef-b2fa-e698a2d4f925)

* Step 3: hit close after the progress reach 100%; you will see the flowaccum layer has been added to Layers.

#### (4) ExtractStreams

* Step 1: search "ExtractStreams" in the Processing Toolbox.
* Step 2: select "flowaccum" outputed from above procedure as the input and type output, set the Channelization Threshold as 1000,000, as below

  ![](https://github.com/user-attachments/assets/78cec102-ddaf-42dc-ac85-015b1e487435)

* Step 3: hit close after the progress reach 100%; you will see the stream10_6 layer has been added to Layers.

::::::::::::::::::::::::::::::::::::::: callout


To better see the streams, you could uncheck other layers except the google map layer, and zoom in to compare the generated streams with the ones on the map.

Or we have convert it to vector: Go to Raster | Conversion | Polygonize (Raster to Vector), as below

![](https://github.com/user-attachments/assets/a66ba8b9-90c8-4996-9062-291162c9f7b5)

![](https://github.com/user-attachments/assets/70fa3c47-ce96-4256-9b2c-18cd91ee0a32)

![you can choose different file format of vector](https://github.com/user-attachments/assets/3cf31f5f-78f4-427c-b045-e53013f5b33e)

:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: spoiler

Channelization Threshold
Try different Channelization Threshold and compared the extracted streams.
![](https://github.com/user-attachments/assets/c8d469dd-babe-44a8-8f48-e9800d0a79dd)

::::::::::::::::::::::::



## Calculate Topographic Index
