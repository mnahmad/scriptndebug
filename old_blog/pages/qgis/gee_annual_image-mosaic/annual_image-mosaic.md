# Create Annual Image mosaic using QGIS GEE plugin

Lets create an annual mosaic of Images by using the following code in QGIS python console.

```
import ee
from ee_plugin import Map

Map.setCenter(83.34135,18.54646,20)

s2 = ee.ImageCollection('COPERNICUS/S2').filterDate('2019-01-01', '2019-12-31')


blue    = s2.select('B2').reduce(ee.Reducer.median())
green   = s2.select('B3').reduce(ee.Reducer.median())
red     = s2.select('B4').reduce(ee.Reducer.median())

rgb_stack = ee.Image(blue).addBands(green)
rgb_stack = rgb_stack.addBands(red)

Map.addLayer(rgb_stack,{'bands': 'B4_median,B3_median,B2_median', 'min':0, 'max':5000, 'gamma': 1.4},'RGBTrueColor_median')

```
