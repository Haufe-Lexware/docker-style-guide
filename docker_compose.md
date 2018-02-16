# Composing applications with Docker Compose

Composing is exactly what you do with Docker compose. While it's possible to create an application from a single docker image, when you think about docker's purpose - to serve as a packaging system for our software applications and also how docker "packages" these applications - creating a full-blown application on one big image requires more work than creating many small images and configuring them to work together - when Docker is involved. Single big images defeat the purpose of Docker. [Docker Compose Overview](https://docs.docker.com/compose/overview/)    states that:

> Compose enables you to configure and run multi-container applications.

Like Dockerfile, Docker Compose file serves as configuration and documentation. With Docker Compose though, you are configuring multi-container applications. Unlike images built with Dockerfile, where you build and then run, you can run and manage applications packaged with Docker-Compose directly, using the Docker Compose CLI. Once you start using Compose, you can \(mostly\) say bye-bye to the `docker run` command. Maybe the best definition of a Docker Compose file by Docker is:

> The Compose file is a YAML file defining services, networks and volumes. The default path for a Compose file is ./docker-compose.yml.

## Compose File Instruction Reference

**Achtung:** The compose file defines services, and services are normally implemented with / within 1 docker container. For the this section the word "service" refers to both: a Docker service is exposed by a Docker container. Additionally, you may want to test. _ToDo check this statement to see if it is still correct - If not then remove_

Some of the Docker Compose instructions that help to configure multi-container applications are listed below. For documentation that list all Docker Compose instructions, [go to Docker Compose file reference](https://docs.docker.com/compose/compose-file/). The top level Compose file sections - `services:` and

| Instruction | Function |
| :--- | :--- |
| args | Adds build arguments that are processed as environment variables during the service build process \(only\). |
| build | Configuration options that are applied to a service at build time |
| depends\_on | Assigns dependencies \(on other services\) to service definitions in a Compose file. with `depends\_on` you also configure container startup order for `docker-compose up` time. |
| deploy | Define deployment and service-run configurations. Only active when deploying to a Docker swarm, using `docker stack deploy`. Compose v3 only. |
| entrypoint | Override for default image entrypoint. |
| expose | Exposes a service port without mapping it to the Docker Host. |
| env\_file | Add environment variables from a file. Can be a single value or a list. |
| labels | Adds metadata to a service. |
| networks | Assigns a network to a service. By default all services run on the same network. |
| ports | Exposes ports for a Docker service and performs port mapping between Docker Host and the service. |
| restart\_policy | Configures service restart when a service exits. |
| volume | Mounts paths or named volumes to a service. For v3 compose files volumes replaces volumes\_from for mounting data containers. _ToDo: check and see if this is the right way to configure storage volumes._ |

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
* Know how to use many DC CLI commands
* Compose your own application from docker-compose.yml
* Compose an application using variables - values in an .env file
* Compose different service environments by using the extended override configuration
* Know how to make a docker-compose.yml file Haufe Group compliant 



