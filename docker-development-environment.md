# My Docker development environment - Draft

So what you have seen so far are the basic docker tools that you may use here at Haufe Group. What you have hopefully also noticed is that there is a tooling progression that makes using docker more efficient and speeds up development with Docker. One example would be that if you have started using Docker Compose, you should have less use for the Docker Engine CLI. That doesn't mean you won't need it, it just means you will need it less because it is much more convenient to to use Docker-Compose to create and spin up applications that can actually do something.

That brings us to developing with Docker. Remember, one of our Docker principles is that Docker acts as packaging and orchestration technology for software. This is no different in the production environment.  

Fortunately Docker is not work-intensive. So, if you are packaging your software using docker, the only difference to what you are doing right now is that that you pack your software into a Docker image when you are ready to merge up the next version of your software.

Now that you are acquainted with Haufe Group Docker tooling, let's look at your Dev Env for working with Docker. 

## Docker at dev-time
Reusing Docker packages - images - enables you to develop applications without lots of setup overhead, and being able to string multiple Docker images together to create a full-blown application environment with just one configuration file is definitely an advantage for you as a developer. 

Theoretically, these images don't even have to be of the same technology stack to talk to each other and, realistically, Docker images can run in any environment where you can install docker. If you have read up to now, you shouldn't have to be asking yourself,"What the hell can Docker do for my development?". Now that you can pull and extend images, and compose these images into coordinated services to create applications, you can incorporate Docker into your normal dev workflow by:

* Packing your software into new Docker images that "contain" a single reusable process - Dockerfile(s)
* Reuse these images and images from others to extend to create composed services - docker-compose.yml

Naturally, it's a lot easier to develop with an IDE. 

## IDE Support
IDEs are also starting to support managing docker from within the IDE environment.  IDE dev teams are still developing their Docker support offerings and all have different levels of support for both the Docker toolchain and for the different application framworks that they support. Here is rundown on the Docker capabilities for some well-known IDEs.

### Visual Studio / .NET et al.

We have many products developed with Microsoft Products. For these products developing in a native Microsoft environment is probably a good idea. In additon to provisioning Docker Hosts on Azure with Docker Machine, to support development with Docker, Microsoft has created [Visual Studio Tools for Docker](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.VisualStudioToolsforDocker-Preview). The level of support and how docker is supported (**toolchain up to Docker Compose**) for "VS Tools for Docker" is still evolving.

Microsoft enables developers to add native docker support in Visual Studio **for .NETCore projects**. Most of Microsofts Docker Support Documentation can be found at [Visual Studio Tools](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.VisualStudioToolsforDocker-Preview). Support here is  still pretty rudimentary, and so it is kind of awkward how Docker Compose files are placed in the project, but it's coming along...

## Eclipse / Java et al.
Eclipse is also moving toward supporting  Docker, and there are already [Eclipse plugins](https://marketplace.eclipse.org/search/site/%2522Docker%2522) in the marketplace for creating, running and managing **Docker images and containers**. For the moment it looks like docker engine is the only supported tooling. So here too, the eclipse folks are just getting started. 

##Intellij IDEA, PHP Storm / Java, PHP, JavaScript et al.
Intellij has perhaps the [most support for Docker](https://www.jetbrains.com/help/idea/2016.2/docker.html). Both the IDEA IDE and its stripped down cousin PHP Storm have support for **docker tooling up to Docker compose**

Another example: Currently, the only Docker technology supported by Haufe Group release engineering is building docker images to the Haufe Group Docker Registry. 





