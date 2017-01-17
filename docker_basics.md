# Docker Basics

Learning the Docker basics means getting up to speed on the Haufe Group Docker tooling and the Docker repositories. More advanced stuff - like composing multiple docker processes into coordinated services or building docker processes and services as part of CI/CD comes later.

The Haufe Group Docker Style Guide has an section on which [Docker tools are accepted](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/HaufeDockerToolset.md). And, There is also a style guide section for [accepted Docker repositories](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/Dockerfile.md#use-only-well-maintained-images-from-a-trusted-registry) - where predefined images can be searched, stored and reused.

We have already linked to docker concepts so hopefully, you've already read up on them. You should have already installed and tested docker, so now, it's time to get started. You may want to bookmark Docker Store too.

## Getting Help

Before getting into the basics, if you need help you can get to various Docker community channels from [this web page](https://docs.docker.com/opensource/get-help/). And also, of course, you can get help at the [Stackoverflow Docker area](http://stackoverflow.com/documentation/docker/topics).

Additionally, you can ask questions to the Haufe Docker Community in our [Rocket Chat Docker Channel](https://chat.haufe.com/channel/docker).

Don't hesitate to ask for help. Docker has a big community, and usually it's better to ask around before you experience frustration.

## A work flow proposal to capture the basics

There are lots of ways to learn Docker but one way of doing it is to follow these steps:

* Learn Docker Hub - Create a Docker ID. Learn what's out there so you can avoid doing extra work
* Learn the Docker Engine Client and Client commands - You'll need this at build time too!
* Learn to build images with the Dockerfile - define and document Docker images with on artifact
* Learn about the docker-machine - the tool that manages Docker host machines and Docker swarms

In this section you are going to create a base image, use Dockerfile to create images, and learn how to create new hosts and manage these hosts.

Never forget: You can always learn more. But to get started, it's probably best to review [how docker images and containers work](https://docs.docker.com/engine/getstarted/step_two/). Also before your get started, please read:

* [Haufe Docker Style Guide - Docker Images](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/DockerImage.md)
* [Haufe Docker Style Guide - Docker Containers](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/DockerContainer.md)
* [Haufe Docker Style Guide - Container Best Practices](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/BestPracticesContainer.md)



