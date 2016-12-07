# Docker Basics
Learning the docker basics means getting up to speed on the Haufe Group docker tooling and the accepted docker repositories. More advanced stuff - like composing multiple docker processes into coordinated services or building docker processes and services as part of CI/CD comes later. 

The Haufe Group Docker Style Guide has an section on which [Docker tools are accepted](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/HaufeDockerToolset.md). And, There is also a style guide section for [accepted Docker repositories]( https://github.com/Haufe-Lexware/docker-style-guide/blob/master/Dockerfile.md#use-only-well-maintained-images-from-a-trusted-registry) - where predefined images can be searched, stored and reused.

We have already linked to docker concepts so hopefully, you've already read up on them. You should have already installed and tested docker, so now, it's time to get started.

## A work flow proposal to capture the basics
There are lots of ways to learn Docker but one way of doing it is to follow these steps:
* Learn Docker Hub - Learn what's out there so you can avoid doing extra work
* Learn the Docker Engine Client and Client commands - You'll need this at build time too!
* Learn to build images with the Dockerfile - define and document Docker images with on artifact
* Learn about the docker-machine - the tool that manages Docker host machines and Docker swarms

In this section you are going to create a base image, use Dockerfile to create images, and learn how to create new hosts and manage these hosts. 

Never forget: You can always learn more more. But to get started, it's probably best to review [how docker images and containers work](https://docs.docker.com/engine/getstarted/step_two/). 

## Searching Registries
When you begin with docker you should have a good idea what you want to do. This is where Docker's composability can help, and chances are, that there is already an image at the Docker Hub or in the Haufe Docker Hub, that already meets your needs. So let’s say you want to create a Web application. Then you probably need some kind of Web Server. 

There are several ways to look for images but the best way to find what’s out there is to go to [https://hub.docker.com/](https://hub.docker.com/) and search for what you need to build your application. You will also want to create a docker hub account – here you can store your personal images. Try this: 

Go to Docker Hub and type in "httpd" in the search field. You should get a very long SERP of dockerized Apache Web Server images. If search for other well known applications and frameworks like node JS, MongoDB, FluentD, Ubuntu, and many others - you will find that all of this software has been dockerized into docker images and that, just like the software, these docker images are open source. 

You can also search for images from the command line by using the “[docker search](https://docs.docker.com/engine/reference/commandline/search/)” command. But, the documentation at docker hub is in my opinion, more human-readable: i.e. if you don’t know exactly what you want, you’ll be able to research better and figure out if you need it or not on Docker hub. 

Browse for software that interests you.

By seeing what's already on docker hub, you can get a feeling for how wide-spread docker has become and how much easier it is with docker to compose portable applications that take up very few resources. 

**Achtung** There is a new docker registry call the [Docker Store](https://store.docker.com/), which looks like it is slowly replacing the Docker Hub. 

## Creating a base image

The way docker works is that you create images and you create running instances of these images by running them or by building them: running instances are containers. In general, there are two ways to create images. 
* Use the command line interface
* Use a Dockerfile

Both ways are important because you must understand the CLI commands and because you must to use the Dockerfile to persist your image and automate building it later. 

### CLI Commands
You should get to know the following commands. The best documentation is the [Docker Command Line Reference](https://docs.docker.com/engine/reference/commandline/) and the [Docker Run Reference](https://docs.docker.com/engine/reference/run/), so this is just a list of some of the commands. 

* Build 
* Images
* Inspect
* Logs
* Pull
* PS
* Rmi
* Rm
* **Run** 
* Search

There are many more commands - like "Network" - that may be useful to you as you develop with docker. 

### Building your own image with Dockerfile
Once you get used to the CLI you should also get know the Dockerfile. One Dockerfile defines one Docker image that will be loaded into your container at run or build time. Don't forget, in the Docker style guide there are [some Dockerfile practices](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/BestPracticesDockerfile.md) that you must follow - you might as well do it from the beginning. 

Docker Docs also has a [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/) that contains all of the information about Dockerfiles

Important to know about Dockerfiles is that you can not only build an image in a Dockerfile you can also do things like set environment variables and specify commands to run from the the bash console of the containers of this image. There are two types of command directives in a Dockerfile:
* Entrypoint
* CMD

**ENTRYPOINT** shall be used to start any executables within a container. For example, if your container uses MongoDB as a database, you must start the MongoDB with ENTRYPOINT in your dockerfile: otherwise MongoDB will not be available.

**CMD** shall be used to run commands within the container that are likely to change.

### Whalesay tutorial
The [Docker Whalesay tutorial](https://docs.docker.com/engine/getstarted/step_three/) is a good basic tutorial to understand how to build images with both the CLI and [to build an image using Dockerfile](https://docs.docker.com/engine/getstarted/step_four/). Go ahead and do this tutorial. While you are doing this one, also note that at this stage you will always need to run an image to create a Docker container that actually does something.

### More Tutorials




To get up to speed go ahead work through the Docker documentation, starting with the [Docker docs welcome page](Docker docs welcome page).