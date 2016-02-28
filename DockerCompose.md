# Docker Compose

The [documentation](https://docs.docker.com/compose/overview/) says, that

> Compose is a tool for defining and running multi-container Docker applications.

Because you can do a lot more that that, the guidelines restrict some usages.

## Use docker-compose for orchestration only
You **MUST NOT** use **Docker Compose** for building **Docker Images**, but only for defining runtime environments.

> The exception to this rule is to an configuration/secret container that uses environment variables from the **Docker Compose** arguments OR from an `env_file`.

## NO secrets in Dockerfile (or its repository)

