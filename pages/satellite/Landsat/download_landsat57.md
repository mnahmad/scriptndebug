---
layout: page
title: Landsat Images download
tagline: Landsat 5 7 8
description: Landsat 5 7 8 downloads
---
*Last Updated: July 2017*

Around a year ago, I came across [landsat_util](https://pythonhosted.org/landsat-util/) that can be used to download Landsat 8 images. It can searches, process and download images from servers.

But what if one has to download Landsat 5/7 images. I googled for such a utility and found an answer on [StackExchange](http://gis.stackexchange.com/questions/124561/is-there-a-ftp-to-get-landsat-images). The utility is called "LANDSAT-Download" and its written in python. Although one does not need to know python to run this program but its good to know as you might have to look at this script (as in my case, I will explain it later).

### Installation
The code for LANDSAT-Download is available at [LANDSAT-Download](https://github.com/olivierhagolle/LANDSAT-Download) git repository. Download the code (fork if you want to enhance this code).

Make sure you have python 2.7 installed on your computer

### Usage
Usage is very simple, for Example, I wanted to see what options script can support, thus, used the following command

```
python download_landsat_scene.py -h
```

or

```
./download_landsat_scene.py -h
```

The script requires USGS EarthExplorer authentication this you have to register with USGS. Once you get login and password, save them in the file usgs.txt.

Password file should be like

```
username password
```

For example

```
Tom Harrison

```

Note: No spaces or tabs at the end of the file.

Check README.md for documentation as it explains usage with different options.

In my case, I had to download Landsat 5 scenes from around 150 locations for specific years (2010-2011). I created a csv file with ID and PathRow (see below)

```
ID , PR
1  , 168060
2  , 169060
3  , 170060
4  , 171060
```

I wrote a bash script to read this CSV and loop through each PathRow (PR) shown below.   

```bash
#!/bin/bash

clear

INPUT=landsat_pathrow.csv
OLDIFS=$IFS
IFS=,
[ ! -f $INPUT ] && { echo "$INPUT file not found"; exit 99; }


cd  landsat-Download-master_v3

counter=0

while read ID PR
do

	echo $PR "#"

	#make new folder with the name of PR
	new_folder="/home/user/landsat/LS5/"$PR

	# save messages in a file for later review
	output="/home/user/landsat/LS5/"$PR

	echo $new_folder

	# some how mkdir without full path was not working
	/bin/mkdir -p $new_folder

	# output will go to a log file called results.txt
	./download_landsat_scene.py -o scene -b LT5 -d 20100101  -f 20111231 -s $PR -c 10 -u usgs.txt --output $new_folder > $output/result.txt

done < $INPUT

IFS=$OLDIFS

```

I found out that the script has to have ground station IDs to download the image, actually the script uses station IDs to generate a URL request. Thus, I needed to know [Landsat 5 era](http://landsat.usgs.gov/about_landsat5.php) to see which stations were active during that era. I got [current ground stations](http://landsat.usgs.gov/about_ground_stations.php) but I need historic LS 5 era ground stations, thus, I needed info. which i found from [this](http://landsat.usgs.gov/Historical_IGS.php) document. I used the ground station IDs of Landsat 5 to modify the script (at 2 places) so that script can search for specific stations. You can see my small modification to the script at [line430 ](https://github.com/mnahmad/LANDSAT-Download/blob/b7d4ddaad2bf2bd0a2c247025dab8780a6600523/download_landsat_scene.py#L430) and [line582](https://github.com/mnahmad/LANDSAT-Download/blob/b7d4ddaad2bf2bd0a2c247025dab8780a6600523/download_landsat_scene.py#L582).


It worked for me, however, I faced some of the issues like

1) Connection reset by server.

2) Some images can be seen on EarthExplorer but download_lantsat cannot find these images.


Also read about L1T product and naming convention for Landsat.
