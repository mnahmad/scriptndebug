# How to install and use Earth Engine plugin in QGIS 3.


### Installation
This part was not very obvious to me in the beginning

```
sudo pip3 install earthengine-api
```

for python 2

```
sudo pip install earthengine-api
```


Now an other step I found in the GEE python [documentation](https://developers.google.com/earth-engine/python_install-conda.html) was to get oauth2 key for your GEE account by using the following command in . Open terminal and run the following command.  

```
earthengine authenticate
```

the above command will show

```

Running command using Cloud API.  Set --no-use_cloud_api to go back to using the API

To authorize access needed by Earth Engine, open the following URL in a web browser and follow the instructions. If the web browser does not start automatically, please manually browse the URL below.

    https://accounts.google.com/o/oauth2/auth?client_id=????????????-.............

The authorization workflow will generate a code, which you should paste in the box below.
Enter verification code: --------------your auth key here -------------------------

Successfully saved authorization token.

```

Now you can use the QGIS plugin


The python code to load and search for images
```
import ee
from ee_plugin import Map

Map.setCenter(83.34135,18.54646,20)

image = ee.ImageCollection("COPERNICUS/S2").filterBounds(Map.getCenter()).first()
Map.addLayer(image,{'bands': 'B4,B3,B2', 'min':0, 'max':5000, 'gamma': 1.4},'RGBTrueColor');

```

Image annual mosaic code

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
