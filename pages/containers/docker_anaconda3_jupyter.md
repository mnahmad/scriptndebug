---
layout: page
title: Using Continuumio Docker image for python anaconda3
tagline: docker python anaconda3
description: Using Continuumio Docker image for python anaconda3
---

<a href="https://twitter.com/intent/tweet?text=<title with %20 for each space>%20https://mnahmad.github.io/scriptndebug/pages/<url-post>%20@mnabiahmad"><img src="https://mnahmad.github.io/scriptndebug/twiter-icon-15.jpg" height="25" width="25"></a>

*Last update: --/--/----*

#


[https://github.com/ContinuumIO/docker-images/tree/master/anaconda3](https://github.com/ContinuumIO/docker-images/tree/master/anaconda3)


```
docker run -i -t -p 8888:8888 continuumio/anaconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser --allow-root"
```


How to know which image is running

```
docker ps
```

If you want CLI access to docker

```
docker exec -it docker_id /bin/bash


-i --interactive: Take user to container CLI
-t -- tty

-d detach: run in detach mode

```

the docker_ID will come form the ps command

Now your note book is installed at /opt/notebooks and all your notebooks are inside that folder. But when you will shut docker container, the notebook will be deleted. To save your code, you can download your code as notebook by going to File- Download as - Notebook. This way your code will be downloaded onto your computer and when you start the container next time just load the downloaded notebook.

the other way is to load a host folder as volume

```
docker run -v /host/directory:/container/directory -other -options image_name command_to_run
```
this way if you save your code, while in docker container, it will be save on local drive.

like

```
docker run -v /Users/AMuhammad/Downloads/mynotebooks:/opt/notebooks/mynotebooks -i -t -p 8888:8888 continuumio/anaconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser --allow-root"


OR

docker run -v /Users/AMuhammad/mynotebooks:/opt/notebooks/mynotebooks -i -t -p 8888:8888 continuumio/anaconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser --allow-root"


```

It is much better option to load your code, work on it and then save it (and it will be saved on host).

```
docker stop docker_container_id
```


work with iris data https://towardsdatascience.com/knn-using-scikit-learn-c6bed765be75




## Installations inside container
From time to time, I test different libraries inside this container. This second covers the installation steps, issues and their solution and basic working of libraries.

### pandas profiling

Installation and activation:

1. `docker ps` to get container id
2. `docker exec -it docker_id /bin/bash` to start shell session
3. `pip install -U pandas-profiling[notebook]` code taken from [official blog](https://pandas-profiling.github.io/pandas-profiling/docs/master/rtd/pages/introduction.html)
4. `jupyter nbextension enable --py widgetsnbextension` code taken from [official blog](https://pandas-profiling.github.io/pandas-profiling/docs/master/rtd/pages/introduction.html)



Note,
1. special thanks to [Nicole Janeway Bills](https://medium.com/@nicolejaneway) for her [blog](https://towardsdatascience.com/10-underrated-python-skills-dfdff5741fdf).
2. Read more details at this [link](https://pandas-profiling.github.io/pandas-profiling/docs/master/rtd/pages/introduction.html)
