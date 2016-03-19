# Best practices **Docker Compose**

## Container-Compositions are **Microservices**

A container-composition can/should be seen as a microsoervice. If the Container-composition can be started, it should successfully provide the intended service.

## Use Environment Variables

In the past, a docker-compose file could only be used "as is" and it was necessary to handle environment specific information "manually" by either using copies of the compose file or by using different directories with env specific env_files etc.
