# Installing Docker
This is completely up to you. Docker comes in several different flavors. However, it probably makes most sense to install Docker in a Linux environment. We have noticed some problems with drive sharing on Docker for Windows, here it was important to use the “Network user” – Domain\UserName – to be able to perform mounts between the host file system and docker file system: The Network User is the “real owner” of your computer’s file system, and you must use this user to be able to enable sharing and mounting. 

Official Docker documentation has an excellent and comprehensive tutorial on how to install docker [at this location](https://docs.docker.com/engine/getstarted/step_one/) . Here the Docker Docs step you through doing a basic install of docker for your flavor of operating system and how to test docker by running the "hello world" Docker image. Specific links are:
* [Install Docker for Windows](https://docs.docker.com/engine/installation/windows/)
* [Install Docker for Mac](https://docs.docker.com/engine/installation/mac/)
* [Install Docker for Ubuntu](https://docs.docker.com/engine/installation/linux/ubuntulinux/)

You can reach installation instructions for other Linux distributions from [https://docs.docker.com/ and by looking under “Docker Engine” > “Install” > “Linux Distributions” on the left hand menu](https://docs.docker.com/).

While you can run Docker on just about any kind of OS, Docker hosts and containers are always Linux-based, a

---

nd so it's important to get familiar with basic Linux commands and Linux utility commands - for example h

---

ow to use "apt" for retrieving and updating new packages on Ubuntu Linux and basics like "chown", "chmod".

Once you get docker installed, you are going to start working with: 
* [Registries](https://docs.docker.com/docker-hub/)
* [Images](https://docs.docker.com/engine/understanding-docker#docker-images)
* [Containers](https://docs.docker.com/engine/understanding-docker#docker-containers)

Later you will be working with docker environments and docker services

If you are running on Windows, it helps to download a git client and then to install so you can run linux commands in Powershell or Command Console.

## Using Docker inside the Haufe Network

If you plan to use docker from the Offices in Freiburg, You have to ensure that the Haufe Proxy and the Haufe Firewall do not block your Docker from communication with the internet. You are going to go out and get images from Docker Hub and other repositories. There are a couple of workarounds here. Here How to get around working inside the Firewall/Proxy Server environment in an easy way. 

### Documentation for Windows and Mac machines TBD

1. Go to the [Getting Started - Docker for Windows](https://docs.docker.com/docker-for-windows/) or [Getting Started - Docker for Mac](https://docs.docker.com/docker-for-mac/) and read up on how to access the settings
2. Navigate down to the "Proxies" Section - on mac this is the "Advanced" section.
3. Navigate to Shared Drives. Share the drives that you need to mount or copy to docker containers

Once you have read the documentation follow the steps on your own machine, Proxy Server URL for both http and https is: http://10.12.1.236:8083/





The Proxy server settings should propagate down to all Docker layers. If there are domains that your wish to exclude from using the proxy settings like your home network, add the IP address into the exclude section of the software to configure the "no_proxy" setting.

### Develop Remotely

If you are developing remotely, perhaps the easiest way to get around the proxy is to set up a virtual machine on an external service like Azure and depending on the OS, to use an RDP client or your favorite SSH client to tunnel in to remote virtual machine. Here again you have to know how to get outside of the Haufe proxy server and firewall. Once you are on your remote machine, you can install docker and create docker solutions without the normal networking constraints. 












