# Glossary

**Docker practices**: Docker practices are the concrete implementations of our Docker Principles and other low-level technical Docker practices to ensure security and so on. An example of a Docker practices is that no secrets are allowed in Dockerfile.

**Docker principles**: Docker principles are essentially what we want to use Docker and Docker tooling for at Haufe Group. Using Docker for packaging and orchestration of software is one of our Docker principles. Docker principles can be implemented in different ways depending on the context of use. How we implement these principles are Docker practices. There are not too many of these.

**Docker services** - Docker services are individual services used to create a composed application. Services are individually described in a Docker Compose file and when running each service runs in on container.

**Section targets**: Section targets are learning targets placed at the end of each section in the book. These targets show you what you will have learned if you read and work through the linked documentation. Using these targets you can reflect on whether or not you've learned enough or if you should go back and do some more.

**Instruction:** An instruction is an entry in either a Dockerfile or a Docker Compose file. Instructions "instruct" the Docker build component or Docker Compose what to do with the purpose:

* To build an image \(`docker build` command\)
* To spin up a docker services into Docker applications \(`docker-compose up` command, et al.\)

Examples of Docker instructions are: **Dockerfile**: FROM, COPY, ADD, VOLUME, EXPOSE. **Docker Compose**: services, image, ports, restart.

**Command: **A command is issued from the the CLI or uses the Docker API to direct the Docker Daemon to do something. CLI Examples:

* `docker run`
* `docker images`
* `docker rm`



