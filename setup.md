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


:::::::::::::::: spoiler

Open a terminal locally on your laptop and run:

```sh
ssh-keygen -b 4096 -t rsa
```

:::::::::::::::: spoiler
### Callout
this generates the ssh key
::::::::::::::::::::::::

:::::::::::::::: spoiler
### Output
```output
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/your_laptop_account/.ssh/id_rsa):
```
::::::::::::::::::::::::

Now you hit "enter",

:::::::::::::::: spoiler
### Output
```output
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```
::::::::::::::::::::::::

Now you hit "enter" again twice to confirm your input passphrase (no passphrase in this case).

:::::::::::::::: spoiler
### Output
```output
Your identification has been saved in /Users/your_laptop_account/.ssh/id_rsa
Your public key has been saved in /Users/your_laptop_account/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:0vHGCotXkhEg4IKmpJvM92ivPFFyB81l2XgIFTkdsZ8 your_laptop_account@pal-nat187-15-102.itap.purdue.edu
The key's randomart image is:
+---[RSA 4096]----+
|... ..+.+=Ooo    |
|o  . . +.* +.    |
|o+    o . o.     |
|*  . o = +  . .  |
|o   + * S +  E   |
|oo . . * o       |
|oo .o o .        |
|  ooo.           |
|  .++o           |
+----[SHA256]-----+
```
::::::::::::::::::::::::

Now you run:

:::::::::::::::: spoiler
### Windows
```sh
type .ssh\id_rsa.pub | ssh trainXX@negishi.rcac.purdue.edu "mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```
::::::::::::::::::::::::

:::::::::::::::: spoiler
### MacOS / Linux
```sh
cat .ssh/id_rsa.pub | ssh trainXX@negishi.rcac.purdue.edu "mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys"
```
::::::::::::::::::::::::

Then you input the password written in the whiteboard

:::::::::::::::: spoiler
### Callout
this copies the ssh key to trainXX on Negishi
::::::::::::::::::::::::

and then run:

```sh
ssh trainXX@negishi.rcac.purdue.edu
```
:::::::::::::::: spoiler
### Callout
this connects negishi with ssh
::::::::::::::::::::::::

You should be able to land on Negishi without password.
::::::::::::::::::::::::

2. Download the [ThinLinc Client](https://www.cendio.com/thinlinc/download/) and install it to your Laptop.
3. Open ThinLinc Client, then go to Options -> Security, and select "Public key" in the "Anthentication method" as here:
   
   <img width="514" alt="Screenshot 2025-02-21 at 2 27 31 PM" src="https://github.com/user-attachments/assets/1e3e6a5b-8882-4546-b1e3-de313743ad61" />
   
5. Input Server, Username(replace XX with your train number) and Key(correct it with your path of key) like here:
   
   <img width="469" alt="Screenshot 2025-02-21 at 2 27 11 PM" src="https://github.com/user-attachments/assets/7889bdce-6cbd-4cf0-a2eb-a585d83489c4" />
   
6. Hit "Connect".
   
   
## Data Sets

Copy data to your scratch directory:

```sh
rsync -avP /depot/workshop/data/qgis/qgis-data $RCAC_SCRATCH
```
