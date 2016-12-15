# Build Docker Images - Draft
This title may also change in the future as Haufe Group incorporates more of docker into its builds. Currently, Haufe only supports a build process for docker images. This build pipeline pushes newly made images into the Haufe Group Docker Registry. 

The build pipeline has these steps
* Dockerfile is added to project
* Project is added to the Source Repository
* The build uses Dockerfile to create an image
* The build pushes this image to haufe registry haufe.docker.io

This is still an early stage of docker capability, but it allows you and others to push your approved images to the Haufe docker registry and to reuse them in future projects: The major advantage being that you can push these app containers anywhere and run them anywhere. 

## Dockerfile
Once you get to this point you need to  conform to the Haufe Group style guide for [Dockerfile practices](/BestPracticesDockerfile.md). 

**Achtung:** For a build Docker image, you must not use volume mounting. You must use COPY or ADD to copy your files directly and bake them into your docker image. your application to the Docker image. If you have been mounting volumes in your dev project you need to change this.

## Source Control
Once you are done developing and debugging, you commit your Dockerfile to source control. These repositories supported for running Docker builds are:
* BitBucket - Here you can commit to the Haufe Group Cloud or on-premise repo
* TFS w/ Git or Team Foundation Version Control

## Supported Repositories

## Supported Build 
* GO.Cd 
* Jenkins
