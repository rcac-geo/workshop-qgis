---
title: Setup
---

Welcome to Hands-on with QGIS
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
| 10:00 AM | Arrival & Setup  |
| 10:30 AM | Introduction & Open QGIS on Clusters |
| 11:00 AM | View Spatial Data |
| 12:00 PM | Lunch Break |
| 1:00 PM | Project: 	Exploring landscape around Purdue |
| 2:30 PM | Break |
| 3:00 PM | Coding with QGIS: Python Console |
| 4:30 PM | Wrap-Up & Discussion |


## Software Setup


::::::::::::::::::::::::::::::::::::::: discussion

### Details

1. SSH key setup for different systems is detailed in the expandable sections below.
2. Download the [ThinLinc Client](https://www.cendio.com/thinlinc/download/) and install it to your Laptop.
3. Open ThinLinc Client, then go to Options -> Security, and select "Public key" in the "Anthentication method" as here:
   <img width="514" alt="Screenshot 2025-02-21 at 2 27 31 PM" src="https://github.com/user-attachments/assets/1e3e6a5b-8882-4546-b1e3-de313743ad61" />
4. Input Server, Username(replace XX with your train number) and Key(correct it with your path of key) like here:
   <img width="469" alt="Screenshot 2025-02-21 at 2 27 11 PM" src="https://github.com/user-attachments/assets/7889bdce-6cbd-4cf0-a2eb-a585d83489c4" />
5. Hit "Connect".
:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: spoiler

### Windows

Open a terminal and run:

```sh
ssh-keygen -b 4096 -t rsa
type .ssh\id_rsa.pub | ssh trainXX@negishi.rcac.purdue.edu "mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```
Now you input the password written in the whiteboad, and run:
```
exit
ssh trainXX@negishi.rcac.purdue.edu
```
You should be able to return to Negishi without password.
::::::::::::::::::::::::

:::::::::::::::: spoiler

### MacOS and Linux

Open Terminal and run
```sh
ssh-keygen -b 4096 -t rsa
cat .ssh/id_rsa.pub | ssh trainXX@negishi.rcac.purdue.edu "mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```
Now you input the password written in the whiteboad, and run:
```
exit
ssh trainXX@negishi.rcac.purdue.edu
```
You should be able to return to Negishi without password.
::::::::::::::::::::::::


   
## Data Sets

Copy data to your scratch directory:

```bash
rsync -avP /depot/workshop/data/qgis/qgis-data $RCAC_SCRATCH
```

The worked out folder is available at `/depot/workshop/data/genome-assembly/genome-assembly-data` on the training cluster. You can copy the data to your scratch space using the following command:

```bash
rsync -avP /depot/workshop/data/qgis/qgis-data $RCAC_SCRATCH
```
