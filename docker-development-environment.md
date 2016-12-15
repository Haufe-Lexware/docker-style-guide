# My Docker development environment - Draft

So what you have seen so far are the basic docker tools that you may use here at Haufe Group. What you have hopefully also notices is that there is a tooling progression that makes using docker more efficient. One example would be that if you have started using Docker Compose, you should have less use for the Docker Engine CLI. That doesn't mean you won't need it, it just means you will need it less because it is much more convenient to to use Docker-Compose to spin up applications that can actually do something.

That brings us to developing with Docker. Remember, one of Docker principles is that Docker acts as packaging and orchestration technology for software. If you are packaging your software using docker, the only difference that that you pack your software into a Docker image, when you are ready to merge up the next version of your software. Right now - end of 2016 - is a good time to get started with Docker, because    Haufe Group is also just getting started. 

Understanding how to use the Docker toolset and being able to develop professional software applications using Docker are two different things. Now that you are acquainted with accepted Haufe Group Docker tooling, let's look at your Dev Env for working with Docker. Another example: Currently, the only Docker technology supported by Haufe Group release engineering is building docker images to the Haufe Group Docker Registry. 

We have already said that the Docker is primarily a mechanism for packaging and orchestrating software applications, and you may have noticed that you can mount(our copy) a local folder into a Docker image by mounting a volume. So you know you can update your docker image by simply rebuilding the image after you make changes to your software. Let's take a look about what kind of support development environments have for Docker.

Web Technologies have already embraced Docker and there are many Docker images to get you started developing containerized web applications written in just about any well known languages.There is a huge community of developers who are creating new images everyday, essentially containerizing development environments that you can pull and start using.  

## Docker at dev-time
Let's review some of the concepts of Docker again quickly. Docker is all about packaging applications. Reusing these packages - images, composed services and so on - to develop images applications without lots of setup overhead by stringing multiple Docker images together to crete a full-blown application environment is definitely an advantage. Theoretically, these images don't even have to be of the same technology stack to talk to each other and, realistically, Docker images can run from anywhere where you can install docker. If you have read this book, you shouldn't have to be asking yourself,"What the hell can Docker do for my development?". Now that you can pull and extend images, and compose these images into coordinated services to create applications, you can incorporate Docker into your normal dev workflow by:

* Packing your software into new Docker images that "contain" a single reusable process - Dockerfile
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


## How to pull images from the Haufe Group Docker Registry





