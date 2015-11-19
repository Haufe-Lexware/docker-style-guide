# Docker Container

## Don't force your Tool/Stack on others

On the commandline (using a Dockerfile to create a Docker-image) the standard command `docker build .` should be sufficient to get the job done.

## Keep Dockerfiles simple and lean

Best use `RUN ...` commands that would work on the commandline without other installation tools. The usual suspects for configuration management on a server  (puppet, ansible, chef, ...) would
- add new filesystem/cache-layers
- add unnecessary bloat to the Docker-image (if you wouldn't remove the tools)
- add complexity (do you REALLY need some additional ppa only to get YOUR most loved tool ?)

## ONYL Base-Images MAY contain Package-Installer "update/upgrade" commands

The first reason is that such commands might invalidate almost everything in/from the cache.  
__The second one is that those command might create a "alternative version" of the baseimage that interferes__ 
__with other (unmodified) containers that use the base image. Finding such modifications can be a quite difficult.__ 
__Much better is to ask for a updated or new baseimage.__

## One (exposed?) Service per Container

Docker is still a process or application isolation tool. As a consequence, a webserver container mustn't provide the db but use a separate container that has the db as it's sole service.

## NO backdoors/remote access

A container IS NOT A SERVER that needs a login service (telnet, ssh, ...). For debugging/inspection purposes, use `docker attach` or a shell (bash, sh, ...) with `docker run -i -t image_name /bin/bash`.

## Use Data-Only Container

You wouldn't want to lose your precious data (or that of a customer), only because the app-container has to be destroyed during scaling/replacement/....

## No volume-mounts on "local" machine

There is NO guarantee that the (Docker) runtime systems are identical (CoreOs, Ubuntu + Docker, RancherOS)

## No "company-exposure"

Never put information about "company-configurations etc." into Containerfiles; That might be ip-addresses, firewall-setups and the like. Those informations are only allowed in runtime definitions (like credentials or certificates).

## Beware of Build-dependencies

A Docker-Container should be "buildable" on any machine/enironment without the need for specific server/services (specific app-repository, user-databases, ...)

## Container are ephermal

Expect the app instance to be destroyed and restarted in a NEW instance at ANY time.

As a consequence, it's best to make your services stateless

## Container-Compositions (e.g.: docker-compose) are self - sufficient

A container-composition can/should be seen as a microsoervice. If the Container-composition can be started, it should successfully provide the intended service.

## Container - "readiness"

A container is an entity that can be used "out of the box". You wouldn't expect additional "preparation" steps or long-lasting "warm-up" phases.
A Docker container should be ready to start "at an instant", with only "parameters" for "personalization". An example would be some web-server that is started with the server-hostname as a parameter.

## Startup-Data via environment

The "environment" in Docker can be setup either by commandline params to `docker`, `docker-compose`, etc. or (sometimes) as a file. For example, there is the option to use an `env_file` to keep the environment definitions out of the `docker-compose.yml`.

## Only use images (prebuild containers) from trusted  repositories

## Never add credentials (username/password/apikeys/certificates) to containers

## Container isolation

How to isolate container for specific customers (e.g. one dockerhost per VM/PM)

---

