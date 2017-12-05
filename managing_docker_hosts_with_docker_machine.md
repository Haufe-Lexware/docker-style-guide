# Docker Machine

The final piece of tooling in the basics section is the Docker Machine. According to Docker, Docker Machine used to perform the following tasks.

> * Install and run Docker on Mac or Windows
> * Provision and manage multiple remote Docker hosts
> * Provision Swarm clusters

We will mostly take a look at creating and managing hosts in this section. Remember a Docker Host is a Linux virtual machine that contains a Docker Daemon. In production, it is important to be able to create and manage hosts for many reasons. One of the reasons is data security. For example, the Haufe Docker Guide states that

> For each customer that uses a dockerized application, you must create a separate host machine.

Docker's [Docker-Machine overview](https://docs.docker.com/machine/overview/) is a good place to go to get a basic understanding of Machines's role in the Docker tooling environment. Additionally, [understanding Docker Machine concepts](https://docs.docker.com/machine/concepts/) is also a good for starting to work with Docker Machine.

It's good to note, if you do decide to use Docker Machine to create hosts, you will be working directly with the boot2docker .iso image.

## Create and manage your Docker hosts with Docker-Machine

With docker machine, you can create as many hosts as you like. You manage hosts with the Docker-Machine CLI. Up to now, you should have been able to do all of the docker exercises, because docker installs a "default" host machine at installation. This is great for testing dockerized applications, but for development, you will create many Docker Hosts - both for different customers and for different applications. And so, it's important to have good data labels to be sure that you are working on the right VM!

One of the nice things about working with Docker for Windows / Mac is that Docker Machine is installed along with the other tools by the installer. If you have Linux you must [install Docker Machine separately](https://docs.docker.com/machine/install-machine/).

The Haufe Style Guide has [Docker-Machine practices](https://github.com/Haufe-Lexware/docker-style-guide/blob/master/DockerMachine.md), but you only have to start thinking about them when you start to deploy remote hosts.

Again, Docker has fantastic documentation on all of its tooling and the [Docker-Machine documentation](https://docs.docker.com/machine/get-started/) is no exception: So it's a good idea to work through this "getting started" tutorial. Since you are just getting started, you can stay local and skip the "provisioning a host" in the cloud part if you like.

**Achtung:** Be sure to name your Docker Host Machines extremely well: While there is no official naming convention a transparent naming system with **Application, Customer** and other relevant information is important so you know what's running on your host machines.

[This tutorial](https://rominirani.com/docker-toolbox-setup-windows-4d65c3f691eb#.694oqa466) can get you up to speed with some of the basic Docker Machine commands, including how to create a host and how to use `docker-machine env <hostname>`and`docker-machine ssh <hostname>`to select and to work with a specific host from console. Again, this tutorial was designed for Docker Toolbox, so if Machine is already installed, you want to skip to the part with the commands. Also remember, if you are working on Hyper V hosts and Docker Machine stops working, you can continue to work with your hosts by SSHing in with an SSH client or by connecting to each host individually

## Creating boot2docker hosts with Docker Machine

With the advent of Docker release 1.13.x, Creating hosts with Docker Machine and Hyper V works much better now. There are still some network issues that need to be tackled, but I was able to create hosts with Machine and I have also been able to create a swarm and begin working through the swarm tutorial.

Some things to be aware of when you are working with Docker Machine and HyperV here at Haufe Group.

1. Virtual switches must be external and connected to a physical network adapter
2. The physical network adapter must support IPv4 so that it assigns an IPv4 IP address to your Docker Host/VM: Docker will need this to pull images from registries outside of the firewall.
3. You must work out a solution with ICT to enable your Virtual machines to tunnel out of the proxy server: I have been provided a solution where I must install a registry key and then set a custom proxy script in my internet connection settings.
4. You must specify the correct virtual switch with the `--hyperv-virtual-switch` Docker command option at `docker-machine create` time.
5. When creating a host you must set, at least, the `HTTP_PROXY`_ \_and_ \_`HTTPS_PROXY`environment variables at `docker-machine create` time

Still extremely annoying is that, at create-time, docker-machine still cannot tunnel out and download the latest version of Docker Engine. So, I have to download the ISO by hand and add it to the cache folder in my Docker home directory. But, you can also run `docker-machine upgrade <yourhostname>` to upgrade to the latest version of Docker Engine!? Another pain point about Docker for Windows and hosts created with the Hyper V driver, is that often the hosts are no longer manageable from Docker Machine, showing a status of timeout. To work around you have to SSH into individual machines with an SSH client like putty, using the c[redentials for the docker user](http://stackoverflow.com/questions/30330442/how-to-ssh-into-docker-machine-virtualbox-instance) or using an SSH certificate. Or you must create new hosts. 

**Achtung**: Please make sure to set up your networking before you run `docker-machine create`, otherwise you must create new certificates for your docker host with `regenerate-certs` before your Docker hosts can talk to each other. Please also remember that, if you are working from a console like powershell, you must have administrator rights to create new hosts!

Once this environment is configured, you can create boot2docker image Docker Hosts on you machine that network with each other over the Docker Network and with the internet.

To help you get started with this, there is a batch file that sequentially creates three Docker Hosts in the examples folder. **Please rename the generic virtual switch and host names before running**. With three nodes you can perform the [Docker Swarm tutorial](https://docs.docker.com/engine/swarm/swarm-tutorial/)!

## Docker Machine commands

Docker machine also has a CLI, the following table contains some of the important commands. As usual, the best reference though is the [docker machine command line reference](https://docs.docker.com/machine/reference/).

| Command | Description |
| :--- | :--- |
| ls | lists all docker hosts that you have created, these hosts' information, and which host is currently active. |
| create | Creates a new host. At create-time you have to [supply a driver for your environment](https://docs.docker.com/machine/drivers/). |
| ssh | SSH into the host shell directly from console. |
| url | Print the URL of a host machine to stdout. |
| active | Print your active Docker host. |
| start, stop, kill, rm | Start, stop, kill, and remove hosts. |
| env | Display commands to set up host environment for the machine CLI. You need this to work with a specific host or to switch hosts from a single shell! |

## Provision remote hosts with Machine

With Docker Machine you can also create hosts in the cloud. You can work these tutorials to provision Docker hosts locally and in the cloud:

* [Local Docker Host](https://docs.docker.com/machine/get-started/)
* [Docker Host on AWS](https://docs.docker.com/machine/examples/aws/)
* [Docker Host on Digital Ocean](https://docs.docker.com/machine/examples/ocean/)
* [Docker Host on Microsoft Azure](https://docs.microsoft.com/en-us/azure/vs-azure-tools-docker-machine-azure-config)

## Section targets

When you are done with this section, you should be able to:

* Create a new Docker Host 
* Know how to use Docker Machine commands
* Discover important information about your host \(inspect, port, url, ip\)
* Select and switch hosts that contain different images
* Create \(and clean up\) remote Docker hosts on cloud service providers
