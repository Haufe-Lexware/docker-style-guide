# Docker Images

Docker Images are the result of using `docker build` with a [Dockerfile](Dockerfile.md).

## Docker Engine commands for Docker Images

![Docker Engine Commands](https://raw.githubusercontent.com/rossbachp/docker-basics/master/images/docker-command-flow.png)

## Getting (pulling) acceptable/reliable DockerImages

To cut a long story short: We trust "Docker" and "ourselves". As a consequence, you can pull images from hub.docker.com, docker.io or registry.haufe.io.

A (tiny bit) more elaborate explanation can be found at https://github.com/Haufe-Lexware/docker-style-guide/blob/master/Dockerfile.md#use-only-well-maintained-images-from-a-trusted-registry

## Names and TAGs

Without preparations, a Docker Image has only a quite long HASH identifier. To make the (human) handling with a Docker Image easier, it **MUST** have at least a name and a `TAG`.
The name tells what to expect in/from the image and the TAG provides a version, a date or buildnumber to distinguish between different builds or compilations of an Docker Image. 

myregistry/myuser/myservice:1.0.1-nginx

How the Name and TAGs are used in Docker processes and workflows, you can see in the example [Tag, push and pull your image](https://docs.docker.com/linux/step_six/)

## Here is some help for what image names and versions should contain:

0. Image names should not contain version info "in themselves".  
  Example: There is no mysql4:1.0 or ubuntu14:0.4 but only mysql:4.x.x and ubuntu:14.0.4
  
1. container:latest - you **MUST** use "latest" only with the most recent **STABLE** version (not necessarily the latest being build). 
  Meaning: The version everybody should use because he/she doesn't know any better.  
    Example: php or php:latest
  
2. container:major - this is for a specific version/featureset.  
  Meaning: For testing of forward- or backward compatibility  
  Example: php:4, php:5 or php:7  
  
3. container:major.minor - this is for a specific (compatible) version with a compatible featureset  
  Meaning: A (backward) container with no breaking changes, but new/removed plugins or optimizations  
  Example: mysql:5.6 vs mysql:5.7
  
4. container:major.minor.build - this is/must be EXACTLY THE current container. If anybody needs THIS container he has to use this tag.  
  Meaning: Builds are most likely security fixes etc. that are NOT intended to change any functionality.You might want to FORCE the presence of a specific (old) error, check the absence of a problem in a new container or guarantee compatibility while using a new version  
  Example: mysql:5.6.28 vs mysql:5.7.10  
  
## Adding information to version

X.a. container:info  
X.b. container:major-info  
X.b. container:major.minor-info  
X.d. container:major.minor.build-info  
  Meaning: Most likely, there are "base" containers, that can be use in conjunction with other parts, but provide the same base service.  
  Example: php:5.6.17-cli (is IDENTICAL to php:5.6.17 and so the default)  
  Example: php:5.6.17-apache is an php container installation that provides the apache webserver WITH php  
  Example: php:5.6.17-fpm is an php container that can be used with nginx (FPM=FastCGI Process Manager)
