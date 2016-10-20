# Installing Docker

Official Docker documentation has an excellent and comprehensive tutorial on how to install docker [at this location](https://docs.docker.com/engine/getstarted/step_one/) . Here the Docker Docs step you through doing a basic install of docker for your flavor of operating system and how to test docker by running the "hello world" Docker image.

While you can run Docker on just about any kind of OS, a Docker host is always Linux-based, and so it's important to get familiar with basic Linux commands and Linux utility commands - for example "apt-get commands" for retrieving and updating new packages on Ubuntu Linux.

## Using Docker inside the Haufe Network

If you plan to use docker from the Offices in Freiburg, You have to ensure that the Haufe Proxy and the Haufe Firewall do not block your Docker from communication with the internet. You are going to want to go out and get images from Docker Hub after all. There are a couple of workarounds here. Here How to get around working inside the Firewall/Proxy Server environment in an easy way. 

### Documentation for Windows and Mac machines

1. Go to the [Getting Started - Docker for Windows](https://docs.docker.com/docker-for-windows/) or [Getting Started - Docker for Mac](https://docs.docker.com/docker-for-mac/) and read up on how to access the settings
2. Navigate down to the "Proxies" Section - on mac this is the "Advanced" section.
3. Once you have read the documentation follow the steps on your own machine, Proxy Server URL for both http and https is: http://10.12.1.236:8083/

The Proxy server settings should propagate down to all Docker layers. If there are domains that your wish to exclude from using the proxy settings like your home network, add the IP address into the exclude section of the software to configure the "no_proxy" setting.

### Develop Remotely

If you are developing remotely, perhaps the easiest way to get around the proxy is to set up a virtual machine on an external service like Azure and depending on the OS, to use an RDP client or your favorite SSH client to tunnel in to remote virtual machine. Here again you have to know how to get outside of the Haufe proxy server and firewall. Once you are on your remote machine, you can install docker and create docker solutions without the normal networking constraints. 












