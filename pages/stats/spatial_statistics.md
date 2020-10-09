---
layout: page
title: Summery of Zonal, Focal, local and Global operations
description: Zonal Focal local Global
---
*Last update: 09/10/2020*

Its always helpful to know some of the basic spatial statistical concepts while working with GIS datasets especially raster datasets. Following are some basic concepts

__Note:__ These are my own notes thus only cover summery of the actual concept.

__Zonal:__<br>
Calculate statistics from raster images for geometry like polygon. The statistics include

1. sum of all pixel values inside polygon
2. mean of all pixel values inside polygon
3. total count
4. ....


Example:
How much rain occers inside a watershed in a month or in the past few years. The input raster in this example could be TRMM or GPM and watershed boundary from (catchment area analysis for a project).

__Focal:__<br>
Cell value is depending on the values of its neighbours. Usually there is 3x3 (total 9 cells) matrix/window and based on values from all cells in window/matrix centre cell value is determined.

Such type of statistical techniques are used to smooth raster surfaces to get more homogeneous values.

__Local:__<br>
This type of statistics is simple map algebra like adding, subtracting, multiplying layers etc.

__Global:__<br>
Apply changes to all cells based on some operations for examples, euclidean distance of cells from a cell to get shortest distance between two locations (cells).

Example:<br>
After disaster, how accessible an area is, however, one needs before disaster and after disaster cost surfaces.

References:<br>
[Map Algebra: Global, Zonal, Focal and Local Operations](https://gisgeography.com/map-algebra-global-zonal-focal-local/)

*Note: Is post is a work in progress.*
