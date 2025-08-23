
QGIS Raster Calc

Extract one class from multi class raster 

(layer = value ) * layer 

  

Example 

In a raster pixel value 1 is forest

  

(raster = 1) *  raster 

  

Will give you raster with 1 as forest and zero has nonforest. 

  
  
  

Rescale raster from old values to new values

  
  
  

(("MCE_sample_only _roads@1"  > 0 ) AND ("MCE_sample_only _roads@1" <= 40 )) * 0.2 + (("MCE_sample_only _roads@1"  > 40 ) AND ("MCE_sample_only _roads@1" <= 80 )) * 0.4 +

(("MCE_sample_only _roads@1"  > 80 ) AND ("MCE_sample_only _roads@1" <= 120 )) * 0.6 +

(("MCE_sample_only _roads@1"  > 120 ) AND ("MCE_sample_only _roads@1" <= 160 )) * 0.8 +

(("MCE_sample_only _roads@1"  > 160 ) AND ("MCE_sample_only _roads@1" <= 210 )) * 1

  

ref: [https://gis.stackexchange.com/questions/17712/how-to-perform-raster-reclassification-in-qgis](https://gis.stackexchange.com/questions/17712/how-to-perform-raster-reclassification-in-qgis)