---
layout: page
title: Field Papers part 2
description: Field Papers
---

<a href="https://twitter.com/intent/tweet?text=Field%20Papers%20part%20https://mnahmad.github.io/scriptndebug/pages/fieldpapers/fieldpapers-part2.md%20@mnabiahmad"><img src="https://mnahmad.github.io/scriptndebug/twiter-icon-15.jpg" height="25" width="25"></a>

*Last update: 10/10/2020*

I hope you have enjoyed [part 1](https://mnahmad.github.io/scriptndebug/pages/fieldpapers/fieldpapers.html) of Field Papers. In part 2, we discus two use cases where Field Papers might come handy. The use cases are

1. Field data collection  where
	- you need paper based maps to draw responses
	- Record responses on the device with an offline satellite image

### Paper based maps to draw responses
In first case, the process is straight forward like
1. Goto Field Papers website
2. Select your area
3. Generate an atlas
4. Download atlas as pdf
5. Print pdf
6. Use printed copy in the field to draw your objects
7. Back from the field, scan the printed paper as png/jped etc.
8. Upload to field papers to convert it into a geo referenced Tiff file.
9. Download the geo referenced tiff file.
10. Open the tiff file in QGIS, and start digitizing.   


### Secord responses on the device
In second case, You can skip some of the above steps like 10, as all the object drawing will be happen on the device. All you have to do is

1. Goto Field Papers website
2. Select your area
3. Generate an atlas
4. Download atlas as pdf
5. Convert into png by using the following command (if on Linux)
~~~
convert -density 150 atlas-2apfrt1t.pdf -quality 90 atlas-2apfrt1t.png
~~~
6. Upload to field papers for conversion to geo tiff
7. Download geo tiff, open it in QGISs and start digitizing	  


Note, you can also convert geo tif file to mbtiles for mobile use as well but that a topic for an other post.

Note, it is also good to read this LearnOSM [post](https://learnosm.org/en/mobile-mapping/field-papers/).

Icon references:<br>
<a href="https://icon-library.net/icon/twiter-icon-15.html">Twiter Icon #268986</a>
