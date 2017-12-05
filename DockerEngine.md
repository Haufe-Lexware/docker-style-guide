# Docker Engine

The Docker Engine is used in one or two roles on each [Docker Host](DockerHost.md):

* Docker Client - issuing commands to a local or remote Docker Engine
* Docker Daemon - executing commands send by a Docker Client

![Docker Engine - Client and Host](https://docs.docker.com/engine/article-img/architecture.svg)

## General Installation

There are three quick start guides for installing the **Docker Engine** on a "local" machine to be found at Docker's website:

- [Get Started with Docker Engine for Linux](https://docs.docker.com/linux/)
- [Get Started with Docker for Windows](https://docs.docker.com/windows/)
- [Get Started with Docker for Mac OS X](https://docs.docker.com/mac/)

For non-experimental installations You **MUST** use a [Docker Host](DockerHost.md) as described in the [**Haufe Docker Style Guide**](DockerHost.md).

> Setups with "all you need" for Mac or Windows developers can be found on the [Docker Toolbox](https://www.docker.com/products/docker-toolbox) page. 

Detailed instructions are to be found at [Install Docker Engine](https://docs.docker.com/engine/installation/)

## Enforce encrypted (SSL) connections to the docker daemon API.

A (standard) local installation of Docker is quite safe from a security point of view. Client and server use non-network unix-sockets for communication. Accessing a Docker Daemon via network is a more serious business.

From [Protect the Docker daemon socket](https://docs.docker.com/engine/security/https/):

> If you need Docker to be reachable via the network in a safe manner,
you can enable TLS by specifying the tlsverify flag and pointing Docker’s tlscacert flag to a trusted CA certificate.
>
> In the daemon mode, it will only allow connections from clients authenticated by a certificate signed by that CA. In the client mode, it will only connect to servers with a certificate signed by that CA.

You **MUST** only use such mutual authenticated Docker Engines for Client/Server (Daemon) communication.

IF you have control over the client machine and the remote machine CAN be created in a supported cloud environment (Azure, AWS, Google, ...), then **Docker Machine** is the easiest route to follow. The `docker-machine create ...` command not only creates the cloud instance, but takes care of generating a new certificate on the client and the host, the exchange of the keys and the configuration of the remote Docker Daemon.

If you are using company (Haufe) managed certificates, you have to take care of the configuration (especially of the remote machine) by following the steps in [Protect the Docker daemon socket](https://docs.docker.com/engine/security/https/).

