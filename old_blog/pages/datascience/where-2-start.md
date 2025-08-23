---
layout: page
title: Data science with Python, where to start. Part 1
tagline: Data science, where to start. Part 1
description: Data science, where to start
---
*Last Updated: 19/05/2019*

I started programming back in 1997 while in school, my first language was foxpro, moved to C (in second semester) and ended up programming in Visual Basic (started from version 5). Over the years I learned php, Javascript, python and R. Python turned out to be my favourite language due to huge number of libraries and it is part of my work (Django, data processing etc.). During data processing, I followed some tutorials and videos, thus, thought it would be good share my learning path with others.

__Note__ This is a list of URL I following and not at all comprehensive list. All credit goes to the authors of these tutorials, posts and videos.

### Which python to use
You can use Official [Python](https://www.python.org/
), however for data science [anaconda python](https://www.anaconda.com/distribution/) is recommend, it has all the data science packages thus you don't have to install packages (at least not all of them) like numpy, Scipy, pandas, metaplotlib etc.   

### Integrated Development Environment (IDE)
This is a well discussed question, there are many suggestions like [PyCharm](https://www.jetbrains.com/pycharm/), [Spider](https://www.spyder-ide.org/), [Atom](https://atom.io/) etc. However, for data science, [Jupyter](https://jupyter.org/) and Anaconda Python is highly recommend, you can read more about jupyter at [this link](https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook?utm_source=adwords_ppc&utm_campaignid=1455363063&utm_adgroupid=65083631748&utm_device=c&utm_keyword=&utm_matchtype=b&utm_network=g&utm_adpostion=1t1&utm_creative=332602034364&utm_targetid=aud-299261629574:dsa-473406581035&utm_loc_interest_ms=&utm_loc_physical_ms=9076848&gclid=EAIaIQobChMI_LzB-MeQ4gIVCIXVCh1x1A-OEAAYASAAEgLETPD_BwE).

For beginners, I also suggest [Google CoLab](https://colab.research.google.com/) (if internet accessibility is not an issue) as, in my opinion, it is the fastest way to start coding as Google CoLab provides Jupyter Notebook as IDE.

You can read more abote IDEs at this [link](https://www.datacamp.com/community/tutorials/data-science-python-ide?utm_source=adwords_ppc&utm_campaignid=1455363063&utm_adgroupid=65083631748&utm_device=c&utm_keyword=&utm_matchtype=b&utm_network=g&utm_adpostion=1t1&utm_creative=278443377092&utm_targetid=aud-299261629574:dsa-473406587035&utm_loc_interest_ms=&utm_loc_physical_ms=9076848&gclid=EAIaIQobChMIkN-Oo-2l4gIVkUPTCh3h6gN7EAAYASAAEgJ99PD_BwE).

Recently, I have moved to dockers and started using [continuumio anaconda docker image](https://hub.docker.com/r/continuumio/anaconda3/). If you are not familiar with docker I suggest you read more about it first. The continuumio anaconda docker image uses Debian Linux and anaconda python, thus, is perfect for data scientist. I will write an other blog in future about how I am using this image for my work.    

### Where to start
The best tutorial website I found is [tutorials point](https://www.tutorialspoint.com/python/). I suggest any one learning python should start form this website.   

I highly recommend that you complete all topic on this website.

### Object Oriented Programming (OOP)
Python 2.7 End of Life (EOL) is on 1st January 2020, [reference](https://www.anaconda.com/end-of-life-eol-for-python-2-7-is-coming-are-you-ready/), thus, beginners better start from Python 3.

There are many OOP tutorials for python 3, however, I followed this [Youtube video](https://www.youtube.com/watch?v=ZDa-Z5JzLYM&amp=&feature=youtu.be&amp=&fbclid=IwAR1adWPPtb_wIVn9v8qr_fyNC4lBYD3xtu0kWYA6FGefpsK_zfWrdS9Sfgg) series. Its short but explains all the necessary bits and pieces.  

#### Some essential topics

##### dictionary
An other topic one should master is python dictionary, although it is cover in the tutorial above, however, I followed this [Youtube video](https://www.youtube.com/watch?v=daefaLgNkw0).  

##### Regular expression
During data processing, some time one needs to search big files for certain string patterns or load files with different names from single/multiple folders. Like return all the /lines starting from "A", have number and ends with "Z" like "A2Z" or "Y2Z" OR load all files that a certain string patten in their name. Regular expression is the solution for such cases, thus, have a look at this [Youtube video](https://www.youtube.com/watch?v=WQlKPdKVXfw&amp=&index=11&amp=&fbclid=IwAR256F4TxtMmIR7_YfvdqZDtUFTsl3vXZatXrm9XYG4R_sFE2CRfiMY4-CE) and this [amazing post](https://medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285)


#### Some essential libraries
Some important libraries that you should know as they are essential for data science (and other fields).

__numpy__

After basic tutorial, I also read [this post](https://towardsdatascience.com/practical-numpy-understanding-python-library-through-its-functions-adf2e3841894) and an other post at [this link](https://medium.com/fintechexplained/why-should-we-use-numpy-c14a4fb03ee9).

__Pandas__

 If you have not work with pandas before, it is the right time. Have a look at [this excellent post](https://medium.com/kitepython/pandas-tutorial-da4dd84edd00)

__Plotly__
One aspect of data science is data visualization, thus, you will need graphs and plotly will come handy so have a look at [this link](https://towardsdatascience.com/the-next-level-of-data-visualization-in-python-dd6e99039d5e) and [this link](https://techarena51.com/blog/how-to-visualise-data-in-python-3-with-plotly/?utm_source=fb-page&fbclid=IwAR3eP1wi67PSo7-zo2DqDGS3Wv9ZdRnwRdOC0gOHDRyY3C0pUtiJ1_kDDko).

__metaplotlib__
Also have a look at metaplotlib.

__seaborn__

Seaborn is build on metaplotlib. Have a look at [this nice post](https://medium.com/@neuralnets/data-visualization-with-python-and-seaborn-part-1-29c9478a8700).

__Scikit__

[this link](https://towardsdatascience.com/an-introduction-to-scikit-learn-the-gold-standard-of-python-machine-learning-e2b9238a98ab)

[this link](https://www.youtube.com/watch?v=Yd5oEIBFQ_E)

__pathlib__
You will be loading data from different paths, thus, pathlib will come handy so have a look at [this link](https://treyhunner.com/2018/12/why-you-should-be-using-pathlib/?fbclid=IwAR3JpO679KfQuZjfB4eRBH4nX4eIvU2MsQpWsj6Em7HoSqkNnRQJI9l_Odc).

There are a lot of libraries, you need to keep you self uptodate with new libraries like for example have a look at these [top 7 libs](https://heartbeat.fritz.ai/top-7-libraries-and-packages-of-the-year-for-data-science-and-ai-python-r-6b7cca2bf000).  


### Statistics
Before jumping into data science topics, its good to know statistics as you will be using a lot of techniques in data science.

For this, I took help from [this post](https://towardsdatascience.com/python-tutorial-short-stop-to-introduce-main-statistical-concepts-8213724550f4) and also read about some of the concepts on [this website](https://towardsdatascience.com/python-tutorial-short-stop-to-introduce-main-statistical-concepts-8213724550f4) and in [this post](https://medium.com/diogo-menezes-borges/introduction-to-statistics-for-data-science-16a188a400ca).


Also read [this post](https://medium.com/@Saslow/simulating-probability-events-in-python-5dd29e34e381) for probability analysis.  Finally, I also take help from [this link]((https://www.dummies.com/education/math/statistics/))

### Data Science
Its all about data processing, to learn the trends and insights out of data. But before we can start data analysis, we need to learn data cleaning. Its rare that you will find clean analysis ready data. data cleaning is the first tasks of data science.
[this link](https://towardsdatascience.com/the-complete-beginners-guide-to-data-cleaning-and-preprocessing-2070b7d4c6d)

A good start is to watch [this video](https://www.youtube.com/watch?v=eTxyviU0Ddo) about data science, In the video description you will see link to [github book](https://github.com/jakevdp/PythonDataScienceHandbook/blob/8a34a4f653bdbdc01415a94dc20d4e9b97438965/notebooks/Index.ipynb) by Jake VanderPlas. Its an excellent book.   

#### Exploratory data analysis
The first step in data science is to learn about your data, what it contains like columns, number of rows, basic patterns etc. For exploratory data analysis I read [this post ](https://towardsdatascience.com/exploratory-data-analysis-8fc1cb20fd15) and it is excellent.

This is the end of part 1. In future, I will show some case studies and hopefully show some specific examples.
