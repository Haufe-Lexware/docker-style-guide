# Build Docker Images
This title may also change in the future as Haufe Group incorporates more of docker into its builds. Currently, Haufe only supports a build process for docker images. This build pipeline pushes newly made images into the Huafe Docker Registry. 

The pipeline has several steps
* Dockerfile is added to project
* Project is added to the Source Repository
* Project is built from source and and added to the haufe registry haufe.docker.io

## Dockerfile
* No Volume Mounting use COPY or ADD to move add your application to the Docker image
* 


## Source 
* BitBucket
* TFS w/ Git

## Supported Repositories

## Supported Build 
* GO.Cd 
* Jenkins
