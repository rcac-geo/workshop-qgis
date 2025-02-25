---
title: "Introduction"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- Why QGIS?
- How to use QGIS on Clusters?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain why we should use QGIS
- Demonstrate how to start QGIS on Clusters

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction to QGIS

GIS stands for ‘Geographical Information System’. We can use a GIS application, such as ArcGIS and QGIS to manipulate spatial information. 

Why QGIS? It's free and flexible.

 1. Cost-free: Enjoy QGIS without any financial burden. It's completely free, no hidden fees.
 2. Free as in "Do It Your Way": You could extend QGIS to meet your specific needs, sponsor development or contribute your own code.
 3. Works where you work: Run QGIS on macOS, Windows, and Linux (so available for HPC Clusters). 
 4. Always getting better: Benefit from rapid development because anyone can add new features and improve on existing ones.
 6. Never get stuck: Access extensive documentation and a supportive community is there for help.
 7. Easily integrate Artificial Intelligence (AI) and GeoAI.

## Open QGIS on Clusters

We can start QGIS via ThinLinc Client or Gateway. 

#### Start QGIS via ThinLinc

Follow up with [the Setup page](https://rcac-geo.github.io/workshop-qgis/index.html#software-setup), and connect with ThinLinc. To open QGIS as an interactive job, we could go to "Cluster Software" and select "QGIS", as the figure below:

<img width="391" alt="Picture1" src="https://github.com/user-attachments/assets/1df48747-d717-442e-9af5-c25d4dc9f78d" />

Then select the "workshop" queue as below:

<img width="406" alt="Screenshot 2025-02-24 at 4 15 16 PM" src="https://github.com/user-attachments/assets/72d72419-4484-4e6e-9fed-3ec2fdf4920d" />

Then hit "No":

<img width="529" alt="Screenshot 2025-02-24 at 4 15 41 PM" src="https://github.com/user-attachments/assets/e3ea5e98-e83e-4d77-ba9c-bba7c62fbea3" />

Now input two cores and five minutes and hit Okay. You don't need to specifically request memory because memory will be relocated proportional with cores. But if you do, include unit such as "4G".

<img width="608" alt="Screenshot 2025-02-24 at 4 16 10 PM" src="https://github.com/user-attachments/assets/55a2b0be-3bc1-447c-a44d-04c4ec6a7e60" />


::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Look up QGIS version with Terminal?

<img width="186" alt="Screenshot 2025-02-25 at 9 51 03 AM" src="https://github.com/user-attachments/assets/c06429f8-15b6-4242-b416-080085cf8f23" />


:::::::::::::::::::::::: solution 

```sh
module spider qgis
```

:::::::::::::::::::::::::::::::::

## Challenge 2: Start QGIS with Terminal?

How can you open QGIS as an interactive job with Terminal?

:::::::::::::::::::::::: solution 

```sh
sinteractive -A workshop -c4 -t8:00:00
module load qgis
qgis
```

:::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::

#### Start QGIS via Gateway

Gateway, also named Open OnDemand, is a Web interface includes file explorer, interactive apps including QGIS.​ We have to use our own accounts to login Gateway, not the training accounts we used for this workshop. 
Go to [Negishi Gateway](https://gateway.negishi.rcac.purdue.edu), login with our purdue accounts (when we have account on Clusters) and connect QGIS as the figure below.

<img width="911" alt="Screenshot 2025-02-25 at 10 05 05 AM" src="https://github.com/user-attachments/assets/f575bf3a-e6bd-468b-92ad-4a3b93405788" />

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

Inline instructor notes can help inform instructors of timing challenges
associated with the lessons. They appear in the "Instructor View"


You can use standard markdown for static figures with the following syntax:

`![optional caption that appears below the figure](figure url){alt='alt text for
accessibility purposes'}`

![You belong in The Carpentries!](https://raw.githubusercontent.com/carpentries/logo/master/Badge_Carpentries.svg){alt='Blue Carpentries hex person logo with no text.'}
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::




::::::::::::::::::::::::::::::::::::: callout

We could also open QGIS with Gateway, in the way of [Challenge 2](https://rcac-geo.github.io/workshop-qgis/introduction.html#Challenge 2). We could start a terminal as below.

![Start Terminal in Gateway](https://github.com/user-attachments/assets/aac3d529-c726-4793-b3db-e90e55a260fc)


::::::::::::::::::::::::::::::::::::::::::::::::


## Math

One of our episodes contains $\LaTeX$ equations when describing how to create
dynamic reports with {knitr}, so we now use mathjax to describe this:

`$\alpha = \dfrac{1}{(1 - \beta)^2}$` becomes: $\alpha = \dfrac{1}{(1 - \beta)^2}$

Cool, right?

::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
