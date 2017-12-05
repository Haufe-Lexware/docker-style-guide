# Installing Docker

The Docker installation that you use locally is completely up to you. Docker comes in several different flavors. If you want to do something with Docker, it still makes the most sense to install Docker in a Linux environment. Right now, on my machine, with Docker for Windows installed, and I still experience difficulties using Docker-Machine to manage my Docker hosts - although I have been able to get through the Docker Swarm tutorial by now.

Official Docker documentation has excellent and comprehensive instructions on how to install docker [at this location](https://docs.docker.com/engine/getstarted/step_one/) . Here the Docker Docs step you through doing a basic install of docker for your flavor of operating system and how to test Docker by running the "hello world" Docker image. Specific links are:

* [Install Docker for Windows](https://docs.docker.com/docker-for-windows/install/)
* [Install Docker for Mac](https://docs.docker.com/engine/installation/mac/)
* [Install Docker for Linux](https://docs.docker.com/engine/installation/)

### Building blocks for working with Docker

While you can run Docker on just about any kind of OS, Docker hosts and containers are always Linux-based. This may change, but it's still important to get familiar with basic Linux commands and Linux executable and utility commands - for example how to use "apt" or "curl" for retrieving and updating new packages on Ubuntu Linux and permissions basics like "chown", "chmod".

Once you get docker installed, you are going to start working with:

* [Registries](https://docs.docker.com/docker-hub/)
* [Images](https://docs.docker.com/engine/understanding-docker#docker-images)
* [Containers](https://docs.docker.com/engine/understanding-docker#docker-containers)

Later you will be working with Docker environments and Docker services

**Achtung:** If you are running on Windows, it helps to download a git client and then to install so you can run Linux commands in Powershell or DOS prompt. If your CI-pipeline includes Git this makes sense anyway. Also you need the Linux shell to be able to run more powerful commands that you can't run in a Windows shell - [like removing all containers or all images](https://techoverflow.net/blog/2013/10/22/docker-remove-all-images-and-containers/). Docker is making this easier with commands like prune but you still get more power with Linux.

## Using Docker inside the Haufe Network

If you plan to use Docker from the offices in Freiburg, You have to ensure that the Haufe Proxy and the Haufe Firewall do not block your Docker Engine from communication with the internet. Since you are going to go out and get images from Docker Hub and other repositories. There are a couple of workarounds here.

If you must set a proxy server please use: `proxy.haufemg.com:8083/`

You can also arrange other solutions with our ICT department. To do so, please contact them.

### Docker on Linux

Things change but right now it looks like Docker for Windows and Docker for Mac still have some limitations, so it's better to work \(also\) with Docker on Linux. This is why linux comes first in this section.

After having installed Linux on a VM on my Windows machine, using HyperV, **I  recommend that you set up a dual-boot configuration on your dev machine or get hold of a second computer that has Linux as the operating system**.

If I run Docker on Linux, I would like to be able to leverage all of the features of Docker, including Docker Machine and swarm mode. The immediate problem I encountered with Linux was that I still could not network properly. Our ICT department helped me to fix this - and since then I've learned and re-learned much about Linux.

Our Docker practices for Docker Hosts allow you to use the following Linux distributions:

* [CentOS](https://docs.docker.com/engine/installation/linux/centos/)
* [Redhat](https://docs.docker.com/engine/installation/linux/rhel/)
* [Debian](https://docs.docker.com/engine/installation/linux/debian/)
* [Ubuntu](https://docs.docker.com/engine/installation/linux/ubuntu/)
* CoreOS - [CoreOS Container Linux](https://coreos.com/os/docs/latest/#running-coreos) is specifically designed for container infrastructure and [Docker in CoreOS](https://coreos.com/os/docs/latest/quickstart.html#container-management-with-docker) is supported OoTB.

For Linux, you can set the environment variables for your virtual machine – HTTP\_PROXY, HTTPS\_PROXY and NO\_PROXY - for the domains where you intend to work with Docker that are behind and not behind a proxy server. If you are using Docker Machine to create hosts you can set these environment variables at host-creation-time. More in this in the Docker Machine chapter.

### Docker for Windows and Docker for Mac

Go to the [Getting Started - Docker for Windows](https://docs.docker.com/docker-for-windows/) or [Getting Started - Docker for Mac](https://docs.docker.com/docker-for-mac/) and read up on how to access the settings. For the "Dockers For" tools you will have to:

* Share drives for Docker volumes
* Set proxy variables
* Set the no\_proxy variable

And you may have to:

* Change network settings

For the Docker for Windows or IOS, one nice feature is that you can configure the firewall to propagate down to the Docker Host level. You can also set “no\_proxy” exceptions from within the Docker Application.

**Editor's Note: Still need to write some more about networking for Linux installations. Also need to organize this section better.**

Even if you have already done this in the Docker for Windows / Mac settings. You may still have some problems building images.

It has also been difficult to start using Docker Swarm on a Windows Machine, using Hyper-V as the virtualization technology. I am still trying to work out all of the kinks with Docker for Windows. Because all of the Docker functionality doesn't "just work", it may be better to develop locally, test to see if it works and then push to a remote location to work with multiple hosts.

### Develop remotely

If the proxy server causes too much pain, perhaps the easiest way to get around the proxy is to set up a virtual machine on an external service like Azure and depending on the OS, to use an RDP client or your favorite SSH client to tunnel in to the remote virtual machine.

Here again you have to know how to get outside of the Haufe proxy server and firewall. Once you are on your remote machine, you can install docker and create docker solutions without the normal networking constraints. More on this in the "Development Environment" section. If you choose to do so, [you can install Docker on cloud services as well](https://docs.docker.com/engine/installation#on-cloud).

