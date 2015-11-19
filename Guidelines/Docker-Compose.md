# docker-compose

## Use docker-compose for orchestration only
The orchestration (or composition) that is defined by some docker-compose.yml MUST NOT contain the `build:`-statement, 
but only `image:`-lines. 

Using `build:` would start (implicitly) a docker-build, that most likely require a completly different environment   
than the runtime settings.

See [image online documentation](https://docs.docker.com/compose/yml/#image) and [build online documentation](https://docs.docker.com/compose/yml/#build)

## Move environment settings to separate file
Environment settings like username, api-id, ... MUST NOT be stored as part of the general sourcecode. 
One convenient feature of docker-compose is the `env-file:`- statement that includes a simple key/value 
file that can be persisted separatly. See [env-file online documentation](https://docs.docker.com/compose/yml/#env-file)

---
