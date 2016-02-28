# Best practices **Docker Compose**

## Move environment settings to separate file

Secret Environment settings like username, api-id, ... MUST NOT be stored as part of the general sourcecode.
One convenient feature of docker-compose is the `env-file:`- statement that includes a simple key/value
file that can be persisted separatly. See [env-file online documentation](https://docs.docker.com/compose/yml/#env-file)

## Container-Compositions are **Microservices**

A container-composition can/should be seen as a microsoervice. If the Container-composition can be started, it should successfully provide the intended service.

