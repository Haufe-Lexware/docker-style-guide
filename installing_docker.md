# Installing Docker
This is completely up to you. Docker comes in several different flavors. However, it probably makes most sense to install Docker in a Linux environment. We have noticed some problems with drive sharing on Docker for Windows, here it was important to use the “Network user” – Domain\UserName – to be able to perform mounts between the host file system and docker file system: The Network User is the “real owner” of your computer’s file system, and you must use this user to be able to enable sharing and mounting. 

Official Docker documentation has an excellent and comprehensive tutorial on how to install docker [at this location](https://docs.docker.com/engine/getstarted/step_one/) . Here the Docker Docs step you through doing a basic install of docker for your flavor of operating system and how to test docker by running the "hello world" Docker image. Specific links are:
* [Install Docker for Windows](https://docs.docker.com/engine/installation/windows/)
* [Install Docker for Mac](https://docs.docker.com/engine/installation/mac/)
* [Install Docker for Ubuntu](https://docs.docker.com/engine/installation/linux/ubuntulinux/)

You can reach installation instructions for other Linux distributions from [https://docs.docker.com/ and by looking under “Docker Engine” > “Install” > “Linux Distributions” on the left hand menu](https://docs.docker.com/).

While you can run Docker on just about any kind of OS, Docker hosts and containers are always Linux-based, and so, it's important to get familiar with basic Linux commands and Linux utility commands - for example how to use "apt" for retrieving and updating new packages on Ubuntu Linux and basics like "chown", "chmod".

Once you get docker installed, you are going to start working with: 
* [Registries](https://docs.docker.com/docker-hub/)
* [Images](https://docs.docker.com/engine/understanding-docker#docker-images)
* [Containers](https://docs.docker.com/engine/understanding-docker#docker-containers)

Later you will be working with docker environments and docker services

**Achtung:** If you are running on Windows, it helps to download a git client and then to install so you can run Linux commands in Powershell or DOS prompt.

## Using Docker inside the Haufe Network
If you plan to use docker from the offices in Freiburg, You have to ensure that the Haufe Proxy and the Haufe Firewall do not block your Docker from communication with the internet. You are going to go out and get images from Docker Hub and other repositories. There are a couple of workarounds here. 

Go to the [Getting Started - Docker for Windows](https://docs.docker.com/docker-for-windows/) or [Getting Started - Docker for Mac](https://docs.docker.com/docker-for-mac/) and read up on how to access the settings. For the "Dockers For" tools you will at least have to:
* Share drives for Docker volumes
* Set proxies
* Set No_Proxy

And you may have to:
* Change network settings

For the Docker for Windows or IOS, one nice setting is that you can configure the firewall to propagate down to the Docker Host level. You can also set “no_proxy” exceptions from within the Docker Application. For Linux you can set the environment variables – HTTP_PROXY, HTTPS_PROXY and NO_PROXY for the domains where you intend to work with Docker. 

Even if you have already done this in the Docker for Windows / Mac settings. You may still have some problems building images. 

For Linux you will have to set these proxy settings as environment variables and in the docker.io file, restarting the docker service. 

**Achtung:** On Windows, I have also encountered some problems at create image time when extending base image by using package managers like “apt” on Linux from a Dockerfile. The workaround for this was to add build arguments that set the proxy server. In Docker you can do this two ways
•	Use the -–build-arg option with the “docker build” command
•	Use the ARG instruction in a Dockerfile
These arguments are only passed to the builder and do not persist in the container


### Develop Remotely

If you are developing remotely, perhaps the easiest way to get around the proxy is to set up a virtual machine on an external service like Azure and depending on the OS, to use an RDP client or your favorite SSH client to tunnel in to remote virtual machine. Here again you have to know how to get outside of the Haufe proxy server and firewall. Once you are on your remote machine, you can install docker and create docker solutions without the normal networking constraints. 

This can be a workaround to the firewall but can only be a permanent solution if it is comfortable, secure and performant enough. 












