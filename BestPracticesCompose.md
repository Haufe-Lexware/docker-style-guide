# Best practices **Docker Compose**

## Container-Compositions are **Microservices**

A container-composition can/should be seen as a microservice. If the Container-composition can be started, it should successfully provide the intended service.

## Use Environment Variables

In the past, a docker-compose file could only be used "as is" and it was necessary to handle environment specific information "manually" by either using copies of the compose file or by using different directories with env specific env_files etc.
Since 1.5, you can use **variable expansion** to organize env-specific settings more easily. Here's an example that shows how to use the environment variable "ENV" for selecting a specific "env_file" that sets the environment variable "ME" being used as part of the command executed in the container:

The docker-compose file:

    $ cat docker-compose.yml
    version: "2"
    services:
      dummy:
        env_file: ${ENV}
        image: ubuntu
        command: /bin/sh -c "echo $${ME}"

The two env_file(s):

    $ cat .env1
    ME=me

    $cat .env2
    ME=I

Check for the environment variable "ENV" controlling the env_file setting in the docker-compose.yml:

    $ ENV=.env1 docker-compose up dummy
    Recreating identityandservices_dummy_1
    Attaching to identityandservices_dummy_1
    dummy_1 | me
    identityandservices_dummy_1 exited with code 0

	$ ENV=.env2 docker-compose up dummy
    Recreating identityandservices_dummy_1
    Attaching to identityandservices_dummy_1
    dummy_1 | I
    identityandservices_dummy_1 exited with code 0
