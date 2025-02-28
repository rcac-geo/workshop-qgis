---
title: Setup
---

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

1. SSH key setup for different systems is detailed in the expandable sections below.
2. Download the [ThinLinc Client](https://www.cendio.com/thinlinc/download/) and install it to your Laptop.
3. Open ThinLinc Client, then go to Options -> Security, and select "Public key" in the "Anthentication method" as here:
   
   <img width="514" alt="Screenshot 2025-02-21 at 2 27 31 PM" src="https://github.com/user-attachments/assets/1e3e6a5b-8882-4546-b1e3-de313743ad61" />
   
5. Input Server, Username(replace XX with your train number) and Key(correct it with your path of key) like here:
   
   <img width="469" alt="Screenshot 2025-02-21 at 2 27 11 PM" src="https://github.com/user-attachments/assets/7889bdce-6cbd-4cf0-a2eb-a585d83489c4" />
   
6. Hit "Connect".

::::::::::::::::::::::::::::::::::::::: discussion
   
:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: spoiler

### Windows

Open a terminal locally on your laptop and run:

```sh
ssh-keygen -b 4096 -t rsa
```

:::::::::::::::: spoiler
this generates the ssh key
::::::::::::::::::::::::

```sh
type .ssh\id_rsa.pub | ssh trainXX@negishi.rcac.purdue.edu "mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```
Now you input the password written in the whiteboard

:::::::::::::::: spoiler
this copies the ssh key to trainXX on Negishi
::::::::::::::::::::::::

Now run:

```sh
ssh trainXX@negishi.rcac.purdue.edu
```
You should be able to land on Negishi without password.
::::::::::::::::::::::::

:::::::::::::::: spoiler

### MacOS / Linux

Open Terminal locally on your laptop and run
```sh
ssh-keygen -b 4096 -t rsa
```
:::::::::::::::: spoiler
this generates the ssh key
::::::::::::::::::::::::

```sh
cat .ssh/id_rsa.pub | ssh trainXX@negishi.rcac.purdue.edu "mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```
Now you input the password written in the whiteboard, 

:::::::::::::::: spoiler
this copies the ssh key to trainXX on Negishi
::::::::::::::::::::::::

Now run:

```sh
ssh trainXX@negishi.rcac.purdue.edu
```
You should be able to land on Negishi without password.
::::::::::::::::::::::::


   
## Data Sets

Copy data to your scratch directory:

```sh
rsync -avP /depot/workshop/data/qgis/qgis-data $RCAC_SCRATCH
```
