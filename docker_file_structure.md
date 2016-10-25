# Docker file structure
There are generally the following sections: 
* Image configuration 
* Container entrypoint
* Container bash

Let's take a look at a Dockerfile with all three sections. The section names are intuitive

## Image configuration
With this part you configure your image. The parts of  your Docker image that your configure here are:
* FROM - your base image that you found in the last section
* Copy 
* Run Create a new docker layer makes more sense Modify your image. 
* Volume



Here Link to style guide
## Container entry-point

In this section, you may configure a shell script that runs at Linux boot. This section is good for starting up your applications and services that must happen before issuing commands over the bash prompt. This is the last command Really only. Dummy entry points. Really no third section. 

Here Examples

## Container command

In this section, you may configure commands to run from the bash prompt. If you have created a Docker image that uses several applications to create a "Docker Process", you must start them up in this section of the file.

Here Examples









