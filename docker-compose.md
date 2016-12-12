# Composing applications with Docker Compose

Composing is exactly what you do with docker compose. While it's possible to create an application from a single docker image, when you think about docker's purpose - to serve as a packaging system for our software applications and also how docker "packages" these applications - creating a full-blown application on one big image requires more work than creating many small images and configuring them to work together. Single big images defeat the purpose of Docker. In [Docker Compose Overview](https://docs.docker.com/compose/overview/)    states that:


```
Compose enables you to configure and run multi-container applications. 

```

Like Dockerfile, Docker Compose file serves as configuration and documentation - providing Docker Compose . For Docker Compose though, you are configuring multi-container applications. Unlike images built with Dockerfile, where you build and then run, you can run and manage applications packaged vwith Docker-Compose directly, using the Docker Compose CLI. Once you start using Compose, you can (mostly) say bye-bye to the `docker run` command. Maybe the best definition of a Docker Compose file by Docker is: 

```
The Compose file is a YAML file defining services, networks and volumes. The default path for a Compose file is ./docker-compose.yml.
```

Docker Compose provides you with an easy way to isolate different application environments from one another. Highly convenient is that you can extend your compose configuration with addtional files to:
*Use variables within your files - .env files
*Create different service configurations e.g CI, Test, Production - .override files

Haufe Group Docker Style Guide has both requirements and best practices for working with Docker Compose and creating Docker Compose files:

* [Docker Compose](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/DockerCompose.md)
* [Docker Compose Best Practices](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/BestPracticesCompose.md)

Once you have read through these, get started by going through Docker's [Docker Compose documentation](https://docs.docker.com/compose/overview/)

### Section Targets
* Understand the concept behind Docker Compose and how it should be used in Haufe Group
* Create several composed applications by working the docker tutorial
* Know how to use many DC CLI commmands
* Compose your own application from docker-compose.yml
* Know how to make a docker-compose.yml file Haufe Group compliant - example using data containers as volumes, no-secrets, use variable expansion.

