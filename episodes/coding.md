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
- Demonstrate how to automate QGIS tasks using Python coding and processing from the command line.
- Demonstrate how to monitor CPU and memory usage.

::::::::::::::::::::::::::::::::::::::::::::::::

## QGIS Python Console

- The QGIS Python Console is an interactive shell for Python command executions.
- It also has a Python file editor that allows you to edit and save your Python scripts.
- Modules from QGIS (analysis, core, gui, server, processing, 3d) and Qt (QtCore, QtGui, QtNetwork, QtWidgets, QtXml) as well as Python’s math, os, re and sys modules are already imported and can be used directly (25.3. QGIS Python Console — QGIS Documentation  Documentation, n.d.).

  The screenshots below show how to open QGIS Python Console, and how it looks like.

<img width="595" alt="Screenshot 2025-03-04 at 10 58 51 AM" src="https://github.com/user-attachments/assets/3157328b-18c8-43bf-b0a7-a434496de234" />


<img width="1048" alt="Screenshot 2025-03-04 at 11 00 04 AM" src="https://github.com/user-attachments/assets/79248436-7123-46cc-814c-d09074375c7f" />

Let's create an output directory through Terminal, you should replace trainXX with your training account.

```sh
mkdir -p /scratch/negishi/trainXX/project/code_output
```

Let's copy the code below to the python console.

```python
# change work directory
path ="/scratch/negishi/trainXX/project/code_output"
os.chdir(path)
```

### Load Data

You can load data in two ways, depending on if you want it on the QGIS map canvas. Choose the first method if you only require computation; select the second if visualization is also needed.

#### The first way

There are two steps to load data. 

* Step 1: data is loaded in memory.
  
* Step 2: the data is added to QGIS map canvas. This is not necessary if you just do computation and do not visualize data.

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

Now it gets added to the QGIS map canvas.

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

It loads a vector or raster layer and immediately adds it to the map canvas

##### (1) Load Vector Data

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

### Merge DEM Data

```python
rlayer = QgsRasterLayer(path_to_tif, "dem")
rlayer2 = QgsRasterLayer(path_to_tif2, "dem2")

# Merge rasters
processing.run("gdal:merge", {"INPUT": [rlayer, rlayer2], "OUTPUT": "merged_dem.tif"})

#check the merged_dem
iface.addRasterLayer("merged_dem.tif","merged_dem")
```

### Calculate Slope

```python
# Calcualting slope
processing.run("qgis:slope", {"INPUT": "merged_dem.tif", "OUTPUT": "slope.tif"})

#check it 
iface.addRasterLayer("slope.tif","slope")
```

You may wonder how to easily write the python code to perform tasks. Well, QGIS provide a smart way.

:::::::::::::::::::::::: spoiler 
### Hint

Step 1: Search the processing in the Processing Toolbox with QGIS interface, and fill in all the parameters.

Step 2: Click "Advanced", and select "Copy as Python Command".

Step 3: Paste it to run in the python console. 

:::::::::::::::::::::::::::::::::

### Calculate Hillshade

```python
processing.run("native:hillshade", {'INPUT':'merged_dem.tif','Z_FACTOR':1,'AZIMUTH':300,'V_ANGLE':40,'OUTPUT':'hillshade.tif'})

```

## Using processing from the command line

QGIS includes the Processing Executor, a command-line tool that enables the execution of QGIS processing algorithms and models (23.8. Using Processing From the Command Line — QGIS Documentation  Documentation, n.d.), including those from plugins, outside of the QGIS Desktop interface.

To use it, Let first close QGIS application, and then we will submit a job to HPC Cluster. 

* Step 1: Let's start a new file named "myhydrojob" and copy in the code below. 

```sh

#!/bin/sh -l
# FILENAME:  myjob10_4

#SBATCH -A workshop
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8 
#SBATCH --time=00:10:00
#SBATCH --job-name myhydro_job
#SBATCH --output=/home/liu4201/jobs/hydro10_4.out    ## replace with your own path
#SBATCH --error=/home/liu4201/jobs/hydro10_4.out     ## replace with your own path

module reset
module load qgis
module load monitor

export QT_QPA_PLATFORM=offscreen

monitor cpu percent --sample-rate 10 --total > cpu.log &
monitor cpu memory --sample-rate 10 --actual -H > mem.log &

workdir=/scratch/negishi/liu4201/project/code_output  ## replace with your own path

qgis_process run wbt:FillDepressionsWangAndLiu  -- dem=$workdir/merged_dem.tif output=$workdir/fillsinks.tif
qgis_process run wbt:D8Pointer  -- dem=$workdir/fillsinks.tif output=$workdir/flowdirect.tif
qgis_process run wbt:D8FlowAccumulation --distance_units=meters --area_units=m2 --ellipsoid=EPSG:7030 --input=$workdir/flowdirect.tif --out_type=0 --log=false --clip=false --pntr=true --esri_pntr=false --output=$workdir/flowaccum.tif
qgis_process run wbt:ExtractStreams --distance_units=meters --area_units=m2 --ellipsoid=EPSG:7030 --flow_accum=$workdir/flowaccum.tif --threshold=10000 --zero_background=false --output=$workdir/stream10_4.tif
qgis_process run wbt:Subbasins --distance_units=meters --area_units=m2 --ellipsoid=EPSG:7030 --d8_pntr=$workdir/flowdirect.tif --streams=$workdir/stream10_4.tif --esri_pntr=false --output=$workdir/subbasins10_4.tif
qgis_process run wbt:WetnessIndex --distance_units=meters --area_units=m2 --ellipsoid=EPSG:7030 --sca=$workdir/subbasins10_4.tif --slope=$workdir/slope.tif --output=$workdir/wetnessIndex10_4.tif

```

:::::::::::::::::::::::: spoiler 
### Hint

Step 1: Search the processing in the Processing Toolbox with QGIS interface, and fill in all the parameters.

Step 2: Click "Advanced", and select "Copy as qgis_process Command".

Step 3: Paste it to run in the job script. 

:::::::::::::::::::::::::::::::::

* Step 2: Then we could submit the job with typing the code below in Terminal.

```sh
sbatch myhydrojob
```

:::::::::::::::::::::::: callout 

monitor is a module to monitor your resources, such as cpu and memory. You can look up for help after loading the module, as below.

To look up help for "monitor", after "module load monitor", run
```sh
monitor --help
```
To look up help for "qgis_process", after "module load qgis", run
```sh
qgis_process --help
```
:::::::::::::::::::::::::::::::::

## Coding with Standalone Python

Now let's experiment on a different Channelization Threshold, 10,000 by coding with standalone Python Script. 

* Step 1: Start a new python script named "hydro_10_5.py" and copy in the code below. You should replace the path with your own where it is noted.

```python
import os
from qgis.core import *
import sys

# initialize qgis
qgs_app = QgsApplication([], False)
qgs_app.initQgis()

#add whiteboxTools path
module_path = "/home/liu4201/apps/qgis_tools/WhiteboxTools_linux_amd64/WBT" ## replace with your own path
sys.path.append(module_path)

#import processing tools
import whitebox as wbtool
#from qgis import processing
#from processing.core.Processing import Processing

#Processing.initialize()
# change work directory
path ="/scratch/negishi/liu4201/project/code_output/"  ## replace with your own path
os.chdir(path)

#for alg in QgsApplication.processingRegistry().algorithms():
#    print(alg.id(), "->", alg.displayName())

wbt = wbtool.WhiteboxTools()

#processing.run("native:hillshade", {'INPUT':'merged_dem.tif','Z_FACTOR':1,'AZIMUTH':300,'V_ANGLE':40,'OUTPUT':'hillshade.tif'})

wbt.extract_streams(flow_accum = path + "flowdirect.tif",
                   threshold=100000,
                   zero_background=False,
                   output= path + "stream10_5.tif")
wbt.subbasins(d8_pntr= path + "flowdirect.tif", streams= path + "stream10_5.tif",esri_pntr=False, output= path + "subbasins10_5.tif")
wbt.wetness_index(sca= path + "subbasins10_5.tif", slope= path + "slope.tif", output= path + "wetnessIndex10_5.tif")

qgs_app.exitQgis()

```

:::::::::::::::::::::::: spoiler 

Note 1: Refer [WhiteBoxTools User Manual](https://www.whiteboxgeo.com/manual/wbt_book/available_tools/index.html) for the code to use the algorithm, "Copy as Python Command" provided by QGIS does not match the real WhiteBoxTools algorithms.

Note 2: Refer to the code commented out in the snippet to use processing tools provided by QGIS (for example, native:hillshade). To highlight, it's necessary to include the code below in the right place.

```python
from qgis import processing
from processing.core.Processing import Processing

Processing.initialize()
```

:::::::::::::::::::::::::::::::::


* Step 2: Start a file named "myjob10_5" and copy the code below in. You should replace the path with your own where it is noted in parenthesis.

```sh
#!/bin/sh -l
# FILENAME:  myjob10_5

#SBATCH -A workshop
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8 
#SBATCH --time=00:10:00
#SBATCH --job-name myhydro_job
#SBATCH --output=/home/liu4201/jobs/hydro10_5.out  ## replace with your own path
#SBATCH --error=/home/liu4201/jobs/hydro10_5.out   ## replace with your own path

module reset
module load qgis
module load monitor

export QT_QPA_PLATFORM=offscreen

monitor cpu percent --sample-rate 10 --total > cpu1.log &
monitor cpu memory --sample-rate 10 --actual -H > mem1.log &

python /home/liu4201/qgis_data/code/hydro_10_5.py  ## replace with your own path
```

* Step 3: Submit your job via running the code below in terminal.

```sh
sbatch myjob
```

:::::::::::::::::::::::: spoiler 

The export QT_QPA_PLATFORM=offscreen command tells Qt (the GUI framework used by QGIS) to use the "offscreen" platform plugin.

:::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- To automate geospatial tasks with QGIS algorithms, we can use three coding approaches: the QGIS Python Console, standalone Python scripts, and command-line execution.
- For QGIS Python Console, data can be loaded in two ways depending on whether you want to add it to the QGIS map canvas.
- Standalone Python scripts and command-line execution allow us to submit jobs to HPC clusters, enabling enhanced automation of QGIS geospatial tasks.
- We monitor CPU and memory usage within jobs to guide our computation resource requests.

::::::::::::::::::::::::::::::::::::::::::::::::
