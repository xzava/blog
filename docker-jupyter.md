> Last updated: Nov 1 2020

## Setting up Docker jupyter

Why use docker? Using docker as the main form allows the env to become a cloud env and use cloud resources rather than limited local resources.

Thinks I don't like about jupyter is light mode, I have installed dark mode aswell but it messed with graphs and rendering html. Update this information when I find the best solution.

The way I'm using jupyter is using the ~/notebook dir and everything jupyter related goes in here. If not keeping everything organised, then to keep jupyter system access limited. I don't like a browser bring able to read/ write files. I turn this off, browsers should not have this type of access unless they ask each time for permission.


### CURRENT VERSION

docker pull jupyter/datascience-notebook

(lastest version is using python 3.8)
(note /home/pc )

docker run -p 8888:8888 -v /home/pc/notebook:/home/jovyan/work --name notebook jupyter/datascience-notebook 

(Open the provided link)
http://127.0.0.1:8888/?token=d4gbfd446773gbfd4467735et77664

(Check docker status)
docker ps -a
docker images
docker image list -a

(test to see what the python version of this notebook is)

(install pytorch inside notebook container)
python -m pip install torch==1.7.0+cpu torchvision==0.8.1+cpu torchaudio==0.7.0 -f https://download.pytorch.org/whl/torch_stable.html

docker stop notebook
docker start notebook

docker ps -a



### Docker jupyter Quick Start
https://jupyter-docker-stacks.readthedocs.io/en/latest/index.html

### Docker jupyter images
Here are a list of jupyter docker images
https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html

I want to use the lastest python version.

- jupyter/tensorflow-notebook
- jupyter/datascience-notebook 


#### Loose commands for reference
docker pull jupyter/datascience-notebook
docker pull python:3.9.0-alpine3.12

docker pull jupyter/datascience-notebook:python-3.8.6

## DATASCIENCE NOTEBOOK
### Simple version no volumes.
docker run -p 8888:8888 jupyter/datascience-notebook

### Adds the current working dir as a volume.
docker run -p 8888:8888 -v "$PWD":/home/jovyan/work jupyter/datascience-notebook

### Enables Jupyter lab and sets current working dir as a volume.
docker run -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes -v "$PWD":/home/jovyan/work jupyter/datascience-notebook

### Auto Deletes container when finished.
docker run --rm -p 8888:8888 jupyter/datascience-notebook


# TENSORFLOW NOTEBOOK
docker run -p 8888:8888 jupyter/jupyter/tensorflow-notebook

docker run --rm -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes -v "$PWD":/home/jovyan/work jupyter/datascience-notebook

docker run --rm -p 8888:8888 -e JUPYTER_ENABLE_LAB=yes -v "$PWD":/home/jovyan/work jupyter/tensorflow-notebook

http://127.0.0.1:8888/?token=a98c8e4405253f01ecd352ec3c8e549

## Next you will be given a url similar to this

http://127.0.0.1:8888/?token=a98c8e4405253f01ecd352ec3c8e549


docker pull pytorch/pytorch:latest

### Note: 
1. Allow cookies
2. If their is a problem it might be the browser.


1. I had this error on Chrome 'Couldn't authenticate WebSocket connection' but it worked fine on firefox.

2. You will need to allow cookies on this port, because their is a cookie needed to enter the password, or token.




You might ask where is everything being saved?

At a high level its being saved inside the container

while this container is running open a new terminal

type

docker ps

These are the running containers, you should only have one in this example. Note the CONTAINER ID

docker exec -it <CONTAINER_ID> bash
docker exec -it <CONTAINER_ID> /bin/bash
docker exec -it <CONTAINER_ID> sh

replace <CONTAINER_ID> with the container ID of the container you would like to enter with a open terminal.

You will see your name has changed

mike@mike: ~$
jovyan@8a0fdfba2e18:~$

You are inside the container

~~~
jovyan@8a0fdfba2e18:~$ ls
work
~~~
everything is saved into the work folder

~~~
cd work
ls
~~~

Its probably empty. 


Try create a file in your jupyter notebook, or a folder or both.

> ls

You should see a new file or folder has been added. 

> things to add, where is this file actually stored on the disc.
> does the container have access to any or my other files
> is it safe to run javascript in the container if the container has access to my file system


https://phase2.github.io/devtools/common-tasks/ssh-into-a-container/

> docker exec -it <container name> /bin/bash

This only works if the container is already running
ie listed when you type "docker ps"


### While still in the container terminal

You can run pip freeze to see all of the python modules installed on the container

pip freeze




## Other:
- https://jakevdp.github.io/blog/2017/12/05/installing-python-packages-from-jupyter/



python -m pip install pytorch
conda install pytorch torchvision cudatoolkit=10.0 -c pytorch





# Misc docker commands


docker exec -it <container name> /bin/bash
docker-compose run <container name>
docker-compose run web /bin/bash

### Note: You cant ssh into a docker conatiner if its running a flask webapp on startup.

# Starts a new instance of a image
docker run -it <image name> <command>

# Show logs of active conatiner
docker logs [OPTIONS] CONTAINER
