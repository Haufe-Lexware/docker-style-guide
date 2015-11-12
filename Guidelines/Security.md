Security
========

Using Docker means (more or less) to move an application into a standardized container for subsequent use.
As one might expect, there are a couple of security considerations (as always). Docker addresses this on https://docs.docker.com/articles/security/ :
  > There are three major areas to consider when reviewing Docker security:
  * the intrinsic security of the kernel and its support for namespaces and cgroups;
  * the attack surface of the Docker daemon itself;
  * loopholes in the container configuration profile, either by default, or when customized by users.
  * the “hardening” security features of the kernel and how they interact with containers.

To mitigate those problems, you should follow theses suggestions:
  * Only make necessary ports of the container available (EXPOSE and PORTS)
  * Never run anything as root within a container. If you do, you’ll just be asking for trouble.
  * Enforce encrypted (SSL) connections to the docker daemon API.
  * ONLY install docker, sshd and (host-)monitoring tools on a dockerhost.
  * Only put data of the same sensitivity level AND of the same owner onto the same dockerhost.
  * DO NOT include credentials/keys/certs/... in Docker-Images
  * DO NOT (IMPLICITLY) TRUST EXTERNAL/3RD PARTY IMAGES.

Only make necessary ports of the container available (EXPOSE and PORTS)
------------------------------------------------------------------------
Docker strives for security. Isolation (namespaces) and control (cgroups) are quite successful in preventing processes INSIDE the containers from wreaking havoc on other containers or the dockerhost.

Like with other (virtual) servers, security is directly related to accessible endpoints of the systems. The fewer endpoints are available to "the public", the better. As a rule of thumb, you should use EXPOSE for everything, except the service the container/composition should provide to the outside of the dockerhost where you have to use PORTS.

E.g. in case of a standard LAMP stack, there's no need to use PORTS for the mysql container, because it only provides the mysql services to the PHP container (EXPOSE is sufficient). The Apache service uses PORTS to provide 80 and 443.

Never run anything as root within a container. If you do, you’ll just be asking for trouble.
---------------------------------------------------------------------------------------------
For the time being (we’re at docker 1.6), user - IDs are “shared” between containers and the host.

A container-process run as root with uid “0” (inside the container) has the same permissions in respect to accessing mounted volumes etc. (could change everything) as root from the docker-host.

Create the Docker-Containers in a fashion that the intended process runs as a NON-ROOT/-SYSTEM user. It is suggested to create a separate user/group for each service. See http://refspecs.linux-foundation.org/LSB_3.1.0/LSB-Core-generic/LSB-Core-generic/usernames.html:

  > Generally daemons should now run under individual User ID/Group IDs in order to further partition daemons from one another.

If possible, set the effective runtime-user in the dockerfile.

Example:

``` dockerfile
FROM ubuntu

# Installing as almighty "root"
RUN ...
COPY ...

# now switching to harmless "sample_daemon" runtime user
USER sample_daemon

ENTRYPOINT ["/my_entrypoint.sh"]
CMD ["/my_command.sh"]
```

Enforce encrypted (SSL) connections to the docker daemon API.
--------------------------------------------------------------
When controlling the dockerhost from remote via docker, docker-compose or docker-machine, ONLY authenticated users MAY be permitted. docker-machine guarantees this by creating certificates for docker-host AND client to enforce an encrypted connection that verifies (by validating the certificates) the correct target (dockerhost) from a valid client (e.g. docker-compose)

> …, you MUST use secure-socket layer (SSL) web connections, and making the connection over a virtual private network (VPN) wouldn’t be amiss either.

ONLY install docker, sshd and (host-)monitoring tools on a dockerhost.
-----------------------------------------------------------------------
Just because your database server (with a huge amount of sensitive or valuable data) is somewhat underutilized, it is not a good idea to install docker on the same machine. IF there is some vulnerability in Docker, the otherwise services are at immediate risk!

> Given the Docker daemon’s potential to be used for harm, it’s also a good idea to run Docker instances on their own servers. The only other software that should run on those servers are SSH server and monitoring and logging programs (such as Nagios Remote Plugin Extender (NRPE)).

Only put data of the same sensitivity level AND of the same owner onto the same dockerhost.
-------------------------------------------------------------------------------
Like the "no docker on a machine with other services" rule, you MUST NOT put data from different owners/customers onto the same dockerhost. In case of a security breach in one of the customer-containers, other customers MUSTN'T BE AFFECTED. This holds true for data theft, corruption etc. as well as rendering a service useless for one customer (DoS ...).

DO NOT include credentials/keys/certs/... in Docker-Images
----------------------------------------------------------
A Docker image MUST NOT contain authentication or authorization information for provided or consumed services to prevent
security breaches by only getting a "copy" oth the sole Docker-image.
Required credentials/keys or similar data MUST be injected into the docker-image at startup time using the environment.

DO NOT (IMPLICITLY) TRUST EXTERNAL/3RD PARTY IMAGES.
--------------------------------------------------------
Using the command `docker pull image` or the line `FROM image` in docker-compose.yml are like using a black box. You just download a (hopefully) usable container - without knowing what's really inside.

Since Version 1.3 of docker, there is a feature for the official Docker-registry ( https://registry.hub.docker.com/ ) that provides "a level of trust" for the retrieved image:

  > ... the Docker Engine will now automatically verify the provenance and integrity of all Official Repos using digital signatures. Official Repos are Docker images curated and optimized by the Docker community to be the best building blocks for assembling distributed applications.  A valid signature provides an added level of trust by indicating that the Official Repo image has not been tampered with.


And you are going to build YOUR software on top of that? And present/offer that to our customers?

  > In doubt, get the Dockerfile, the resources and build the Docker container yourself.

---

[Guidelines](Guidelines)  
[Docker Docs - Home](../wiki/Home)  
