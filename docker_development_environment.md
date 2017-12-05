# The extended Docker environment

So what you have seen so far are the basic docker tools that you may use here at Haufe Group. What you have hopefully also noticed is that there is a tooling progression that makes using docker more efficient and speeds up development with Docker the higher-up you go on the toolchain.

One example would be that if you have started using Docker Compose, you should have less use for the Docker Engine CLI run command. That doesn't mean you won't need it, it just means you will need it less because it is much more convenient to to use Docker-Compose to create and spin up applications that can actually do something. You can do more with less.

That brings us to developing with Docker. Remember, one of our Docker principles is that Docker acts as packaging and orchestration technology for software. This is no different in the production environment.

Now that you are acquainted with Haufe Group Docker tooling, let's look at your Dev Env for working with Docker.

## Docker at dev-time

Reusing Docker packages - images - enables you to develop applications without lots of setup overhead, and being able to string multiple Docker images together to create a full-blown application environment with just one configuration file is definitely an advantage for you as a developer.

Theoretically, these images don't even have to be of the same technology stack to interoperate with each other and, realistically, Docker images can run in any environment where you can install docker. If you have read up to now, you shouldn't have to be asking yourself,"What the hell can Docker do for my development?". Now that you can pull and extend images, and compose these images into coordinated services to create applications, you can incorporate Docker into your normal dev workflow by:

* Packing your software into new Docker images that "contain" a single reusable process - Dockerfile\(s\)
* Reuse these images and images from others to extend to create composed services - docker-compose.yml

Naturally, it's a lot easier to develop with an IDE.

## IDE Support

IDEs are also starting to support developing with Docker from within the IDE environment.  IDE dev teams are still developing their Docker support offerings and all have different levels of support for both the Docker toolchain and for the different application frameworks that they support. Here is a rundown on the Docker capabilities for some well-known IDEs.

### Visual Studio / .NET et al.

We have many Microsoft-technology-based products. For these products, developing in a native Microsoft environment is probably a good idea. In addition to provisioning Docker Hosts on Azure with Docker Machine, to support development with Docker, Microsoft has created [Visual Studio Tools for Docker](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.VisualStudioToolsforDocker-Preview). The level of support and how docker is supported \(**toolchain up to Docker Compose**\) for "VS Tools for Docker" is still evolving.

Microsoft enables developers to add native docker support in Visual Studio **for .NET Core projects**. Much of Microsoft's Visual Studio Docker Support Documentation can be found at [Visual Studio Tools](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.VisualStudioToolsforDocker-Preview). Support here is  still pretty rudimentary, and so it is kind of awkward how Docker Compose files are placed in the project, but it's coming along... Docker and Microsoft are teaming up to and sometime soon Docker may support Windows containers. To see what Microsoft and Docker are up to take a look [here](https://www.simple-talk.com/cloud/platform-as-a-service/windows-containers-and-docker/) and here.

## Eclipse / Java et al.

Eclipse is also moving toward supporting Docker development, and there are already [Eclipse plugins](https://marketplace.eclipse.org/search/site/%2522Docker%2522) in the marketplace for creating, running and managing **Docker images and containers**. For the moment it looks like docker engine is the only supported tooling. So here too, the Eclipse folks are just getting started.

## Intellij IDEA, PHP Storm / Java, PHP, JavaScript et al.

Intellij has perhaps the [most support for Docker](https://www.jetbrains.com/help/idea/2016.2/docker.html). Both the IDEA IDE and its stripped down cousin PHP Storm have support for **docker tooling up to Docker compose**

Another example: Currently, the only Docker technology supported by Haufe Group release engineering is building docker images to the Haufe Group Docker Registry.

## Cloud Environments

Cloud providers are very docker friendly and major cloud players like Azure, AWS and Digital Ocean all offer native support for Docker. They are even beginning to offer Administrating and Operating services for containers. While Docker has proven problematic for some of the product offerings from cloud "as a service" providers, they are embracing the technology.

### Azure

Microsoft Azure premiere service for Docker is its [Azure Container Service](https://azure.microsoft.com/en-us/services/container-service/) for enabling native hosting, deployment, monitoring and management of containers natively. But there are more services including [Docker on Ubuntu VM](https://azure.microsoft.com/en-us/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/), [Docker Datacenter](https://azure.microsoft.com/en-us/marketplace/partners/docker/dockerdatacenterdocker-datacenter/), and a [VM that enables deploying Docker Apps to Red Hat Open Shift](https://azure.microsoft.com/en-us/marketplace/partners/click2cloud-inc/click2cloud-devops-cloud-solution/). We probably don't want to use this last one.

### Amazon Web Services

AWS has their [EC2 Container Service](https://aws.amazon.com/ecs/?nc2=h_m1) as part of their EC2 service for launching and managing containers - EC2CS integrates with other services like the load balancing service. Amazon also has [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/), which focuses on deploying applications and auto-scaling these applications as needed to handle load.

### Digital Ocean

Digitial Ocean also enables you to create [Docker servers](https://www.digitalocean.com/products/one-click-apps/docker/) with one click. Digital Ocean is more on the IaaS side of cloud services but they have been working closely with Docker to support container technology.

It is important to note that you can provision Docker hosts on all of these cloud service providers using docker-machine. The acceptance for Docker is wide and their are many options where you can deploy and manage your docker apps in the cloud. Even if some of these services aren't what we would select in a production environment, it is interesting to see that the big providers are developing them. This next section may be more interesting for Haufe Group.

## Container Orchestration and Management Software

This software is designed to deploy and manage container applications in production. There are many offerings at the moment but here we link to some of this software that may be put to use here at Haufe Group. Interesting about this software are the functions they automate - deploying and managing containerized applications. 

### Kubernetes

According to Kubernetes \(K8s\):

> Kubernetes is an open-source platform for automating deployment, scaling, and operations of application containers across clusters of hosts, providing container-centric infrastructure.  
> With Kubernetes, you are able to quickly and efficiently respond to customer demand:
>
> * Deploy your applications quickly and predictably.
> * Scale your applications on the fly.
> * Seamlessly roll out new features.
> * Optimize use of your hardware by using only the resources you need.
>   
> Our goal is to foster an ecosystem of components and tools that relieve the burden of running applications in public and private clouds.

### Swarm

### Rancher



