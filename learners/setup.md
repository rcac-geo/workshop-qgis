---
title: Agenda
---

## Welcome to Hands-on with QGIS
---

Welcome to the Hands-on with QGIS Workshop, where you'll learn to navigate and utilize QGIS, a powerful open-source Geographic Information System (GIS).

What You'll Learn:

1. **Get Started with QGIS.** We'll cover the basics of opening QGIS on clusters, loading and viewing spatial data, and installing plugins such as QuickMapServices and WhiteboxTools.
  * Introduction
  * Open QGIS on Clusters
  * View Spatial Data

2. **Project: 	Exploring landscape around Purdue.** Through a hands-on project, you'll learn to apply raster analysis techniques to explore the landscape around Purdue University. Specifically, you'll work with: 
  * Slope
  * Hill shade
  * Stream and watershed
  * Raster to Vector

3. **Coding with QGIS: Python Console.** Take your analysis to the next level by learning how to write Python scripts using the QGIS Python Console. You'll learn how to automate geospatial tasks, such as replicating the same tasks you performed in the "Exploring Landscape around Purdue" project, but this time using code. By automating these tasks, you'll be able to streamline your workflow and increase efficiency.

## Schedule

| **Time**  | **Session**  |
|:---|-------------|
| **10:00 AM** | Arrival & Setup  |
| **10:30 AM** | Introduction & Open QGIS on Clusters |
| **11:00 AM** | View Spatial Data |
| **12:00 PM** | Lunch Break |
| **1:00 PM** | Project: 	Exploring landscape around Purdue |
| **2:30 PM** | Break |
| **3:00 PM** | Coding with QGIS: Python Console |
| **4:30 PM** | Wrap-Up & Discussion |


## Software Setup

::::::::::::::::::::::::::::::::::::::: discussion

### Details

1. Download the [ThinLinc Client](https://www.cendio.com/thinlinc/download/) and install it to your Laptop.
2. SSH key setup for different systems is detailed in the expandable sections below.

:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: spoiler

### Windows

Open a terminal and run:

```sh
ssh-keygen -b 4096 -t rsa
type .ssh\id_rsa.pub | ssh trainXX@negishi.rcac.purdue.edu "mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```

::::::::::::::::::::::::

:::::::::::::::: spoiler

### MacOS

Open Terminal and run
```sh
ssh-keygen -b 4096 -t rsa
cat .ssh/id_rsa.pub | ssh trainXX@negishi.rcac.purdue.edu "mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```

::::::::::::::::::::::::


:::::::::::::::: spoiler

### Linux

Open a terminal and run:
```sh
ssh-keygen -b 4096 -t rsa
cat .ssh/id_rsa.pub | ssh trainXX@negishi.rcac.purdue.edu "mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```

::::::::::::::::::::::::


## Data Sets

<!--
FIXME: place any data you want learners to use in `episodes/data` and then use
       a relative link ( [data zip file](data/lesson-data.zip) ) to provide a
       link to it, replacing the example.com link.
-->
Download the [data zip file](https://example.com/FIXME) and unzip it to your Desktop
