# Composing applications with Docker Compose

Composing is exactly what you do with Docker compose. While it's possible to create an application from a single docker image, when you think about docker's purpose - to serve as a packaging system for our software applications and also how docker "packages" these applications - creating a full-blown application on one big image requires more work than creating many small images and configuring them to work together when Docker is involved. Single big images defeat the purpose of Docker. In [Docker Compose Overview](https://docs.docker.com/compose/overview/)    states that:

> Compose enables you to configure and run multi-container applications.

Like Dockerfile, Docker Compose file serves as configuration and documentation. With Docker Compose though, you are configuring multi-container applications. Unlike images built with Dockerfile, where you build and then run, you can run and manage applications packaged with Docker-Compose directly, using the Docker Compose CLI. Once you start using Compose, you can \(mostly\) say bye-bye to the `docker run` command. Maybe the best definition of a Docker Compose file by Docker is:

> The Compose file is a YAML file defining services, networks and volumes. The default path for a Compose file is ./docker-compose.yml.

### Extending your composed application

Docker Compose provides you with an easy way to isolate different application environments from one another. Highly convenient is that you can extend your Compose configuration with additional files to:

* Use variables within your files - .env files
* Create different service configurations e.g CI, Test, Production - .override files

This can be helpful if you want to test different Compose environments. 

### Docker Compose practices

Haufe Group Docker Style Guide has practices for working with Docker Compose and creating Docker Compose files:

* [Docker Compose](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/DockerCompose.md)
* [Docker Compose Best Practices](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/BestPracticesCompose.md)

Once you have read through these, get started by going through Docker's [Docker Compose documentation](https://docs.docker.com/compose/overview/), starting with the overview and working through the entire Compose section. You can leave out the experimental and "superseded" sections. 

### Docker Compose practice

The best way to understand Compose is to practice. The getting started section and  tutorials in this documentation can help. Direct links to these are:

| Tut | Docker Skill |
| --- | --- |
| [Getting started](https://docs.docker.com/compose/gettingstarted/) | Learn how to to compose a basic Python app, using two services, learn compose file instructions |
| [Django](https://docs.docker.com/compose/django/) | Learn set up a Django / Postgre app, learn how to further define services - build, volumes, ports, depends\_on |
| [Wordpress](https://docs.docker.com/compose/wordpress/) | Learn how to set up a Wordpress service with MySQL and a data volume service, learn how to set environment variables from Compose file, learn the restart instruction |

To get a really good basic knowledge, add these tasks when you work the tutorials:

* Extend the configuration of each Compose file and create multiple environments with .env and .override files.
* Apply Haufe Group practices to all Compose Files. **Hint:** No secrets, Data Containers and so on. 

### Section Targets

* Understand the concept behind Docker Compose and how it should be used in Haufe Group
* Create several composed applications by working the docker tutorial
* Know how to use many DC CLI commmands
* Compose your own application from docker-compose.yml
* Compose an application using variables - values in an .env file
* Compose different service environments by using the extended override configuration
* Know how to make a docker-compose.yml file Haufe Group compliant 



