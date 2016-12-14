# Build Docker Images - Draft
This title may also change in the future as Haufe Group incorporates more of docker into its builds. Currently, Haufe only supports a build process for docker images. This build pipeline pushes newly made images into the Haufe Group Docker Registry. 

The build pipeline has these steps
* Dockerfile is added to project
* Project is added to the Source Repository
* The build uses Dockerfile to create an image
* The build pushes this image to haufe registry haufe.docker.io

## Dockerfile
Once you get to this point you need to  conform to the Haufe Group style guide for [Dockerfile practices](/BestPracticesDockerfile.md). 

**Achtung:** You must not use volume mounting. You must use COPY or ADD to copy your files directly into the docker image. your application to the Docker image



## Source 
* BitBucket
* TFS w/ Git

## Supported Repositories

## Supported Build 
* GO.Cd 
* Jenkins
