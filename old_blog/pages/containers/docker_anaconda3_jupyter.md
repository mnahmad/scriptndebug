---
layout: page
title: Using Continuumio Docker image for python anaconda3
tagline: docker python anaconda3
description: Using Continuumio Docker image for python anaconda3
---

<a href="https://twitter.com/intent/tweet?text=Using%20Continuumio%20Docker%20image%20for%20python%20anaconda3%20https://mnahmad.github.io/scriptndebug/pages/containers/docker_anaconda3_jupyter.md%20@mnabiahmad"><img src="https://mnahmad.github.io/scriptndebug/twiter-icon-15.jpg" height="25" width="25"></a>

*Last update: 01/06/2019*

Few months back I decided to try python anaconda for some of my data science tasks but wanted to isntall in a VM (so my other python pasths are not disturbed). On of the best solution was to use anaconda docker image that not only have anaconda but jupyter notebookas well so
- Every thing comes preinstalled
- I can access IDE as a web service (this is where jupyter comes in)

I started looking for images and came accross [ContinuumIO](https://github.com/ContinuumIO/docker-images/tree/master/anaconda3) image. It has every thing I needs this I downlaoded it and following is the usage story.

Note, at the time I was using this image, I was new to docker thus you will see lots of basic stuff and explanation.  

Lets start the container

```
docker run -i -t -p 8888:8888 continuumio/anaconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser --allow-root"
```

some details about the above command


--entrypoint entry point tells docker which executable to run when the container starts, when used with -c it means the container will run the next command(s) like `/bin/bash -c "/opt/conda/bin/conda install jupyter && "` where && is pipe to add more commands

Note, good to add quotation but not needed like `docker run -it --entrypoint  /bin/bash  scioquiver/notebooks -c ls -l`. One can move the image name to before `/bin/bash` as well `docker run -it scioquiver/notebooks  /bin/bash -c ls -l`


-e set environment variable like `-e "abc=xyz"` or

```
export today=Wednesday
docker run -e "deep=purple" -e today --rm alpine env
```


__Now__, to explain docker run command, I took an example from one of the docker images I work on. The continuumio/anaconda3 is a data science notebook I use for some of my data processing etc., following is command to start it

```
docker run -i -t -p 8888:8888 continuumio/anaconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser --allow-root"

```  

Following is break down of the above command

| command/option/ | explanation   |
| :------------- | :------------- |
| docker run    | command to run the image|
|  -i           | the session will be interactive |
| -t            | tty          |
| -p 8888:8888  | map host port to container port |
| continuumio/anaconda3 | image name |
| /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser --allow-root"   |  -c tells the container to (a) use the bash as cli tool, (B) use conda command as first command from /opt/conda/bin/conda and install jypyter notebook software, (c) create a folder in /opt/notebaook and finally (d) run command jupyter notebook from /opt/conda/bin/. While starting notebook , set the default folder for all notebooks to be /opt/notebooks , listen on all IPs, port for jupyter is 8888 , do not opne web browser and allow root user to access it.  


Now that container is running, lets see which other containers are running

```
docker ps
```

One can also use `docker ps -a` to see which images were executed in the past.


If you want CLI access to docker container (specific one), use the following commands.

```
docker exec -it docker_id /bin/bash


-i --interactive: Take user to container CLI
-t -- tty

-d detach: run in detach mode

```

the docker_ID will come form the ps command

With the above `docer run command` jupyter notebook is installed (every time you this command the jupyter notebook will be installed) and a folder is created at /opt/notebooks, thus, all your notebooks will be stored inside this folder.

I felt it was a good idea to safe all my notebooks outside the container thus, I used a `-v` for volumne option. So now when I will starte the container, all my notebooks (and changes) will be saved in a folder outside the container.

```
docker run -v /host/directory:/container/directory -other -options image_name command_to_run
```

like

```
docker run -v /Users/<my-user>/mynotebooks:/opt/notebooks/mynotebooks -i -t -p 8888:8888 continuumio/anaconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser --allow-root"

```

It is much better option to load your code, work on it and then save it (and it will be saved on host).


Once done, docker cotainer can be stoped by using the following command.
```
docker stop docker_container_id
```

## Installations inside container
From time to time, I test different libraries inside this container. This section covers the installation steps, issues and their solution and basic working of libraries.

### pandas profiling

Installation and activation:

1. `docker ps` to get container id
2. `docker exec -it docker_id /bin/bash` to start shell session
3. `pip install -U pandas-profiling[notebook]` code taken from [official blog](https://pandas-profiling.github.io/pandas-profiling/docs/master/rtd/pages/introduction.html)
4. `jupyter nbextension enable --py widgetsnbextension` code taken from [official blog](https://pandas-profiling.github.io/pandas-profiling/docs/master/rtd/pages/introduction.html)



Note:
1. special thanks to [Nicole Janeway Bills](https://medium.com/@nicolejaneway) for her [blog](https://towardsdatascience.com/10-underrated-python-skills-dfdff5741fdf).
2. Read more details at this [link](https://pandas-profiling.github.io/pandas-profiling/docs/master/rtd/pages/introduction.html)


In futuer, I will try to use the container to play around with iris data available at [this](https://towardsdatascience.com/knn-using-scikit-learn-c6bed765be75) link.
