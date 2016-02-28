# Docker Machine / Docker Swarm

According to the [**Docker Machine** overwiew](https://docs.docker.com/machine/overview/), you can use Docker Machine to:

* Install and run Docker on Mac or Windows
* Provision and manage multiple remote Docker hosts
* Provision Swarm clusters

One of the most interesting features for "quick, but secure" Docker Hosts is the ease of getting [Encrypted Connections between **Docker Engines**](DockerEngine.md#enforce-encrypted-ssl-connections-to-the-docker-daemon-api) right.

## Beware of Driver restrictions

While Docker Machine is one of the most convenient methods to create new Docker Hosts in the Cloud, it fails in some areas.

You **SHOULD NOT** use Docker Machine (0.6) to create a Docker Host in Azure, because you can't define a resource group or a virtual network and the result is always one "standalone" machine that has to communicate over its public endpoints.

![](images/DockerMachineAzureNetworking.png)