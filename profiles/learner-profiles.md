---
title: Advice for Geospatial Computations
---

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
