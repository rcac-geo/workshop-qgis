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
    ** Basin ** → contains multiple → ** Sub-Basins ** → made up of → ** Watersheds ** → includes smaller → ** Catchments **
 
## Install Plugins

## Merge DEM Data
## Calculate Slope
## Calculate Hillshade
## Analyze Hydrology
## Calculate Topographic Index
