#Docker-Host (machines that host the docker daemon)

## Basics

While the Dockerfile is the description how to create the requirements for ONE container and a docker-compose.yml describes (network/orchestration as code) the relation between containers, there is still the VERY FOUNDATION of it all: The setup of the machine (virtaul or physical) where the real docker daemon does its magic.

Most of the time this will be some "simple" Linux server with docker installed.

## Services
As a golden rule (this is almost mandatory), ONLY INSTALLED ABSOLUTE NECESSARY SERVICES:
- docker
- sshd
- monitoring/logging

## Partiton-Layout
Always use a separate partition for the Docker-Containers. If you ask any experienced Linux admin, he will knwo about some "horror" stories about servers that were unusable, only because some important partition was "full".

To prevent something like that, because the number of Docker-images wasn't taken into account or the containers created to many files etc. you simply have to provide the docker-daemon with a partiton of its own for the images. (/var/lib/docker)

It is NOT YET DECIDED, if and how those docker-hosts will be patched/upgraded.

---

