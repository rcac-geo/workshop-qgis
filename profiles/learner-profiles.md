---
title: Advice for Geospatial Computations
---

## Advice for Geospatial Computations

When performing geospatial computations involving multiple datasets, ensure they are all in the same Coordinate Reference System (CRS).

* Why it's important:
  - CRSs define how geographic locations are represented on a flat surface (or a 3D globe).
  - If datasets have different CRSs, their spatial relationships will be distorted, leading to inaccurate calculations (e.g., distances, areas, overlaps).
  - Think of it like trying to measure distances on two maps with different scales or projections—the results would be meaningless.

* Practical advice:
  - Check: Before any analysis, always examine the CRS of each dataset.
  - Unify: If the CRSs differ, use geoprocessing tools (e.g., "reproject," "project raster") to transform all datasets to a single, consistent CRS.
  - Choose wisely: Select a CRS that is appropriate for your study area and the type of analysis you are performing. For example, projected coordinate systems for smaller areas, and geographic coordinate systems for global analysis.
  - Document: keep records of the original CRS of each dataset, and the CRS that you reprojected the data to. This will help with reproducibility.

## Additional Reading

### To learn more about QGIS:

- [QGIS User Guide](https://docs.qgis.org/3.40/en/docs/user_manual/index.html)
  - [Call alogorithms from Python Console](https://docs.qgis.org/3.40/en/docs/user_manual/processing/console.html#calling-algorithms-from-the-python-console)

- [QGIS Training Manual](https://docs.qgis.org/3.40/en/docs/training_manual/index.html#qgis-training-manual)

- [A Gentle Introduction to GIS](https://docs.qgis.org/3.40/en/docs/gentle_gis_introduction/index.html)

- [PyQGIS Developer Cookbook](https://docs.qgis.org/3.40/en/docs/pyqgis_developer_cookbook/index.html)
  - [QGIS with standalone python](https://docs.qgis.org/3.40/en/docs/pyqgis_developer_cookbook/intro.html#using-pyqgis-in-standalone-scripts)

### To learn more about WhiteBoxTools:

- [WhiteBoxTools User Manual](https://www.whiteboxgeo.com/manual/wbt_book/available_tools/index.html)

### To learn more about monitor usage:

- [Monitor Manual](https://resource-monitor.readthedocs.io/en/latest/getting_started.html)

### To learn more about submitting jobs on HPC Clusters:

- [Submit Jobs](https://www.rcac.purdue.edu/training/clusters201)
