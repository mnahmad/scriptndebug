---
layout: page
title: Gdal tips
tagline: gdal
description: Gdal commands and tips
---
*Last updated: 20/2/2018*

This blog is about Gdal commands and their usage with examples.

### make a stack
One can create image stack any software like QGIS (it also uses the gdal), R etc. However, if one has a lot of images and wants to script the process one can also use Gdal.


In the example below, I am using gdal to make a stack of landsat 5 bands.

```bash
gdal_merge.py -separate -of GTiff -o  merge_ls5.TIF LT51680602011234MLK00_B1.TIF  LT51680602011234MLK00_B3.TIF  LT51680602011234MLK00_B4.TIF  LT51680602011234MLK00_B5.TIF  LT51680602011234MLK00_B6.TIF  LT51680602011234MLK00_B7.TIF
```


### Resample

First, you need to know the resample resolution of an image. If you already have a target image that you resample your sourced image to, then use the gdalinfo command to know the resolution of target image. I want to resample an image to 0.250000000000000.

```bash
gdalwarp -tr 0.250000000000000 -0.250000000000000 3B-DAY-L.GIS.IMERG.20140331.V04A.tif

```
