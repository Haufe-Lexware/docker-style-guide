# Docker Host

A Docker Host is a physical or virtual machine with a Linux Operation System and (at least) the [Docker Engine](DockerEngine.md) first. The Docker Engine takes care of everything around building Docker Images or running Docker Containers and connects Docker clients to Docker servers.

## Operating system of the HOST

You **MUST** use one of the following Linux Distributions:

- CentOS/Redhat
- Debian/Ubuntu
- CoreOS

## Patch management

A Docker Host is basically a Linux server an **MUST follow all Operation and Security Guidelines** that are already established at Haufe.

> A Docker Host might be treated as an "immutable" host and after the initial provisioning process, NO further modifications are allowed. 
> 
> As a consequence, ANY changes based on feature or security requests are introduced by switching to a new server that meets ALL THE NEW REQUIREMENTS but is identical otherwise.

## Docker version

IF you are planning to use the Docker Host (later) in production,
you **MUST** install a Docker version > 1.10.2.

You **MUST** verify that the host is configured correctly for
Docker by running [The Docker Bench for Security](https://github.com/docker/docker-bench-security).

> Out of experience, you SHOULD treat section
"1.1 Create a separate partition for containers " like a "MUST".

## Services beside Docker Engine

You **MUST** only install services that are required by
security or operations directly on the Dockerhost:

- docker
- sshd (remote access to "bare" machine)
- monitoring tools (**EXAMPLES**)
  - cAdvisor (metrics)
  - nrpe (Nagios Remote Plugin Executor for availability checks etc.)
