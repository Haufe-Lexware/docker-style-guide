# Docker Basics

Learning the docker basics means getting up to speed on the Haufe Group Docker tooling and the accepted docker repositories. More advanced stuff - like composing multiple docker processes into coordinated services or building docker processes and services as part of CI/CD comes later.

The Haufe Group Docker Style Guide has an section on which [Docker tools are accepted](/HaufeDockerToolset.md). And, There is also a style guide section for [accepted Docker repositories](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/Dockerfile.md#use-only-well-maintained-images-from-a-trusted-registry) - where predefined images can be searched, stored and reused.

We have already linked to docker concepts so hopefully, you've already read up on them. You should have already installed and tested docker, so now, it's time to get started.

## A work flow proposal to capture the basics

There are lots of ways to learn Docker but one way of doing it is to follow these steps:

* Learn Docker Hub - Learn what's out there so you can avoid doing extra work
* Learn the Docker Engine Client and Client commands - You'll need this at build time too!
* Learn to build images with the Dockerfile - define and document Docker images with on artifact
* Learn about the docker-machine - the tool that manages Docker host machines and Docker swarms

In this section you are going to create a base image, use Dockerfile to create images, and learn how to create new hosts and manage these hosts.

Never forget: You can always learn more. But to get started, it's probably best to review [how docker images and containers work](https://docs.docker.com/engine/getstarted/step_two/). Also before your get started, pls read:

* [Haufe Docker Style Guide - Docker Images](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/DockerImage.md)
* [Haufe Docker Style Guide - Docker Containers](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/DockerContainer.md)
* [Haufe Docker Style Guide - Container Best Practices](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/BestPracticesContainer.md)

## Searching Registries

When you begin with docker you should have a good idea what you want to do. This is where Docker's composability can help, and chances are, that there is already an image at the Docker Hub or in the Haufe Docker Hub, that already meets your needs. So let’s say you want to create a Web application. Then you probably need some kind of Web Server.

There are several ways to look for images but the best way to find what’s out there is to go to [https://hub.docker.com/](https://hub.docker.com/) and search for what you need to build your application. You will also want to create a docker hub account – here you can store your personal images. Try this:

Go to Docker Hub and type in "httpd" in the search field. You should get a very long SERP of dockerized Apache Web Server images. If search for other well known applications and frameworks like node JS, MongoDB, FluentD, Ubuntu, and many others - you will find that all of this software has been dockerized into docker images and that, just like the software, these docker images are open source.

You can also search for images from the command line by using the “[docker search](https://docs.docker.com/engine/reference/commandline/search/)” command. But, the documentation at docker hub is in my opinion, more human-readable: i.e. if you don’t know exactly what you want, you’ll be able to research better and figure out if you need it or not on Docker hub.

Browse for software that interests you.

By seeing what's already on docker hub, you can get a feeling for how wide-spread docker has become and how much easier it is with docker to compose portable applications that take up very few resources.

**Achtung** There is a new docker registry call the [Docker Store](https://store.docker.com/), which looks like it is slowly replacing the Docker Hub.

Once you are done exploring what's there, you want to create your own docker hub account this is your docker sandbox for customized images. Once you have configured your image locally, you can push it up to Docker hub to make it publicly available.

### Haufe Group Docker registry

her

In addition to docker hub, Docker enables you to push images to the Haufe registry and even create your own private registry.

Now that you are done with section you should be able to -

* Search the Docker Hub for interesting images
* Have your own Docker Hub account
* Search through the Haufe Group Docker registry

## Creating a base image

The way docker works is that you create images and you create running instances of these images by running them or by building them: running instances are containers. In general, there are two ways to create images.

* Use the "run" or "pull" command to create a base image
* Use a Dockerfile and the "build" command to create your own images

Both ways are important. You must understand the CLI commands - these will later be automated by the build agent - and because you must to use the Dockerfile to persist your image and automate building it later.

If you have docker installed, you can create a base image by opening a console and typing in:  
`docker pull ubuntu` if you don't have an ubuntu image on your Docker automatically searches the the Docker Hub for the latest available image.

Since we are just getting started this is ok. If you are working on a project where the application is only supported by ubuntu version 14.04 then you would pull that ubuntu image by specifying the either the version or the release name in the tag - `docker pull ubuntu:trusty`

The tag, what comes after the ":", contains the metainformation about the image. If there is no tag, Docker assumes that you want the latest image and pulls this.

Now, type in `docker images`

You should get a table of images. One of the columns in the table is "tag"

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

### Dockerfile

Once you get up to speed with the CLI you should also get know the Dockerfile. One Dockerfile defines one Docker image that will be loaded into your container at run or build time. Don't forget, in the Docker style guide there are both [Dockerfile requirements](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/Dockerfile.md) and [some Dockerfile practices](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/BestPracticesDockerfile.md) that you must follow - you might as well do it from the beginning.

Docker Docs also has a [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/) that contains all of the Dockerfile instructions.

Important to know about Dockerfiles is that you can not only build an image in a Dockerfile you can also do things like set environment variables and specify commands to run from the the bash console of the containers of this image.

**Achtung:** There are two types of command directives in a Dockerfile and, in the Haufe docker landscape, it is important for you to understand hwo to use them. They are:

* ENTRYPOINT
* CMD

**ENTRYPOINT**

Shall be used to start any executables within a container. For example, if your container uses MongoDB as a database, you must start the MongoDB with ENTRYPOINT in your dockerfile: otherwise MongoDB will not be available.

**CMD**

Shall be used to run commands within the container that are likely to change.

### Whalesay tutorial

The [Docker Whalesay tutorial](https://docs.docker.com/engine/getstarted/step_three/) is a good basic tutorial to understand how to build images with both the CLI and [to build your own image using Dockerfile](https://docs.docker.com/engine/getstarted/step_four/). Go ahead and do this tutorial. While you are doing this one, also note that at this stage you will always need to run an image to create a Docker container that actually does something.

### More Tutorials

There are also many more tutorials that show you how to dockerize applications but also how to do more stuff with docker. These tuts are basically to develop your docker skills, but with a little work you may be able to reuse the these images for your own purposes. Here is a list:

| Tut | Docker Skill |
| --- | --- |
| [MongoDB](https://docs.docker.com/engine/examples/mongodb/) | Learn how to dockerize MongoDB, push your image to your DockerHub account and share |
| [PostgreSQL](https://docs.docker.com/engine/examples/postgresql_service/) | Learn how dockerize PostgreSQL, learn how to use container volumes |
| [SSH service](https://docs.docker.com/engine/examples/running_ssh_service/) | Learn how to set environment variables in Dockerfile \(and propagate further\), review removing containers and images |

### Section targets

* Know how to find what your are looking for in Docker Regsitries \(Docker Hub and Haufe Group Docker Registry\)
* Get to know the Docker Engine CLI and how to use CLI commands to search for and pull, tag and push base images 
* Get to know how to run and manage containers with the docker CLI
* Understand Dockerfile - Instructions like VOLUME, WORKDIR, ADD, COPY
* Know Haufe Group Requirements
* Build your own images with Dockerfile. 
* Understand how to develop locally and add these changes to your Docker image by building Dockerfile

## Docker Machine

The final piece of tooling in the basics section is the Docker Machine. According to Docker, Docker Machine used to perform the following tasks.

> * Install and run Docker on Mac or Windows
> * Provision and manage multiple remote Docker hosts
> * Provision Swarm clusters

We will mostly take a look at creating and managing hosts in this section. Remember a Docker Host is a Linus virtual machine that contains a Docker Daemon. In production, it is important to be able to create and manage hosts for many reasons. One of the reasons is data security. For example, the Haufe Docker Guide states that

> For each customer that uses a dockerized application, you must create a separate host machine.

With docker machine, you can create as many hosts as you like. You manage hosts with the Docker-Machine CLI. Also, up to now you should have been able to do all of the docker exercises, because docker installs a "default" host machine at installation. This is great for testing dockerized applications, but for development, you will create many Docker Hosts - both for different customers and for different applications. And so, it's going to be important to know what's on all of these hosts so you can be sure that your working on the right VM!

One of the nice things about working with Docker for Windows / Mac is that Docker Machine is installed along with the other tools by the installer. If you have Linux you must [install Docker Machine separately](https://docs.docker.com/machine/install-machine/).

The Haufe Style Guide has a [Docker-Machine entry](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/DockerMachine.md), but you don't have to worry about this right now.

Again, Docker has fantastic documentation on all of it's tooling and the [Docker-Machine documentation](https://docs.docker.com/machine/get-started/) is no exception: So it's a good idea to work through this getting started tutorial. Since you are just getting started, you can stay local and skip the "provisioning a host" in the cloud part if you like.

**Achtung:** Be sure to name your Docker Host Machines extremely well: While there is no official naming convention a transparent naming system with **Application, Customer** and other relevant information is important so you know what's running on your host machines.

### Section targets

When you are done with this section, you should be able to:

* Create a new Docker Host 
* Use many Docker-Machine commands
* Discover important information about your host \(inspect, port, ip\)
* Select and switch hosts that contain different images



