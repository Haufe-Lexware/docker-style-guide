## Creating a base image

The way docker works is that you create images and you create running instances of these images by running them or by building them: running instances are containers. In general, there are two ways to create images.

* Use the "run" or "pull" command to create a base image
* Use a Dockerfile and the "build" command to create your own images

Both ways are important. You must understand the CLI commands - these will later be automated by the build agent - and because you must to use the Dockerfile to persist your image and automate building it later.

If you have docker installed, you can create a base image by opening a console and typing in:  
`docker pull ubuntu` if you don't have an ubuntu image on your system, Docker automatically searches the the Docker Hub for the latest available image.

**Achtung:** Since you are just getting started this is ok. If you are working on a project where the application is only supported by ubuntu version 14.04 then you would pull that ubuntu image by specifying the either the version or the release name in the tag - `docker pull ubuntu:trusty`

The tag, that comes after the ":", contains the metainformation about the image. If there is no tag, Docker assumes that you want the latest image and pulls this.

Now, type in `docker images`

You should get a table of images. One of the columns in the table is "tag". If you pulled ubuntu: trusty, you will see trusty in the "tag" column.

### CLI Commands

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

### Section targets

* Get to know the Docker Engine CLI and how to use CLI commands to search for, pull, manage and push Docker images 
* Get to know how to run and manage containers with the docker CLI

