# Docker Basics
Learning the docker basics means getting up to speed on the Haufe Group docker tooling and the accepted docker repositories. More advanced stuff - like composing multiple docker processes into coordinated services or building docker processes and services as part of CI/CD comes later. 

The Haufe Group Docker Style Guide has an section on which [Docker tools are accepted](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/HaufeDockerToolset.md). And, There is also a style guide section for [accepted Docker repositories]( https://github.com/Haufe-Lexware/docker-style-guide/blob/master/Dockerfile.md#use-only-well-maintained-images-from-a-trusted-registry) - where predefined images can be searched and reused.

We have already linked to docker concepts so hopefully, you've already read up on them. You should have already installed and tested docker, so now, it's time to get started.

## A work flow proposal to capture the basics
There are lots of ways to learn Docker but one way of doing it is to follow these steps:
* Learn Docker Hub - Learn what's out there so you can avoid doing extra work
* Learn the Docker Engine Client and Client commands - You'll need this at build time too!
* Learn to build images with the Dockerfile - define and document Docker images with on artifact
* Learn about the docker-machine - the tool that manages Docker host machines and Docker swarms

In this section you are going to create a base image, use Dockerfile to create images, and learn how to create new hosts and manage these hosts. 










To get up to speed go ahead work through the Docker documentation, starting with the [Docker docs welcome page](Docker docs welcome page).

Never forget: There is always more. But to get started it's probably best to understand at least [how docker images and containers work](https://docs.docker.com/engine/getstarted/step_two/). 

You also want to understand how docker engine and 