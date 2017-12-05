# Building Docker Images with Haufe Group Build Infrastructure - Draft

This title may also change in the future as Haufe Group incorporates more of Docker into its builds. Currently, Haufe only supports a build process for docker images. This build pipeline pushes newly made images into the Haufe Group Docker Registry.

The build pipeline has these steps:

* Dockerfile is added to project
* Project is added to the source repository and is picked up by the build
* The build uses Dockerfile to create an image
* The build pushes this image to haufe registry haufe.docker.io

This is still an early stage of docker capability, but it allows you and others to push your approved images to the Haufe docker registry and to reuse them in future projects: The major advantage being that you can push these app containers anywhere and run them anywhere.

## Dockerfile

Once you get to this point you need to  conform to the Haufe Group style guide for [Dockerfile practices](/BestPracticesDockerfile.md).

**Achtung:** if you want to build your Docker image, you must not use volume mounting in your Dockerfile. Instead, you must use COPY or ADD to copy your files directly and bake them into your docker image.  If you have been mounting volumes in your dev project you need to change this before your build.

## Source Control

Once you are done developing and debugging, you commit your Dockerfile to source control. These repositories supported for running Docker builds are:

* BitBucket - Here you can commit to the Haufe Group Cloud or on-premise repo
* TFS w/ Git or Team Foundation Version Control.

On commit of a Dockerfile to either one of these repositories \(that have been configured to build for Docker\), your Docker image is built.

## Supported Build Tools

Build tools that support building Haufe Group Docker image are:

* GO.Cd 
* Jenkins

### Go.Cd

Go.Cd is thoughtworks continuous delivery tool that enables to configure and run continuous delivery pipelines for code projects. Haufe Group has written an plugin for go cd that builds the image Dockerfile and pushes the image to the Haufe repository.

### Jenkins

Jenkins also supports building Docker images. Since there is no Docker plugin for Jenkins, this where the Docker Engine CLI `build` and `push` commands are automated.

In any case, both Go.Cd and Jenkins support building Docker images and placing them in our Docker registry.

### Contact release engineering

The release engineering folks who are in charge of this are:

* Nicolas Dille
* Markus Wehrle

Contact them if you have any further questions.

