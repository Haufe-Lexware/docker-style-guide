# Composing applications with Docker Compose

Composing is exactly what you do with Docker compose. While it's possible to create an application from a single docker image, when you think about docker's purpose - to serve as a packaging system for our software applications and also how docker "packages" these applications - creating a full-blown application on one big image requires more work than creating many small images and configuring them to work together when Docker is involved. Single big images defeat the purpose of Docker. [Docker Compose Overview](https://docs.docker.com/compose/overview/)    states that:

> Compose enables you to configure and run multi-container applications.

Like Dockerfile, Docker Compose file serves as configuration and documentation. With Docker Compose though, you are configuring multi-container applications. Unlike images built with Dockerfile, where you build and then run, you can run and manage applications packaged with Docker-Compose directly, using the Docker Compose CLI. Once you start using Compose, you can \(mostly\) say bye-bye to the `docker run` command. Maybe the best definition of a Docker Compose file by Docker is:

> The Compose file is a YAML file defining services, networks and volumes. The default path for a Compose file is ./docker-compose.yml.

## Compose Instruction Reference

**Editor's Note**: Here we wish to add some compose keywords to reinforce which commands are useful. Especially since v3 is out now.

Some of the Docker Compose instructions that help to configure multi-container applications are listed below. For documentation that list all Docker Compose instructions, [go to Docker Compose file reference](https://docs.docker.com/compose/compose-file/).

| Instruction | Function |
| :--- | :--- |
| FROM | Defines the base image you shall use for your Docker image. |
| COPY/ADD | Adds files from a specific location to your image. |
| RUN | Runs commands on top of your image, creating a new image layer on top of the existing image |
| WORKDIR | Specifies the start directory in your image |
| ENV | Sets environment variable in your image |
| ENTRYPOINT | see above |
| ports | Exposes ports for a Docker service and performs port mapping between Docker Host and the container service. |
| depends\_on | Assigns service dependencies to service definitions in a Compose file. with `depends\_on` you also configure, which containers are started first at `docker-compose up` time. |
| volumes | Mounts paths or named volumes. For v3 compose files volumes replaces volumes\_from for mounting data containers. |

## Extending your composed application

Docker Compose provides you with an easy way to isolate different application environments from one another. Highly convenient is that you also can extend your Compose configuration with additional files to:

* Use variables within your files - [.env files](https://docs.docker.com/compose/env-file/) and [add variables into your Compose file](https://docs.docker.com/compose/environment-variables/)
* [Create different service configurations](https://docs.docker.com/compose/extends/) e.g CI, Test, Production - .override files

This can be helpful if you want to test different Compose environments.

## Docker Compose practices

Haufe Group Docker Style Guide has practices for working with Docker Compose and creating Docker Compose files:

* [Docker Compose](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/DockerCompose.md)
* [Docker Compose Best Practices](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/BestPracticesCompose.md)

Once you have read through these, get started by going through Docker's [Docker Compose documentation](https://docs.docker.com/compose/overview/), starting with the overview and working through the entire Compose section. You can leave out the experimental and "superseded" sections.

## Docker Compose practice

The best way to understand Compose is to practice. The getting started section and  tutorials in this documentation can help. Direct links to these are:

| Tut | Docker Skill |
| --- | --- |
| [Getting started](https://docs.docker.com/compose/gettingstarted/) | Learn how to to compose a basic Python app, using two services, learn compose file instructions |
| [Django](https://docs.docker.com/compose/django/) | Learn set up a Django / Postgre app, learn how to further define services - build, volumes, ports, depends\_on |
| [Wordpress](https://docs.docker.com/compose/wordpress/) | Learn how to set up a Wordpress service with MySQL and a data volume service, learn how to set environment variables from Compose file, learn the restart instruction |

To get a really good basic knowledge, add these tasks when you work the tutorials:

* Extend the configuration of each Compose file and create multiple environments with .env and .override files.
* Apply Haufe Group practices to all Compose Files. **Hint:** No secrets, data containers and so on. 
* Finally, if you didn't already read it, you should read [Compose in Production ](https://docs.docker.com/compose/production/) to understand what you must change to make your compose application production-ready.

## Section Targets

* Understand the concept behind Docker Compose and how it should be used in Haufe Group
* Create several composed applications by working the docker tutorial
* Know how to use many DC CLI commmands
* Compose your own application from docker-compose.yml
* Compose an application using variables - values in an .env file
* Compose different service environments by using the extended override configuration
* Know how to make a docker-compose.yml file Haufe Group compliant 



