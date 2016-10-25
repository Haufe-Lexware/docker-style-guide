# Docker file structure
There are generally the following sections: 
* Image configuration 
* Container entrypoint
* Container bash

Let's take a look at a Dockerfile with all three sections. The section names are intuitive

## Image configuration
With this part you configure your image. The parts of  your Docker image that your configure here are:
* FROM - your base image that you found in the last section
* 


## Container entry-point

In this section, you may configure a shell script that runs at Linux boot. This section is good for setting environment variables and other pre-processing steps that must happen before issuing commands over the bash prompt.

## Container bash

In this section, you may configure commands to run from the bash prompt. So if you have created a Docker image that uses several applications to 








