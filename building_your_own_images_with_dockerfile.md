## Dockerfile

Once you get up to speed with the CLI you should also get to know the Dockerfile. One Dockerfile defines one Docker image that will be loaded into your container at run time. Don't forget, in the Docker style guide there are both [Dockerfile requirements](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/Dockerfile.md) and [some Dockerfile practices](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/BestPracticesDockerfile.md) that you must follow - you might as well do it from the beginning. Actually there are quite a few published practices for writing Dockerfiles:

* [Docker's Dockerfile practices](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)
* [Resion.io Dockerfile practices for 2016](https://resin.io/blog/our-dockerfile-tips-tricks/)

Important to know about Dockerfiles is that, you can not only build an image in a Dockerfile, you can also do things like set environment variables and specify commands to run from the the bash console of running containers. Each new instruction in the Dockerfile creates a layer - which is a little like a code check in for a versioning system and is explained [here](https://docs.docker.com/engine/understanding-docker/#how-does-a-docker-image-work). This is one of the ways that Docker can stay efficient. To keep Docker images lean and mean, it is recommended that you concatenate your instructions or insert them into a shell script and run the script from Dockerfile. This reduces the number of layers created by your Docker images.

**Achtung:** There are two types of command directives in a Dockerfile and, in the Haufe docker landscape, it is important for you to understand how to use them. They are:

* ENTRYPOINT
* CMD

**ENTRYPOINT**

Shall be used to start any executables within a container. For example, if your container uses MongoDB as a database, you must start the MongoDB with ENTRYPOINT in your dockerfile: otherwise MongoDB will not be available.

**CMD**

Shall be used to run commands within the container that are likely to change. You can find the [Docker practice](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/BestPracticesDockerfile.md#entrypoint-vs-cmd) for this in our style guide.

### Dockerfile instructions

Docker Docs also has a [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/) that contains all of the Dockerfile instructions. It makes sense to get acquainted with the following basic instructions:

| Instruction | Function |
| :--- | :--- |
| FROM | Defines the base image you shall use for your Docker image. |
| COPY/ADD | Adds files from a specific location to your image. |
| RUN | Runs commands on top of your image, creating a new image layer on top of the existing image |
| WORKDIR | Specifies the start directory in your image |
| ENV | Sets environment variable in your image |
| ENTRYPOINT | see above |
| CMD | see above |
| USER | After image construction is finished you must switch user. It is required that containers default user is NOT "root". |
| LABEL | Data label your image to provide helpful additional information about it. |

Just like with Docker CLI commands there are many more Dockerfile instructions in the [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/) that will prove useful.

**Achtung:**  Data labeling your images with metadata is very important for image discovery and description purposes, and also to organize docker images in the Haufe Group Docker Registry. In my short research, it looks the only way to easily add labels** to an image** is to use the LABEL instruction in your Dockerfile. You may want to make use of [this proposed labeling schema](http://label-schema.org/rc1) to provide  good, semantic data labeling to your images and containers.

### Whalesay tutorial

The [Docker Whalesay tutorial](https://docs.docker.com/engine/getstarted/step_three/) is a good basic tutorial to understand how to create images with the CLI and [to build your own image using Dockerfile](https://docs.docker.com/engine/getstarted/step_four/). Go ahead and do this tutorial. While you are doing this one, also note that at this stage you will always need to run an image to create a Docker container that actually does something.

**Achtung:** On Windows \(With Docker for Windows\), I have also encountered some problems at create image time when extending base images by using package managers like “apt” on Linux from a Dockerfile. The workaround for this was to add build arguments that set the proxy server with the Docker Builder. These are environment variables that are only set at image build time. In Docker you can do this two ways.

* Use the [-–build-arg option](http://docs-stage.docker.com/v1.10/engine/reference/commandline/build/#set-build-time-variables-build-arg) with the “docker build” command  
* Use the ARG instruction in a Dockerfile  
  These arguments are only passed to the builder and do not persist in image or running container.

### More tutorials

There are also many more tutorials that show you how to dockerize applications and also how to perform tasks with Docker and Dockerfile. These tuts are basically to develop your Docker skills, but with a little work you may be able to reuse the these images for your own purposes. Here is a list:

| Tut | Docker Skill |
| --- | --- |
| [MongoDB](https://docs.docker.com/engine/examples/mongodb/) | Learn how to dockerize MongoDB, push your image to your DockerHub account and share |
| [PostgreSQL](https://docs.docker.com/engine/examples/postgresql_service/) | Learn how to dockerize PostgreSQL, learn how to use                container volumes |
| [SSH service](https://docs.docker.com/engine/examples/running_ssh_service/) | Learn how to set environment variables in Dockerfile \(and    propagate further\), review removing containers and images |

### Dockerfile cheat sheet

Some more good tips on what you can do with [Dockerfiles are here](http://docker.jens-piegsa.com/#dockerfile)

### Section targets

* Understand Dockerfile - Instructions like VOLUME, WORKDIR, ADD, COPY, and LABEL
* Know Haufe Group practices for Dockerfile
* Build your own images with Dockerfile. 
* Understand how to develop locally and add these changes to your Docker image by building a Dockerfile
