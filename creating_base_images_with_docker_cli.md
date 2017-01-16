## Creating a base image

The way docker works is that you create images and you create running instances of these images by running them or by building them: running instances are containers. In general, there are two ways to create images.

* Use the "run" or "pull" command to create a base image
* Use a Dockerfile and the "build" command to create your own images

Both ways are important. You must understand the CLI commands - these will later be automated by the build agent - and because you must to use the Dockerfile to persist your image and automate building it later.

You may want to review the Docker practices for [Images](/DockerImage.md) and [Containers](/DockerContainer.md) again before your start working with the CLI.

### Create an image with the CLI

The CLI is the command line interface part of Docker Engine.

If you have docker installed, you can create a base image by opening a console and typing in:  
`docker pull ubuntu` if you don't have an Ubuntu image on your system, Docker automatically searches the the Docker Hub for the latest available image.

**Achtung:** Since you are just getting started this is ok. If you are working on a project where the application is only supported by ubuntu version 14.04 then you would pull that ubuntu image by specifying either the version or the release name in the tag - `docker pull ubuntu:trusty`

The tag, that comes after the ":", contains the metainformation about the image. If there is no tag, Docker assumes that you want the latest image and pulls this.

Now, type in `docker images`

You should get a table of images. One of the columns in the table is "tag". If you pulled ubuntu: trusty, you will see trusty in the "tag" column.

### CLI commands

You should get to know the following commands. The best documentation is the [Docker Command Line Reference](https://docs.docker.com/engine/reference/commandline/) and the [Docker Run Reference](https://docs.docker.com/engine/reference/run/), so this is just a list of some of the commands are important.

| Command | Function |
| --- | --- |
| build | build an image from Dockerfile |
| images | View images and high-level information |
| inspect | Return low-level image or container information |
| logs | View container logs in stdout |
| pull | Pull an image from Docker Hub or another registry |
| ps | View containers and high-level information |
| rm | Remove containers |
| rmi | Remove images |
| run | Run a container from image |
| search | Search a registry for a particular image |

There are many more commands - like "[docker network](https://docs.docker.com/engine/userguide/networking/)" - that may be useful to you as you develop with docker.

## CLI tutorials

Getting some practice with the CLI is good and here are some tutorials that step you through from basic commands to ssh-ing into the container itself to update software "in-container".

| Tut | Docker Skill |
| :--- | :--- |
| [Romirani Part 2 Basic commands](https://rominirani.com/docker-tutorial-series-part-2-basic-commands-baaf70807fd3#.4et5fzv52) | Learn some basic commands including "search" and "run" |
| [Romirani Part 3 Manage images and containers](https://rominirani.com/docker-tutorial-series-part-3-more-on-images-and-containers-68ce7a026fc1#.81u5vtrpt) | Learn more commands to manage images and containers + expose an Apache Web Server by mapping ports. |
| [Romirani Part 5 Build your own image](https://rominirani.com/docker-tutorial-series-part-5-building-your-own-docker-images-b4a448b44afc#.1mip1x4as) | Build your own image learn how to ssh into your container with the CLI to work inside of it. |
| [Romirani Part 7 Data volumes](https://rominirani.com/docker-tutorial-series-part-7-data-volumes-93073a1b5b72#.mgwgl2c5b) | Learn how to use data volumes from the CLI. |

That should be enough to get started.

**Achtung:** These tutorials were made for the Docker Toolset, which is an older version of Docker for Windows. Still, you should be able to work through the tutorial. Just ignore the part about Boot2Docker. Also, for "Part 5", in the real Docker world, you do not want to work directly inside the container, you will want to configure these commands as instructions in your Dockerfile. More on that in the next section.

### Section targets

* Get to know the Docker Engine CLI and how to use CLI commands to search for, pull, manage and push Docker images 
* Get to know how to run and manage containers with the docker CLI
* Know the Haufe practices for images and containers



