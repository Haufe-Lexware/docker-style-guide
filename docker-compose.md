# Composing applications with Docker Compose

Composing is exactly what you do with docker compose. While it's possible to create an application from a single docker image, when you think about docker's purpose - to serve as a packaging system for our software applications and also how docker "packages" these applications - creating a full-blown application on one image requires more work than creating many base images and configuring them to work together and is, in the end, inefficient. Docker-Compose enables you to configure and run multi-container applications.

Like Dockerfile, Docker Compose file serves as the configuration and documentation. For Docker Compose though, you are configuring multi-container applications. Unlike images built with Dockerfile, where you build and then run, you can run applications packaged via Docker-Compose directly, using the Docker Compose CLI.

Docker Compose also provides you with an easy way to isolate different application environments from one another and even to use variables within the docker-compose.yml file. Haufe Group Docker Style Guide has both requirements and best practices for working with Docker Compose and creating Docker Compose files:



Get started by going through Docker's [Docker Compose documentation](https://docs.docker.com/compose/overview/)

